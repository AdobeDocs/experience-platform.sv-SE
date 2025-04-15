---
title: Versionsinformation om Adobe Experience Platform april 2024
description: Versionsinformationen för Adobe Experience Platform från april 2024.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1895'
ht-degree: 100%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 30 april 2024**

>[!TIP]
>
>Använd [ordlistan för Adobe Experience Platform](/help/landing/glossary.md) för att bekanta dig med terminologin som används i plattformen för kunddata i realtid och Adobe Experience Platform. Om du inte hittar en viss term som du letar efter kan du lämna återkoppling på sidan för att begära att nya termer läggs till i ordlistan.

Uppdateringar av befintliga funktioner i Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Identitetstjänst](#identity-service)
- [Övervakning](#monitoring)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Plattform för kunddata i realtid-insikter | Utforska förkonfigurerade [Real-Time CDP B2B-datainsikter om konton och möjligheter](../../dashboards/insights/account-profiles.md) som hjälper dig att förstå dina data och informera kring dina affärsbeslut. Du kan även [skapa egna insikter med Real-Time CDP B2B-datamodell](../../dashboards/data-models/cdp-insights-data-model-b2c.md) för att visualisera och utforska dina data och spara anpassade visualiseringar på din kontrollpanel. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en rad olika tekniker som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | [!DNL Acxiom Anonymous Visitor Insights] Taggtillägg | Identifiera varifrån besökarna på din webbplats kommer med [!DNL Acxiom's Visitor Insights]. Genom att använda geoIP-sökteknik kan Acxiom identifiera var anonyma webbläsare finns. När de väl har identifierats ger en sökning i deras organiserade databas ytterligare insikter som skickas tillbaka till webbläsaren. Innehållsskapare kan skräddarsy sitt innehåll så att det matchar dessa datapunkter och ger besökarna en mer personlig och engagerande upplevelse, även om de började som främlingar. |
| Dataströmmar | [Identifiering av bot i Edge Network](../../datastreams/bot-detection.md) | Trafik som härrör från icke-mänskliga enheter, som automatiserade program, webbskrapning, spindlar och skriptskannrar kan göra det svårare att identifiera händelser som inträffar från mänskliga besökare. Den här typen av trafik kan påverka viktiga affärsvärden negativt, vilket leder till felaktig rapportering av trafik. <br>Med botdetektering kan du identifiera händelser som har genererats av [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) och [[!DNL Server API]](../../server-api/overview.md) som har genererats av kända spindlar och botar. Genom att konfigurera botdetektering för dina dataströmmar kan du identifiera specifika IP-adresser, IP-intervall och begäranrubriker som du vill klassificera som bothändelser. <br> Identifiering av bottrafik kan ge dig en mer exakt mätning av användaraktivitet på din webbplats eller i din mobilapp. |
| Mobile SDK | Release av huvudversion | Nya större versioner av Mobile SDK har släppts för följande plattformar: iOS Mobile Core 5.x och kompatibla iOS-tillägg, Android Mobile Core 3.x och kompatibla Android-tillägg, React Native Core 6.x och kompatibla React Native-tillägg, Flutter Core 4.x och kompatibla Flutter-tillägg. Den här versionen innehåller flera nya funktioner och förbättringar, bland annat stöd för Android SDK för Jetpack Compose, stöd för kodbaserade upplevelser med Adobe Journey Optimizer och allmän åtkomst till tillägget Adobe Journey Optimizer Messaging för Flutter. Mer information finns i [Versionsinformation för Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes). |
| Mobile SDK | Sekretess | På grund av Apples policyuppdatering, som gäller från 1 maj 2024, måste utvecklare implementera nya sekretessfunktioner för att kunna skicka in till App Store. Alla Adobe-kunder som använder Mobile SDK måste uppgradera till version 5.x av SDK:et om de vill få godkännande på App Store efter 1 maj. |
| Roku SDK | Roku SDK | Den första större versionen av Roku SDK har släppts med stöd för strömmande media för Experience-plattformen Edge Network. |
| Taggar och vidarebefordran av händelser | Vägledning i produkten | [Taggar](../../tags/home.md) och [Vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md) i Experinece Platform erbjuder nya upplevelser som hjälper dig att snabbt komma igång snabbt och uppnå värde. De här upplevelserna omfattar nya registreringsskärmar, självstudiekurser i produkten och verktygstips. <br>![Vidarebefordran av händelser med vägledning i produkten markerad.](../2024/assets/april/event-forwarding.png "Schemaredigeraren med fälten Typ och Mappning markerade."){width="100" zoomable="yes"}<br> |
| Web SDK | Förenklad användning av Web SDK för Audience Manager-kunder | Flera Web SDK-uppdateringar förenklar nu användningen av Web SDK utan att använda Experience Data Model (XDM) för Experience Cloud-lösningar, till exempel Audience Manager, Analytics och Target. Läs mer om användning av Audience Manager Web SDK i följande guider: <ul><li><a href="https://experienceleague.adobe.com/sv/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Uppdatera datainsamlingsbiblioteket för Audience Manager från taggtillägget för Audience Manager till taggtillägget för Web SDK</li><li><a href="https://experienceleague.adobe.com/sv/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Uppdatera ditt datainsamlingsbibliotek för Audience Manager från JavaScript-biblioteket AppMeasurement till JavaScript-biblioteket för Web SDK</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Läs mer på [översikten över datainsamling](../../collection/home.md).

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Parametern `isRequired` är nu tillgänglig för kapslade kunddatafält i Destination SDK | När du konfigurerar en destination i Destination SDK kan du nu [ställa in kapslade kunddatafält efter behov](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). På så sätt kan användare som ställer in destinationen inte fortsätta med sitt aktiveringsflöde förrän de väljer ett värde för det fältet. |
| Edge-segmentering är inte längre något obligatoriskt krav när du ställer in en Adobe Target-destination med Web SDK | Tidigare var dataströmmen aktiverad för personalisering och Edge-segmentering när en [Adobe Target-destination](/help/destinations/catalog/personalization/adobe-target-connection.md) konfigurerades med Web SDK. Kravet på att dataströmmen ska aktiveras för Edge-segmentering [har nu tagits bort](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Observera att det här integreringsmönstret bara gör att du kan dra nytta av en deluppsättning av användningsexemplen för personalisering när du använder Adobe Target med Real-Time CDP. Läs mer om [aktiverade användningsfall efter integreringstyp](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Ta bort flera målgrupper och datauppsättningar från aktiveringsflöden | Nu kan du markera och ta bort flera målgrupper och datauppsättningar från destinationsaktiveringsflöden. Mer information finns i dokumentationen för [destinationsinformation](../../destinations/ui/destination-details-page.md#bulk-remove) och [export av datauppsättningar](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [översikten över destinationer](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Använd identitetstjänsten för Adobe Experience Platform för att skapa en heltäckande bild av dina kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av slutpunkterna `/orgs/{ORG}/` i API:et | Följande slutpunkter i [[!DNL Identity Service] API:et](https://developer.adobe.com/experience-platform-apis/references/identity-service/) har tagits bort:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Du kan använda slutpunkterna `/idnamespace/identities` och `/idnamespace/identities/{ID}` för att utföra samma uppgifter och hämta antingen alla namnrymderna i en organisation eller en specifik namnrymd i en organisation. |

{style="table-layout:auto"}

Mer information om identitetstjänsten finns i [översikten över identitetstjänsten](../../identity-service/home.md).

## Övervakning {#monitoring}

Använd kontrollpanelen i gränssnittet för Experience Platform för att övervaka resan för dina data från källor, identitetstjänst, plattformen för kundprofil i realtid, målgrupper och mål.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Utbyggnad av kontrollpaneler för övervakning | Du kan nu använda kontrollpanelen för övervakning för olika datatyper baserat på din verksamhets användningsområde. Använd kontrollpanelen för övervakning för att övervaka aktiviteter för datatyperna person, konto och prospekt i källor, målgrupper och mål. |

{style="table-layout:auto"}

Mer information finns i guiden om att [använda kontrollpanelen för övervakning](../../dataflows/ui/monitor.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Frågekarantän | Isolera automatiskt misslyckade frågekörningar för att förhindra störningar och upprätthålla konsekvent prestanda. Mer information finns i dokumentationen [frågekarantän](../../query-service/ui/query-schedules.md#quarantine). |
| Avbryt fråga | Ta kontroll över frågekörningen och förbättra produktiviteten genom att avbryta frågor som körs länge. Mer information finns i dokumentationen för [Avbryt fråga](../../query-service/ui/user-guide.md#cancel-query). |
| Schemalagda frågemeddelanden | Håll dig informerad med proaktiva meddelanden när du schemalägger frågor, vilket säkerställer effektiv och snabb uppgiftshantering. Du kan [prenumerera på aviseringar antingen när du skapar en fråga](../../query-service/ui/query-schedules.md#alerts-for-query-status) eller genom att använda inline-åtgärderna för befintliga schemalagda frågor. Se dokumentationen [prenumerera på varningar med inline-åtgärder](../../query-service/ui/monitor-queries.md#alert-subscription) för mer information. |
| Förbättrad navigering i schemalagda frågor | Navigera enkelt mellan frågemallar och schemalagda körningar för ökad produktivitet. Mer information finns i dokumentationen om [Visa schemalagda frågekörningar](../../query-service/ui/query-schedules.md#scheduled-query-runs). |
| Utökad output av frågor | Få tillgång till upp till 500 rader med resultat på frågor i konsolen för djupare analys av dina data. Se dokumentationen [resultatantal](../../query-service/ui/user-guide.md#result-count) för mer information. |
| Äldre frågeredigeraren upphör | Från och med den 30 april 2024 är den förbättrade frågeredigeraren standardredigeraren för alla användare. Den äldre redigeraren kommer att tas bort den 24 maj 2024 och inte längre vara tillgänglig för användning. Mer information finns i användarhandboken för [frågeredigeraren](../../query-service/ui/user-guide.md). |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [översikten över frågetjänster](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Verktyg i sandlådan](../../sandboxes/ui/sandbox-tooling.md) | Använd sandlådeverktyg för att [exportera](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) alla objekttyper som stöds till ett fullständigt sandlådepaket och sedan [importera](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) paketet till olika sandlådor för att replikera objektkonfigurationer. |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Experience Platform] och är tillgängliga för alla Adobe-lösningar.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Livscykelstadier för målgruppen | Målgruppens livscykel har strömlinjeformats för att förenkla hanteringen av livscykeln. Läs [Vanliga frågor om segmenteringstjänsten](../../segmentation/faq.md#lifecycle-states) om du vill veta mer om dessa livscykeltillstånd. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Nya källor**

| Nya källor | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Använd [[!DNL PathFactory] -källan](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) för att integrera dina besökar-, sessions- och sidvisningsdata från [!DNL PathFactory] till Experience Platform. Läs [[!DNL PathFactory] översikten](../../sources/connectors/marketing-automation/pathfactory.md) om du vill ha mer information om hur du kommer igång. |
| [!DNL Teradata Vantage] | Använd [[!DNL Teradata Vantage] -källan](../../sources/tutorials/ui/create/databases/teradata-vantage.md) för att importera data från hybridmiljöer med flera moln till Experience Platform. Läs [[!DNL Teradata Vantage] översikten](../../sources/connectors/databases/teradata-vantage.md) om du vill ha mer information om hur du kommer igång. |

{style="table-layout:auto"}

**Nya och uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av IP-adresser som gör att de kan listas i VA7 | Följande IP-adresser har lagts till i listan över IP-adresser som ska läggas till i din tillåtelselista för VA7 (Nordamerika): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> En omfattande lista över IP-adresser som ska läggas till i tillåtelselista finns i dokumentet [tillåtelselistan för IP Adress](../../sources/ip-address-allow-list.md). |
| Stöd för nya autentiseringstyper med källan [!DNL Azure Event Hubs] | Du kan nu ansluta din [!DNL Event Hubs]-källa till Experience Platform med antingen [!DNL Azure Active Directory Authentication] eller [!DNL Scoped Azure Active Directory Authentication]. Läs guiden om [att ansluta [!DNL Event Hubs] till Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) om du vill ha mer information. |
| Uppdateringar för hämtning av [!DNL Data Landing Zone]-autentiseringsuppgifter | Du kan nu använda rätt spår i källarbetsytan för att hämta dina [!DNL Data Landing Zone]-autentiseringsuppgifter. Nu kan du även använda rätt spår för att uppdatera dina inloggningsuppgifter. Mer information finns i [[!DNL Data Landing Zone] guiden för gränssnitt](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Mer information om källor finns i [källöversikten](../../sources/home.md).
