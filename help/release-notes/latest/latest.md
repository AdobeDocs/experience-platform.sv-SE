---
title: Versionsinformation om Adobe Experience Platform oktober 2025
description: Versionsinformationen för Adobe Experience Platform i oktober 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 28%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 22 oktober 2025**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Aviseringar](#alerts)
- [Mål](#destinations)
- [Real-Time CDP B2B Edition](#b2b)
- [Källor](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator är det nya agentiska lagret i Adobe Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Audience-agent | Audience Agent har nu stöd för kontobaserade målgrupper för att kunna utforska konversationer och upptäcka dubblerade målgrupper. Mer information finns i [dokumentationen om Audience-agent](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Mer information om agenter finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/home).

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Avisering om misslyckad aktiveringsfrekvens | En ny avisering har lagts till för mål: **Aktiveringsfel överskrider tröskelvärdet**. Den här varningen meddelar dig när antalet misslyckade poster under dataaktiveringen har överskridit det tillåtna tröskelvärdet, vilket gör att du snabbt kan åtgärda aktiveringsproblem. Läs dokumentationen om [standardregler för aviseringar](../../observability/alerts/rules.md) om du vill ha mer information. |

{style="table-layout:auto"}

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../../observability/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [!DNL Adform] | Använd det här målet för att skicka Adobe Real-Time CDP-målgrupper till [!DNL Adform] för aktivering baserat på Experience Cloud ID (ECID) och [!DNL Adform]s ID Fusion. ID Fusion för [!DNL Adform] är en ID-matchningstjänst som gör att du kan aktivera dina första målgrupper baserat på Experience Cloud ID (ECID). Mer information finns i [[!DNL Adform] dokumentationen](../../destinations/catalog/advertising/adform.md) |
| [!DNL Amazon Ads] | Ytterligare stöd för personliga identifierare har lagts till. Detta inkluderar fält som `firstName`, `lastName`, `street`, `city`, `state`, `zip` och `country`. Genom att mappa dessa fält som målidentiteter kan ni förbättra målgruppernas matchningsfrekvens. Mer information finns i [[!DNL Amazon Ads] dokumentationen](../../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Snowflake Batch] (begränsad tillgänglighet) | Skapa en [!DNL Snowflake]-dataresurs live för att ta emot dagliga målgruppsuppdateringar direkt som delade tabeller till ditt konto. Den här integreringen är för närvarande tillgänglig för kundorganisationer som etablerats i VA7-regionen. Mer information finns i [[!DNL Snowflake Batch] dokumentationen](../../destinations/catalog/warehouses/snowflake-batch.md). |
| [!DNL Snowflake Streaming] (begränsad tillgänglighet) | Skapa en [!DNL Snowflake]-dataresurs live för att ta emot uppdateringar för direktuppspelad målgrupp direkt som delade tabeller till ditt konto. Den här integreringen är för närvarande tillgänglig för kundorganisationer som etablerats i VA7-regionen. Mer information finns i [[!DNL Snowflake Streaming] dokumentationen](../../destinations/catalog/warehouses/snowflake.md). |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| [Flera nya mål som stöder övervakning på målgruppsnivå](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Följande mål har nu stöd för övervakning på målgruppsnivå: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Kontoengagemang för [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Åtgärda säkerhetsutkast för datauppsättningsexport | En korrigering har implementerats för datauppsättningens exportskyddsutkast. Tidigare behandlades vissa datauppsättningar som innehöll en tidsstämpelkolumn men _inte_ baserat på XDM Experience Events-schemat felaktigt som Experience Events-datauppsättningar, vilket begränsar exporten till ett 365-dagars uppslagsfönster. Det dokumenterade 365-dagars arbetsskyddsutkastet gäller nu enbart för Experience Events-datauppsättningar. Datamängder som använder något annat schema än XDM Experience Events-schemat styrs nu av 10 miljarder poster som skyddsprotokoll. Vissa kunder kan se ett ökat exportnummer för datauppsättningar som felaktigt föll under 365-dagars uppslagsfönstret. På så sätt kan du exportera datauppsättningar för prediktiva arbetsflöden som har ett långt uppslagsfönster. Mer information finns i [DATAuppsättningens exportskyddsutkast](../../destinations/guardrails.md#dataset-exports). |
| Förbättrad rapportering på målgruppsnivå för företagsdestinationer | Efter den här versionen kommer kunderna att se mer korrekta målgruppsrapporteringsnummer som endast innehåller målgrupper som är relevanta för det valda målet. Denna övervakningsjustering säkerställer att rapporteringen endast omfattar målgrupper som kartlagts i dataflödet, vilket ger tydligare insikter i den faktiska dataaktiveringen. Detta påverkar inte mängden data som aktiveras - det är endast en övervakningsförbättring som förbättrar rapporteringsnoggrannheten. |
| UI-nedtonade dataflöden på grund av åtkomstetiketter | För att åtgärda problemet där vissa användare såg tomma sidor eftersom måldataflöden som de inte hade tillgång till var helt dolda, visar nu gränssnittet dessa begränsade dataflöden i ett nedtonat läge i stället för att utelämna dem helt. Mer information finns i dokumentationen om [hur du använder åtkomstetiketter för att hantera användaråtkomst till måldataflöden](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know). |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B edition har omfattande funktioner för hantering av B2B-kunddata, vilket gör det möjligt för organisationer att skapa enhetliga kundprofiler, skapa sofistikerade B2B-målgrupper och aktivera data över olika marknadsföringskanaler.

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av B2B-stöd för icke-standardiserade relationer mellan B2B-enheter | Från och med januari 2026 har Real-Time CDP B2B edition inte längre stöd för **icke-standard**-relationer mellan B2B-enheter. Därför bör du uppdatera dina B2B-enheter så att de använder standardrelationerna som beskrivs i [B2B-namnutrymmen och schemaguiden](../../rtcdp/schemas/b2b.md). |

{style="table-layout:auto"}

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ändring av datauppsättning för Adobe Analytics-källa | Som en del av processen för att skapa dataflöden mellan Adobe Analytics och Experience Platform skapas en datauppsättning via katalogtjänsten. Den här datauppsättningen fungerar som en behållare för data som ska landas i. För närvarande innehåller den här processen ett DataSource-ID som hämtas från Analytics-rapportsviten, skickas till katalogtjänsten och sedan kopplas till den nya datauppsättningen. Efter ändringen är alternativet att ange ID för datakälla inte längre tillgängligt när datauppsättningar skapas. Därför kommer nya datauppsättningar som skapas av Analytics-källan inte längre att ha något associerat DataSource-ID i katalogtjänsten. Den här ändringen gäller endast för metadata och påverkar inte lagringen av data i datauppsättningen på något sätt. Det är dock viktigt att veta att det DataSource-ID som tillhandahålls av katalogtjänsten inte längre är tillgängligt i nya datauppsättningar för Adobe Analytics. Läs [Adobe Analytics källdokumentation](../../sources/connectors/adobe-applications/analytics.md) om du vill ha mer information om Adobe Analytics källanslutning. |
| Allmän tillgänglighet för källan [!DNL Google Ads] (endast API) | [API-versionen av  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md)-källan har nu generell tillgänglighet. API-dokumentationen har uppdaterats för att återspegla att den senaste versionen nu är `v21`, och Experience Platform stöder alla versioner v19 och senare. [Gränssnittsversionen ](../../sources/tutorials/ui/create/advertising/ads.md) finns kvar i betaversionen och stöder endast engångsbruk. Använd API-vägen om du vill använda inkrementell datainhämtning. |
| Stöd för [!DNL Azure Event Hubs] virtuella nätverk | Adobe har nu explicit stöd för virtuella nätverksanslutningar till [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), vilket aktiverar dataöverföring över privata nätverk i stället för offentliga nätverk. Kunderna kan tillåtslista Experience Platform VNet för att dirigera Event Hubs-trafik privat via Azure privata stamnät, vilket ger förbättrad säkerhet och regelefterlevnad för arbetsflöden för dataöverföringar. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->