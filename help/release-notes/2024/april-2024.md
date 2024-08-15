---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformationen för Adobe Experience Platform från april 2024.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 14dccb993b38ca352c6de3ed851bafe7c44ca631
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 april 2024**

>[!TIP]
>
>Använd [Adobe Experience Platform-ordlistan](/help/landing/glossary.md) för att bekanta dig med terminologi som används i Real-time Customer Data Platform och Adobe Experience Platform. Om du inte kan hitta en viss term som du söker efter kan du använda alternativen för feedback på sidan och begära att nya termer läggs till i ordlistan.

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

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Real-time Customer Data Platform B2B-insikter | Utforska förkonfigurerade [Real-Time CDP B2B-datainsikter om konton och möjligheter](../../dashboards/insights/account-profiles.md) som hjälper dig att förstå dina data och informera om dina affärsbeslut. Du kan även [skapa egna insikter med Real-Time CDP B2B-datamodell](../../dashboards/data-models/cdp-insights-data-model-b2c.md) för att visualisera och utforska dina data och spara anpassade visualiseringar på din instrumentpanel. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | [!DNL Acxiom Anonymous Visitor Insights] taggtillägg | Identifiera varifrån besökarna på din webbplats kommer med [!DNL Acxiom's Visitor Insights]. Genom att använda geoIP-sökningsteknik kan Acxiom identifiera var anonyma webbläsare finns. När sökningen i den organiserade databasen har identifierats får den ytterligare information som skickas tillbaka till webbläsaren. Innehållsskapare kan skräddarsy sitt innehåll så att det matchar dessa datapunkter och ger besökarna en mer personaliserad och engagerande upplevelse, även om de började som främlingar. |
| Dataströmmar | [Identifiering av robot i Edge Network](../../datastreams/bot-detection.md) | Trafik som härrör från icke-mänskliga enheter, som automatiserade program, webbskrapor, spindlar, skriptskannrar, kan göra det svårare att identifiera händelser som inträffar från mänskliga besökare. Den här typen av trafik kan påverka viktiga affärsvärden negativt, vilket leder till felaktig trafikrapportering. <br>Med punktidentifiering kan du identifiera händelser som har genererats av [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) och [[!DNL Server API]](../../server-api/overview.md) som om de har genererats av kända spindlar och bottar. Genom att konfigurera robotidentifiering för dina datastreams kan du identifiera specifika IP-adresser, IP-intervall och begäranrubriker som du vill klassificera som båda händelser. Identifiering av <br>-robottrafik kan ge dig en mer exakt mätning av användaraktivitet på din webbplats eller i ditt mobilprogram. |
| Mobil-SDK | Huvudversion | Nya större versioner av Mobile SDK har släppts för följande plattformar: iOS Mobile Core 5.x och kompatibla iOS-tillägg, Android Mobile Core 3.x och kompatibla Android-tillägg, React Native Core 6.x och kompatibla React Native-tillägg, Flutter Core 4.x och kompatibla Flutter-tillägg. Den här versionen innehåller flera nya funktioner och förbättringar, bland annat stöd för Android SDK för Jetpack Compose, stöd för Adobe Journey Optimizer kodbaserade upplevelser och allmän tillgänglighet för Adobe Journey Optimizer Messaging-tillägget för Flutter. Mer information finns i [Versionsinformation för Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobil-SDK | Sekretess | På grund av Apple policyuppdatering, som börjar 1 maj 2024, måste utvecklare implementera nya sekretessfunktioner för att kunna skicka in till App Store. Alla Adobe-kunder som använder Mobile SDK måste uppgradera till version 5.x av SDK om de vill ha App Store-godkännande efter 1 maj. |
| Roku SDK | Roku SDK | Den första större versionen av Roku SDK har släppts med stöd för Streaming Media för Platform Edge Network. |
| Taggar och händelsevidarebefordran | Produktvägledning | Experience Platform [Taggar](../../tags/home.md) och [Vidarebefordra händelser](../../tags/ui/event-forwarding/overview.md) erbjuder en ny rad upplevelser som hjälper dig att komma igång snabbt och få en snabb tid att värdera. De här upplevelserna omfattar nya startskärmar, självstudiekurser i produkten och verktygstips. <br>![Händelsevidarebefordran med produktvägledning markerad.](../2024/assets/april/event-forwarding.png "Schemaredigeraren med fälten för typ och mappningsvärdetyp markerade."){width="100" zoomable="yes"}<br> |
| Webb-SDK | Förenklad användning av Web SDK för Audience Manager-kunder | Flera Web SDK-uppdateringar förenklar nu användningen av Web SDK utan att använda Experience Data Model (XDM) för Experience Cloud-lösningar, till exempel Audience Manager, Analytics och Target. Läs mer om användning av Audience Manager Web SDK i följande handböcker: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Uppdatera datainsamlingsbiblioteket för Audience Manager från Audience Manager-taggtillägget till Web SDK-taggtillägget</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Uppdatera ditt datainsamlingsbibliotek för Audience Manager från AppMeasurement JavaScript-biblioteket till Web SDK JavaScript-biblioteket</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Läs [datainsamlingsöversikten](../../collection/home.md) om du vill veta mer om datainsamlingar.

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Parametern `isRequired` är nu tillgänglig för kapslade kunddatafält i Destinationen SDK | När du konfigurerar ett mål i Destinationen SDK kan du nu [ställa in kapslade kunddatafält efter behov](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). På så sätt kan användare som ställer in målet inte fortsätta med sitt aktiveringsflöde förrän de väljer ett värde för det fältet. |
| Edge-segmentering är inte längre något obligatoriskt krav när du ställer in ett Adobe Target-mål med Web SDK | Tidigare var dataströmmen aktiverad för personalisering och kantsegmentering när ett [Adobe Target-mål](/help/destinations/catalog/personalization/adobe-target-connection.md) konfigurerades med Web SDK. Kravet på att datastream ska aktiveras för kantsegmentering [ har nu tagits bort](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Observera att det här integreringsmönstret bara gör att du kan dra nytta av en delmängd av användningsexempel för personalisering när du använder Adobe Target med Real-Time CDP. Läs mer om [användningsfall som aktiveras av integreringstypen](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Ta bort flera målgrupper och datauppsättningar från aktiveringsflöden | Nu kan du markera och ta bort flera målgrupper och datauppsättningar från målaktiveringsflöden. Mer information finns i dokumentationen för [målinformation](../../destinations/ui/destination-details-page.md#bulk-remove) och [datauppsättningsexport](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Använd Adobe Experience Platform identitetstjänst för att skapa en heltäckande bild av era kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av `/orgs/{ORG}/`-slutpunkterna i API | Följande slutpunkter i [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) har tagits bort:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> Du kan använda slutpunkterna `/idnamespace/identities` och `/idnamespace/identities/{ID}` för att utföra samma uppgifter och hämta antingen alla namnutrymmen i en organisation eller ett specifikt namnutrymme i en organisation. |

{style="table-layout:auto"}

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Övervakning {#monitoring}

Använd kontrollpanelen i användargränssnittet i Experience Platform för att övervaka hur dina data överförs från Sources, Identity Service, Real-Time Customer Profile, Audiences och Destinations.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Övervaka utökning av instrumentpanelen | Du kan nu använda kontrollpanelen för övervakning för olika datatyper baserat på ditt affärsexempel. Använd kontrollpanelen för att övervaka datatypsaktiviteter för personer, konton och potentiella kunder i källor, målgrupper och destinationer. |

{style="table-layout:auto"}

Mer information finns i guiden om [med kontrollpanelen](../../dataflows/ui/monitor.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta till alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datamängd som kan användas för rapportering, Data Science Workspace eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Frågekarantän | Isolera automatiskt misslyckade frågekörningar för att förhindra avbrott och upprätthålla konsekventa prestanda. Mer information finns i dokumentationen för [frågekarantän](../../query-service/ui/query-schedules.md#quarantine). |
| Avbryt fråga | Ta kontroll över frågekörningen och förbättra produktiviteten genom att avbryta frågor som körs länge.Mer information finns i dokumentationen för [Avbryt fråga](../../query-service/ui/user-guide.md#cancel-query). |
| Schemalagda frågemeddelanden | Håll dig informerad med proaktiva meddelanden när du schemalägger frågor, vilket säkerställer effektiv och snabb uppgiftshantering. Du kan [prenumerera på aviseringar antingen när du skapar en fråga](../../query-service/ui/query-schedules.md#alerts-for-query-status) eller när du använder infogade åtgärder för befintliga schemalagda frågor. Mer information finns i dokumentationen för [prenumerera på aviseringar med textbundna åtgärder](../../query-service/ui/monitor-queries.md#alert-subscription). |
| Förbättrad navigering i schemalagda frågor | Navigera enkelt mellan frågemallar och schemalagda körningar för ökad produktivitet. Mer information finns i dokumentationen för [att visa schemalagda frågor ](../../query-service/ui/query-schedules.md#scheduled-query-runs). |
| Utdata för utökad fråga | Få tillgång till upp till 500 rader frågeresultat i konsolen för mer detaljerad analys av dina data. Mer information finns i dokumentationen för [resultatantal](../../query-service/ui/user-guide.md#result-count). |
| Äldre frågeredigerare - solnedgång | Från och med den 30 april 2024 har den förbättrade frågeredigeraren blivit standardredigerare för alla användare. Den äldre redigeraren kommer att bli inaktuell den 24 maj-2024 och inte längre vara tillgänglig för användning. Mer information finns i användarhandboken för [Frågeredigeraren](../../query-service/ui/user-guide.md). |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Verktyg i sandlådan](../../sandboxes/ui/sandbox-tooling.md) | Använd sandlådeverktyg för att [exportera](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) alla objekttyper som stöds till ett fullständigt sandlådepaket och [importera](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) paketet mellan olika sandlådor för att replikera objektkonfigurationer. |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Målgruppsstadier | Målgruppslivscykeln har strömlinjeformats för att förenkla livscykelhanteringen. Läs [Vanliga frågor om segmenteringstjänsten](../../segmentation/faq.md#lifecycle-states) om du vill veta mer om dessa livscykeltillstånd. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

Använd källor i Experience Platform för att importera data från ett Adobe-program eller en datakälla från tredje part.

**Nya källor**

| Nya källor | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Använd [[!DNL PathFactory] source](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) för att integrera dina besökar-, sessions- och sidvisningsdata från [!DNL PathFactory] till Experience Platform. Läs [[!DNL PathFactory] översikten](../../sources/connectors/marketing-automation/pathfactory.md) om du vill ha mer information om hur du kommer igång. |
| [!DNL Teradata Vantage] | Använd [[!DNL Teradata Vantage] källa](../../sources/tutorials/ui/create/databases/teradata-vantage.md) för att importera data från hybridmiljöer med flera moln till Experience Platform. Läs [[!DNL Teradata Vantage] översikten](../../sources/connectors/databases/teradata-vantage.md) om du vill ha mer information om hur du kommer igång. |

{style="table-layout:auto"}

**Nya och uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av IP-adresser som gör att de kan listas i VA7 | Följande IP-adresser har lagts till i listan över IP-adresser som ska läggas till i din tillåtelselista för VA7 (Nordamerika): <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> En omfattande lista över IP-adresser som ska läggas till i tillåtelselista finns i dokumentet [IP Address tillåtelselista](../../sources/ip-address-allow-list.md). |
| Stöd för nya autentiseringstyper med källan [!DNL Azure Event Hubs] | Du kan nu ansluta din [!DNL Event Hubs]-källa till Experience Platform med antingen [!DNL Azure Active Directory Authentication] eller [!DNL Scoped Azure Active Directory Authentication]. Läs guiden om [att ansluta [!DNL Event Hubs] till Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) om du vill ha mer information. |
| Uppdateringar av [!DNL Data Landing Zone]-hämtning av autentiseringsuppgifter | Du kan nu använda rätt spår i källarbetsytan för att hämta dina [!DNL Data Landing Zone]-autentiseringsuppgifter. Nu kan du även använda rätt spår för att uppdatera dina inloggningsuppgifter. Mer information finns i [[!DNL Data Landing Zone] gränssnittshandboken](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Mer information om källor finns i [Källöversikt](../../sources/home.md).
