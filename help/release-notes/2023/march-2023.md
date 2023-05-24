---
title: Versionsinformation om Adobe Experience Platform mars 2023
description: Versionsinformation mars 2023 för Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 29 mars 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Mål ](#destinations)
- [Experience Data Model](#xdm)
- [Frågetjänst](#query-service)
- [Real-Time Customer Data Platform B2B-utgåva](#b2b)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner** {#dashboards-new-updated-features}

| Funktion | Beskrivning |
| --- | --- |
| Användardefinierade kontrollpaneler | Nu kan du **samplingsattributvärden** innan du lägger till ett attribut i en widget i den användardefinierade widgetdispositionen för instrumentpaneler. Ett fåtal exempelvärden från den attributkolumnen är tillgängliga för enskilda attribut när du skapar en widget.<br>Nu kan du **byta X- och Y-axel** på widgeten med utbytesaxelknappen. Detta sparar tid och ger en mer ergonomisk upplevelse när du lägger till attribut i widgetar. Den här sparningen måste hitta båda attributen igen från attributpanelen.<br> Nu kan du **ändra förklaringens placering och rubrik** i widgetarna. När det finns en teckenförklaring på en widget kan du flytta den var som helst runt diagrammet och även ge den ett nytt namn, som du kan med axeletiketter och widgetens rubrik. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikt över instrumentpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nytt snabbstartarbetsflöde för Meta Conversions API (beta) | Kom åt nya snabbstartarbetsflöden via&quot;Komma igång&quot; från startskärmen för datainsamling! The [snabbstartsarbetsflöde för Meta Conversion API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) gör det möjligt för kunderna att snabbt samla in och vidarebefordra händelsedata, från serversidan till Meta för annonskonverteringar med bara några få enkla steg. |
| Nytt snabbstartarbetsflöde för Mobile SDK (beta) | Kom åt nya snabbstartarbetsflöden via&quot;Komma igång&quot; från startskärmen för datainsamling! The [snabbstartarbetsflöde för Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) gör att du snabbt kan implementera Mobile SDK och validera grundläggande mobilhändelser i några enkla steg. |
| [!DNL Braze] tillägg för händelsevidarebefordran | The [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) tillägg för händelsevidarebefordran gör att du kan utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med [!DNL Braze] API:er för användarspårning. |
| [!DNL Epsilon] tillägg för händelsevidarebefordran | The [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) kan du utnyttja händelsevidarebefordran för att samla in händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Epsilon] med [!DNL Epsilon] Händelse-API. |
| [!DNL Mixpanel] tillägg för händelsevidarebefordran | The [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Med hjälp av tillägget kan kunder utnyttja händelsevidarebefordran för att hämta händelseinformation i Adobe Experience Platform Edge Network och skicka den till Mixpanel med API:t för spårningshändelser. |

{style="table-layout:auto"}

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgång till filtrering av Adobe Analytics-data | Ni kan nu använda funktionerna för dataförberedelser för att tillämpa regler och villkor för att filtrera era era analysdata innan ni hämtar dem till kundprofilen i realtid. Mer information finns i guiden [filtrera analysdata för profilinmatning](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nya funktioner för kodning och avkodning av URL-strängar | <ul><li>The `get_url_encoded` funktionen tar en URL som indata och ersätter eller kodar specialtecken med ASCII-tecken.</li><li>The `get_url_decoded` funktionen tar en URL som indata och avkodar ASCII-tecken till specialtecken.</li></ul> Mer information finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md). En omfattande lista över reserverade tecken och motsvarande kodade tecken finns i guiden [specialtecken](../../data-prep/functions.md#special-characters). |

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] anslutning GA](../../destinations/catalog/personalization/adobe-commerce.md) | The [!DNL Adobe Commerce] målanslutning (nu allmänt tillgänglig) låter dig välja en eller flera Real-Time CDP-målgrupper att aktivera för [!DNL Adobe Commerce] för att leverera en dynamisk personaliserad upplevelse till era kunder. |
| [[!DNL Snap Inc] anslutning GA](../../destinations/catalog/advertising/snap-inc.md) | The [!DNL Snap Inc] destinationsanslutning (nu allmänt tillgänglig) tillåter marknadsförare att importera användarsegment som skapats i Experience Platform till [!DNL Snapchat Ads] och använda dem för att rikta in sina annonser. |
| [(API) Oraclena Eloqua-anslutning](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Använd den API-baserade anslutningen för att [!DNL Oracle Eloqua] att planera och genomföra kampanjer samtidigt som ni levererar en personaliserad kundupplevelse för sina presumtiva kunder i [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] anslutning](../../destinations/catalog/advertising/amazon-ads.md) | The [!DNL Amazon Ads] integrering med Adobe Experience Platform ger nyckelfärdig integrering med [!DNL Amazon Ads] produkter, inklusive [!DNL Amazon DSP (ADSP)]. Använda [!DNL Amazon Ads] i Adobe Experience Platform kan man definiera målgrupper för annonser för målinriktning och aktivering på [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] anslutning](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (tidigare Bizible) ger marknadsförarna insikt i vilka marknadsföringssatsningar som är mest effektiva när det gäller att öka intäkterna och maximera avkastningen på investeringen för deras företag. Målet möjliggör dataflöden från företag till företag (B2B) från Adobe Experience Platform till [!DNL Marketo Measure]. Kortet är bara tillgängligt för [!DNL Marketo Measure Ultimate] kunder. |
| [TikTok-anslutning](../../destinations/catalog/social/tiktok.md) | Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. |
| [Zendesk-anslutning](../../destinations/catalog/crm/zendesk.md) | Använd det här målet för att skapa och uppdatera identiteter inom ett segment som kontakter inom [!DNL Zendesk]. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Ny åtkomstkontrollbehörighet för mål: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | Den nya behörigheten ger användarna möjlighet att aktivera segment för befintliga destinationer, utan att visa [mappningssteg](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Användare kan lägga till och ta bort segment i aktiveringsarbetsflöden, men kan inte lägga till eller ta bort mappade attribut eller identiteter. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

Vi släpper en felkorrigering för PGP/GPG-kryptering i filbaserade mål för CDP i realtid. Den här ändringen innebär att befintliga filbaserade mål som använder kryptering genererar ett filnamn med ett annat filtillägg än tidigare.

- Aktuellt tillägg när kryptering används: `filename.csv`
- Framtida tillägg när kryptering används: `filename.csv.gpg`

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| CSV till schemarapport | Du kan nu överföra dina lokala filer för att skapa scheman som genereras av maskininlärning och som eliminerar behovet av att skapa ett schema manuellt. Från [!UICONTROL Sources] arbetsyta, ladda upp en CSV-exempelfil och Adobe maskininlärningsalgoritmer föreslår ett schema åt dig baserat på målfälten. Se [dokumentation](../../ingestion/tutorials/map-csv/recommendations.md) för mer information.&quot; |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL Offer Item]](https://github.com/adobe/xdm/pull/1678/files) | En klass som representerar ett erbjudande. |
| Klass | [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1678/files) | En artikel som kan bli föremål för beslut. Resultatet av en beslutsprocess är en eller flera beslutsposter. |
| Klass | [[!UICONTROL Media Session Server Timeout]](https://github.com/adobe/xdm/pull/1676/files) | Detta anger hur lång tid (i sekunder) som har gått mellan användarens senaste kända interaktion och tidpunkten då sessionen stängdes. |
| Fältgrupp | [[!UICONTROL XDM Profile Computed Attributes]](https://github.com/adobe/xdm/pull/1686/files) | Detta lägger till beräknade attribut från interna Adobe-tjänster till inkommande kunddata. Detta bör inte användas av kunder för att importera data. |
| Datatyper | [[!UICONTROL Refund Item]](https://github.com/adobe/xdm/pull/1685/files) | Anger om en återbetalning är kopplad till en order och definierar typ av återbetalning, belopp och associerad valuta. |
| Datatyper | [[!UICONTROL Category data]](https://github.com/adobe/xdm/pull/1677/files) | Den här nya datatypen representerar kategorin för en produkt. |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1682/files) | Ett nytt XDM-schema skapades för målklassificeringsdatamängder. Det innehåller en uppsättning metadatafält som klassificerar Target-aktiviteter och -upplevelser. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL Content Component Details]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` togs bort från [!UICONTROL Content Component Details] |
| Fältgrupp | [[!UICONTROL AJO Entity tags]](https://github.com/adobe/xdm/pull/1672/files) | Lagt till AJO-enhetstaggar i [!UICONTROL AJO Entity Fields], som motsvarar en resa eller kampanj |
| Fältgrupp | (Flera) | Flera fält har lagts till för [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/pull/1671/files) |
| Fältgrupp | (Flera) | [Flera XDM-händelsetyper har lagts till för [!UICONTROL Media Reporting]](https://github.com/adobe/xdm/pull/1670/files). |
| Fältgrupp | [!UICONTROL Workfront Change Event] | The `Full Record` och `Accessor Employee Ids` fältgrupper lades till. |
| Datatyper | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/pull/1685/files) | The [!UICONTROL Refund Amount] har lagts till för att ange det belopp som återbetalats för posten, om ett sådant finns. |
| Datatyper | [[!UICONTROL Order ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refunds List] har lagts till i listan över återbetalningar för den här ordern. |
| Datatyper | [[!UICONTROL Product List Item ]](https://github.com/adobe/xdm/pull/1677/files) | Produktkategorierna har lagts till i listan över kategoridata för den här produkten. |
| Datatyp | [!UICONTROL Session details information] | Lagt till `pev3` strängfält som [anger vilken typ av medieström som används för rapportering](https://github.com/adobe/xdm/pull/1676/files). Dessutom lades `pccr` anger om en omdirigering har gjorts. |
| Datatyp | [!UICONTROL Requisition List] | Tillhandahåller [egenskaper för rekvisitionslista](https://github.com/adobe/xdm/pull/1675/files). De innehåller namn, ID och beskrivning. |
| Datatyp | [!UICONTROL Commerce] | The [Commerce-datatypen har uppdaterats](https://github.com/adobe/xdm/pull/1675/files) inkludera `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`och `requisitionList`. |

{style="table-layout:auto"}

Mer information om XDM in Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta alla datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att matas in i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Attributbaserad åtkomstkontroll i det accelererade arkivet | Använd attributbaserad åtkomstkontroll med Data Distiller för att definiera åtkomstkontroll för alla datauppsättningar i det accelererade arkivet. Detta styr åtkomsten till anpassade datamodeller som skapats av användare och lagrats på en accelererad butik för att styra anpassade instrumentpaneler. |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Real-Time Customer Data Platform B2B-utgåva {#b2b}

Real-Time CDP B2B Edition bygger på Real-time Customer Data Platform (Real-Time CDP) och är särskilt framtagen för marknadsförare som använder en tjänstmodell som bygger på business-to-business. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Bugfix | För att profilerna ska återges mer korrekt i systemet, inkluderar systemet inte längre interna profiler i det totala antalet profiler eller adresserbara målgruppsmått för Real-time Customer Data Platform B2B Edition. Från och med idag kan du se en engångsminskning av det totala antalet profiler/adresserbara målgruppsmått. Inga data har raderats, det här är bara en ändring av antalet. Kontakta din Adobe-chef om du har några frågor |

{style="table-layout:auto"}

Läs mer om Real-Time CDP B2B Edition i [Real-Time CDP B2B Edition - översikt](../../rtcdp/overview.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilmått | För att ni ska få en mer korrekt återgivning av profilmätvärden kombineras uppdelning efter medlemskap och omsättningsstatistik och beräknas nu över en 24-timmarsperiod. Mer information finns i [Användargränssnittsguide för segmentering](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tillgänglighet för betaversion av [!DNL Chatlio] | The [!DNL Chatlio] finns nu i betaversionen. Använd [!DNL Chatlio] strömma [!DNL Chatlio] händelsedata till Experience Platform. Mer information finns i [[!DNL Chatlio] översikt](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Tillgänglighet för betaversion av [!DNL Customer.io] | The [!DNL Customer.io] finns nu i betaversionen. Använd [!DNL Customer.io] för att strömma era kundhändelsedata till Experience Platform. Mer information finns i [[!DNL Customer.io] översikt](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Tillgänglighet för betaversion av [!DNL Pendo] | The [!DNL Pendo] finns nu i betaversionen. Använd [!DNL Pendo] för att strömma era produktanalysdata till Experience Platform. Mer information finns i [[!DNL Pendo] översikt](../../sources/connectors/analytics/pendo-webhook.md). |
| Stöd för dataflöden | Du kan nu använda API:t för Flow Service för att ställa in dataflödena till ett utkasttillstånd. Ritade dataflöden kan senare uppdateras och publiceras med ny information. Mer information finns i guiden [ange källans dataflöden som utkast](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
