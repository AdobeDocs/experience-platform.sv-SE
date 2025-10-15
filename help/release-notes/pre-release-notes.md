---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: de95e9a51c979e9249ddf9ceb262fc521d2b38f4
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 30%

---

# Information om förhandsversionen av Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet är avsett som en **förhandsgranskning** av versionsinformationen för den aktuella månaden. Utgivningsobjekt kan ändras och kan läggas till eller tas bort i den slutliga versionen.

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: oktober 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [Mål &#x200B;](#destinations)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Varning om felfrekvens för destinationen | En ny avisering har lagts till för mål: **Målets felfrekvens överskrider tröskelvärdet**. Den här varningen meddelar dig när antalet misslyckade poster under dataaktiveringen har överskridit det tillåtna tröskelvärdet, vilket gör att du snabbt kan åtgärda aktiveringsproblem. |

{style="table-layout:auto"}

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../observability/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [!DNL AdForm] | Använd det här målet för att skicka Adobe Real-Time CDP-målgrupper till [!DNL AdForm] för aktivering baserat på Experience Cloud ID (ECID) och [!DNL AdForm]s ID Fusion. ID Fusion för [!DNL AdForm] är en ID-matchningstjänst som gör att du kan aktivera dina första målgrupper baserat på Experience Cloud ID (ECID). |
| [!DNL Amazon Ads] | Vi har lagt till ytterligare stöd för personliga identifierare som `firstName`, `lastName`, `street`, `city`, `state`, `zip` och `country`. Genom att mappa dessa fält som målidentiteter kan ni förbättra målgruppernas matchningsfrekvens. |
| [!DNL Snowflake Batch] (begränsad tillgänglighet) | Skapa en [!DNL Snowflake]-dataresurs live för att ta emot dagliga målgruppsuppdateringar direkt som delade tabeller till ditt konto. Den här integreringen är för närvarande tillgänglig för kundorganisationer som etablerats i VA7-regionen. |
| [!DNL Snowflake Streaming] (begränsad tillgänglighet) | Skapa en [!DNL Snowflake]-dataresurs live för att ta emot uppdateringar för direktuppspelad målgrupp direkt som delade tabeller till ditt konto. Den här integreringen är för närvarande tillgänglig för kundorganisationer som etablerats i VA7-regionen. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för [!DNL AES256]-kryptering på serversidan i [!DNL Amazon S3] mål | [!DNL Amazon S3] mål har nu stöd för [!DNL AES256]-serversideskryptering vilket ger förbättrad säkerhet för exporterade data. Du kan konfigurera den här krypteringsmetoden när du konfigurerar eller uppdaterar [!DNL Amazon S3]-målanslutningar och ser till att dina data krypteras i vila med [!DNL AES256] -krypteringsalgoritmer som följer branschstandard. Mer information finns i [[!DNL Amazon] dokumentationen](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Flera nya mål som stöder övervakning på målgruppsnivå](../dataflows/ui/monitor-destinations.md#audience-level-view) | Följande mål har nu stöd för övervakning på målgruppsnivå: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Kontoengagemang för [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Åtgärda säkerhetsutkast för datauppsättningsexport | En korrigering har implementerats för datauppsättningens exportskyddsutkast. Tidigare behandlades vissa datauppsättningar som innehöll en tidsstämpelkolumn men _inte_ baserat på XDM Experience Events-schemat felaktigt som Experience Events-datauppsättningar, vilket begränsar exporten till ett 365-dagars uppslagsfönster. Det dokumenterade 365-dagars arbetsskyddsutkastet gäller nu enbart för Experience Events-datauppsättningar. Datamängder som använder något annat schema än XDM Experience Events-schemat styrs nu av 10 miljarder poster som skyddsprotokoll. Vissa kunder kan se ett ökat exportnummer för datauppsättningar som felaktigt föll under 365-dagars uppslagsfönstret. På så sätt kan du exportera datauppsättningar för prediktiva arbetsflöden som har ett långt uppslagsfönster. Mer information finns i [DATAuppsättningens exportskyddsutkast](../destinations/guardrails.md#dataset-exports). |
| Förbättrad rapportering på målgruppsnivå för företagsdestinationer | Förbättrad rapporteringslogik på målgruppsnivå för företagsdestinationer. Efter den här versionen kommer kunderna att se mer korrekta målgruppsrapporteringsnummer som endast innehåller målgrupper som är relevanta för det valda målet. Denna övervakningsjustering säkerställer att rapporteringen endast omfattar målgrupper som kartlagts i dataflödet, vilket ger tydligare insikter i den faktiska dataaktiveringen. Detta påverkar inte mängden data som aktiveras - det är endast en övervakningsförbättring som förbättrar rapporteringsnoggrannheten. |

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av strömningssegmentering | Realtidsövervakning för direktuppspelningssegmentering ger transparens vad gäller utvärderingsfrekvens, fördröjning och datakvalitetsstatistik på sandbox-, dataset- och målgruppsnivå. Detta stöder förebyggande varningar och åtgärdbara insikter som hjälper datatekniker att identifiera kapacitetsöverträdelser och problem med inmatning. Övervakningsmätningar inkluderar utvärderingshastighet, fördröjning av P95-intag samt mottagna, utvärderade, misslyckade och hoppade över poster. Funktioner för visa-för-data och visa-för-målgrupp ger omfattande insyn i nya profiler som är kvalificerade och diskvalificerade. |

Mer information finns i [[!DNL Segmentation Service] översikten](../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one]-källor för lojalitetsdata | Använd [!DNL Talon.One]-källorna för att importera grupper och strömma lojalitetsdata till Experience Platform. Kopplingen stöder strömning av profildata, transaktionsdata och lojalitetsdata, inklusive intjänade poäng, inlösta poäng, utgångna poäng samt skiktdata. |

**Uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för källan [!DNL Google Ads] (endast API) | API-versionen av [!DNL Google Ads]-källan är nu i allmän tillgänglighet. API-dokumentationen har uppdaterats för att återspegla att den senaste versionen nu är `v21`, och Experience Platform stöder alla versioner v19 och senare. Användargränssnittsversionen finns kvar i betaversionen och stöder endast engångsbruk. Använd API-vägen om du vill använda inkrementell datainhämtning. |
| Stöd för [!DNL Azure Event Hubs] virtuella nätverk | Adobe har nu uttryckligen stöd för virtuella nätverksanslutningar till Azure Event Hubs, vilket möjliggör dataöverföring över privata nätverk snarare än offentliga nätverk. Kunderna kan tillåtslista Experience Platform VNet för att dirigera Event Hubs-trafik privat via Azure privata stamnät, vilket ger förbättrad säkerhet och regelefterlevnad för arbetsflöden för dataöverföringar. |

Mer information finns i [översikten över källor](../sources/home.md).
