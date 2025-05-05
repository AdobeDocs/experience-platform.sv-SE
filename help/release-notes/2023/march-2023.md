---
title: Versionsinformation om Adobe Experience Platform mars 2023
description: Versionsinformationen för Adobe Experience Platform i mars 2023.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 26%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 29 mars 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Experience Data Model](#xdm)
- [Frågetjänst](#query-service)
- [Real-Time Customer Data Platform B2B-utgåva](#b2b)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner** {#dashboards-new-updated-features}

| Funktion | Beskrivning |
| --- | --- |
| Användardefinierade kontrollpaneler | Du kan nu **sampla attributvärden** innan du lägger till ett attribut i en widget i den användardefinierade widgetdispositionen för instrumentpaneler. Ett fåtal exempelvärden från den attributkolumnen är tillgängliga för enskilda attribut när du skapar en widget.<br>Du kan nu **byta X- och Y-axel** i widgeten mot utbytesaxelknappen. Detta sparar tid och ger en mer ergonomisk upplevelse när du lägger till attribut i widgetar. Den här sparningen måste hitta båda attributen igen från attributpanelen.<br> Du kan nu **ändra plats och rubrik för teckenförklaringen** i dina widgetar. När det finns en teckenförklaring på en widget kan du flytta den var som helst runt diagrammet och även ge den ett nytt namn, som du kan med axeletiketter och widgetens rubrik. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nytt snabbstartsarbetsflöde för Meta Conversions API (Beta) | Få tillgång till nya arbetsflöden för snabbstart under ”Komma igång” från startskärmen för datainsamling! Med [snabbstartsarbetsflödet för Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=sv-SE#quick-start) kan kunderna snabbt samla in och vidarebefordra händelsedata, från serversidan till Meta för annonskonverteringar med bara några få enkla steg. |
| Nytt snabbstartsarbetsflöde för Mobile SDK (Beta) | Få tillgång till nya arbetsflöden för snabbstart under ”Komma igång” från startskärmen för datainsamling! Med [snabbstartsarbetsflödet för Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) kan du snabbt implementera Mobile SDK och validera grundläggande mobilhändelser i några enkla steg. |
| [!DNL Braze]-tillägg för händelsevidarebefordring | Med tillägget [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=sv-SE) för vidarebefordran av händelser kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka det till [!DNL Braze] i form av händelser på serversidan med API:erna för användarspårning i [!DNL Braze]. |
| [!DNL Epsilon]-tillägg för händelsevidarebefordring | Med tillägget [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=sv-SE) kan du utnyttja händelsevidarebefordran för att hämta händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Epsilon] med hjälp av [!DNL Epsilon] Event API. |
| [!DNL Mixpanel]-tillägg för händelsevidarebefordring | Tillägget [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=sv-SE) gör det möjligt för kunder att utnyttja händelsevidarebefordran för att hämta händelseinformation i Adobe Experience Platform Edge Network och skicka den till Mixpanel med API:t för spårningshändelser. |

{style="table-layout:auto"}

## Dataförberedelse {#data-prep}

Med dataförberedelse kan utvecklare mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgång till filtrering av Adobe Analytics-data | Ni kan nu använda funktionerna för dataförberedelser för att tillämpa regler och villkor för att filtrera era era analysdata innan ni hämtar dem till kundprofilen i realtid. Mer information finns i handboken om [filtrering av analysdata för profilintagning](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nya funktioner för kodning och avkodning av URL-strängar | <ul><li>Funktionen `get_url_encoded` tar en URL som indata och ersätter eller kodar specialtecken med ASCII-tecken.</li><li>Funktionen `get_url_decoded` tar en URL som indata och avkodar ASCII-tecken till specialtecken.</li></ul> Mer information finns i handboken [Dataförberedelser ](../../data-prep/functions.md). En omfattande lista över reserverade tecken och deras motsvarande kodade tecken finns i handboken om [specialtecken](../../data-prep/functions.md#special-characters). |

Mer information om dataprep finns i [översikten för dataprep](../../data-prep/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] anslutning GA](../../destinations/catalog/personalization/adobe-commerce.md) | Med målanslutningen [!DNL Adobe Commerce] (som nu är allmänt tillgänglig) kan du välja en eller flera Real-Time CDP-målgrupper att aktivera för ditt [!DNL Adobe Commerce]-konto för att leverera en dynamisk, personlig upplevelse till era kunder. |
| [[!DNL Snap Inc] anslutning GA](../../destinations/catalog/advertising/snap-inc.md) | Med målkopplingen [!DNL Snap Inc] (som nu är allmänt tillgänglig) kan marknadsförare importera användarsegment som skapats i Experience Platform till [!DNL Snapchat Ads] och använda dem för att rikta sina annonser. |
| [(API) Oracle Eloqua-anslutning](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Använd den API-baserade anslutningen till [!DNL Oracle Eloqua] för att planera och köra kampanjer samtidigt som en anpassad kundupplevelse för deras potentiella kunder i [!DNL Oracle Eloqua] levereras. |
| [(Beta) [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | Integrationen [!DNL Amazon Ads] med Adobe Experience Platform ger körklar integrering med [!DNL Amazon Ads]-produkter, inklusive [!DNL Amazon DSP (ADSP)]. Med målplatsen [!DNL Amazon Ads] i Adobe Experience Platform kan användare definiera annonsörer för målinriktning och aktivering på [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] anslutning](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (tidigare Bizible) ger marknadsförarna insikt i vilka marknadsföringssatsningar som är mest effektiva när det gäller att öka intäkterna och maximera avkastningen på investeringen för deras företag. Målet möjliggör dataflöden mellan företag (B2B) från Adobe Experience Platform till [!DNL Marketo Measure]. Kortet är bara tillgängligt för [!DNL Marketo Measure Ultimate] kunder. |
| [TikTok-anslutning](../../destinations/catalog/social/tiktok.md) | Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. |
| [Zendesk-anslutning](../../destinations/catalog/crm/zendesk.md) | Använd det här målet om du vill skapa och uppdatera identiteter inom ett segment som kontakter inom [!DNL Zendesk]. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Ny åtkomstkontrollbehörighet för mål: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | Den nya behörigheten ger användarna möjlighet att aktivera segment till befintliga mål, utan att visa [mappningssteget](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Användare kan lägga till och ta bort segment i aktiveringsarbetsflöden, men kan inte lägga till eller ta bort mappade attribut eller identiteter. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

Vi släpper en felkorrigering för PGP/GPG-kryptering i filbaserade mål för Real-Time CDP. Den här ändringen innebär att befintliga filbaserade mål som använder kryptering genererar ett filnamn med ett annat filtillägg än tidigare.

- Aktuellt tillägg vid användning av kryptering: `filename.csv`
- Framtida tillägg vid användning av kryptering: `filename.csv.gpg`

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| CSV till schemarapport | Du kan nu överföra dina lokala filer för att skapa scheman som genereras av maskininlärning och som eliminerar behovet av att skapa ett schema manuellt. Ladda upp en CSV-exempelfil från arbetsytan [!UICONTROL Sources], så föreslår Adobe maskininlärningsalgoritmer ett schema åt dig baserat på målfälten. Mer information finns i [dokumentationen](../../ingestion/tutorials/map-csv/recommendations.md).&quot; |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL Offer Item]](https://github.com/adobe/xdm/pull/1678/files) | En klass som representerar ett erbjudande. |
| Klass | [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1678/files) | En artikel som kan bli föremål för beslut. Resultatet av en beslutsprocess är en eller flera beslutsposter. |
| Klass | [[!UICONTROL Media Session Server Timeout]](https://github.com/adobe/xdm/pull/1676/files) | Detta anger hur lång tid (i sekunder) som har gått mellan användarens senaste kända interaktion och tidpunkten då sessionen stängdes. |
| Fältgrupp | [[!UICONTROL XDM Profile Computed Attributes]](https://github.com/adobe/xdm/pull/1686/files) | Detta lägger till beräknade attribut från interna Adobe-tjänster till inkommande kunddata. Detta bör inte användas av kunder för att importera data. |
| Datatyp | [[!UICONTROL Refund Item]](https://github.com/adobe/xdm/pull/1685/files) | Anger om en återbetalning är kopplad till en order och definierar typ av återbetalning, belopp och associerad valuta. |
| Datatyp | [[!UICONTROL Category data]](https://github.com/adobe/xdm/pull/1677/files) | Den här nya datatypen representerar kategorin för en produkt. |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1682/files) | Ett nytt XDM-schema skapades för målklassificeringsdatamängder. Det innehåller en uppsättning metadatafält som klassificerar Target-aktiviteter och -upplevelser. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL Content Component Details]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` togs bort från [!UICONTROL Content Component Details] |
| Fältgrupp | [[!UICONTROL AJO Entity tags]](https://github.com/adobe/xdm/pull/1672/files) | AJO Entity-taggar har lagts till i [!UICONTROL AJO Entity Fields], som motsvarar en resa eller kampanj |
| Fältgrupp | (Flera) | Flera fält har lagts till för [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/pull/1671/files) |
| Fältgrupp | (Flera) | [Flera XDM-händelsetyper har lagts till för [!UICONTROL Media Reporting]](https://github.com/adobe/xdm/pull/1670/files). |
| Fältgrupp | [!UICONTROL Workfront Change Event] | Fältgrupperna `Full Record` och `Accessor Employee Ids` lades till. |
| Datatyp | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refund Amount] lades till för att ange det belopp som återbetalats för artikeln, om någon. |
| Datatyp | [[!UICONTROL Order &#x200B;]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refunds List] har lagts till i listan över återbetalningar för den här ordern. |
| Datatyp | [[!UICONTROL Product List Item &#x200B;]](https://github.com/adobe/xdm/pull/1677/files) | Produktkategorierna har lagts till i listan över kategoridata för den här produkten. |
| Datatyp | [!UICONTROL Session details information] | `pev3`-strängfältet som [anger vilken typ av medieström som används för rapportering](https://github.com/adobe/xdm/pull/1676/files) har lagts till. Egenskapen `pccr` har också lagts till och anger om en omdirigering har gjorts. |
| Datatyp | [!UICONTROL Requisition List] | Tillhandahåller egenskaperna för [rekvisitionslistan](https://github.com/adobe/xdm/pull/1675/files). De innehåller namn, ID och beskrivning. |
| Datatyp | [!UICONTROL Commerce] | Datatypen [Commerce har uppdaterats](https://github.com/adobe/xdm/pull/1675/files) så att den omfattar `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` och `requisitionList`. |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från datasjön och fånga upp sökresultaten som en ny datauppsättning för användning i rapportering, arbetsyta för datavetenskap eller för inmatning i kundprofil i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Attributbaserad åtkomstkontroll i det accelererade arkivet | Använd attributbaserad åtkomstkontroll med Data Distiller för att definiera åtkomstkontroll för alla datauppsättningar i det accelererade arkivet. Detta styr åtkomsten till anpassade datamodeller som skapats av användare och lagrats på en accelererad butik för att styra anpassade instrumentpaneler. |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [översikten över frågetjänster](../../query-service/home.md).

## Real-Time Customer Data Platform B2B-utgåva {#b2b}

Real-Time CDP B2B edition bygger på Real-Time Customer Data Platform (Real-Time CDP) och är utformat för marknadsförare som arbetar i en affärs-till-affärstjänstmodell. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Bugfix | För att profilerna ska återges mer korrekt i systemet, inkluderar systemet inte längre interna profiler i det totala antalet profiler eller adresserbara målgruppsmått för Real-Time Customer Data Platform B2B edition. Från och med idag kan du se en engångsminskning av det totala antalet profiler/adresserbara målgruppsmått. Inga data har raderats, det här är bara en ändring av antalet. Kontakta din Adobe-chef om du har några frågor |

{style="table-layout:auto"}

Läs [Real-Time CDP B2B edition overview](../../rtcdp/overview.md) om du vill veta mer om Real-Time CDP B2B edition.

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilmått | För att ni ska få en mer korrekt återgivning av profilmätvärden kombineras uppdelning efter medlemskap och omsättningsstatistik och beräknas nu över en 24-timmarsperiod. Mer information finns i [Användargränssnittsguiden för segmentering](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Beta-tillgänglighet för [!DNL Chatlio] | [!DNL Chatlio]-källan är nu tillgänglig i betaversion. Använd [!DNL Chatlio]-källan för att strömma dina [!DNL Chatlio]-händelsedata till Experience Platform. Mer information finns i [[!DNL Chatlio] översikten](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Beta-tillgänglighet för [!DNL Customer.io] | [!DNL Customer.io]-källan är nu tillgänglig i betaversion. Använd källan [!DNL Customer.io] för att strömma dina kundhändelsedata till Experience Platform. Mer information finns i [[!DNL Customer.io] översikten](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Beta-tillgänglighet för [!DNL Pendo] | [!DNL Pendo]-källan är nu tillgänglig i betaversion. Använd [!DNL Pendo]-källan för att strömma produktanalysdata till Experience Platform. Mer information finns i [[!DNL Pendo] översikten](../../sources/connectors/analytics/pendo-webhook.md). |
| Stöd för dataflöden | Du kan nu använda API:t för Flow Service för att ställa in dataflödena till ett utkasttillstånd. Ritade dataflöden kan senare uppdateras och publiceras med ny information. Mer information finns i guiden om att [ställa in källans dataflöden som utkast](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Mer information om källor finns i [översikten över källor](../../sources/home.md).
