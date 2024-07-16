---
title: Adobe Experience Platform Release Notes januari 2023
description: Versionsinformationen för Adobe Experience Platform i januari 2023.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: d23f1cc9dd0155aceae78bf938d35463e9c38181
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 januari 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Säkerhet](#assurance)
- [Datainsamling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Artificiell intelligens/maskininlärning {#ai-ml}

Artificiell intelligens och maskininlärningstjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja kraften i AI/ML i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prognoser, utan behov av datavetenskap, som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| HIPAA-beredskap | Vårdsköldens kunder kan nu ta emot, använda, underhålla eller överföra skyddad hälsoinformation i Attribution AI och vissa andra Experience Platform-baserade tillämpningar. Sjukvården är avsedd för vårdkunder som antingen är en enhet som omfattas av avtalet eller en affärsassociation enligt HIPAA. Mer information finns i dokumentationen om [HIPAA och Adobe Products and Services](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Redigera kolumner för extra poängdatauppsättning | Nu kan du lägga till eller ta bort ytterligare spaltdatakolumner (rapportkolumner) när du redigerar befintliga modeller. Detta utökar flexibiliteten i attribueringspoängen för att ge dig insikter om ytterligare dimensioner efter att en modell redan har skapats. Mer information finns i [Användargränssnittsguiden för attribut](../../intelligent-services/attribution-ai/user-guide.md). |

{style="table-layout:auto"}

Mer information finns i översikten för [AI/ML-tjänster](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI

Kundens AI för Real-time Customer Data Platform används för att generera anpassade benägenhetspoäng som bortfall och konvertering för enskilda profiler i stor skala. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbilda eller distribuera.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| HIPAA-beredskap | Vårdsköldens kunder kan nu ta emot, använda, underhålla eller överföra skyddad hälsoinformation i Customer AI för Real-time Customer Data Platform och vissa andra Experience Platform-baserade tillämpningar. Sjukvården är avsedd för vårdkunder som antingen är en enhet som omfattas av avtalet eller en affärsassociation enligt HIPAA. Mer information finns i dokumentationen om [HIPAA och Adobe Products and Services](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Mer information finns i översikten för [AI/ML-tjänster](../../intelligent-services/customer-ai/overview.md).

## Säkerhet {#assurance}

Med Adobe Assurance kan ni inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Valideringsredigerare | Nya förbättringar av valideringsredigeraren har lagts till. Dessa förbättringar omfattar valideringskolumner, nya kodbyggningsverktyg och förbättrade vyer. |

{style="table-layout:auto"}

Mer information om Assurance finns i [Assurance-dokumentationen](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny hemskärm | Startsidan för användargränssnittet för datainsamling har uppdaterats med information om introduktion och länkar som effektiviserar produktiviteten. Detta omfattar följande:<ol><li>Dokumentation och rekommenderade arbetsflöden för att komma igång</li><li>Senaste egenskaper, regler och dataelement</li><li>Populära tillägg</li><li>Nya tilläggsuppdateringar med en snabbinstallationsfunktion</li></ol> |
| Skicka data till [!DNL Google Ads] med händelsevidarebefordran | Du kan nu använda [[!DNL Google Ads Enhanced Conversions] API-tillägget](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) för vidarebefordran av händelser i kombination med [Google Oauth 2-hemligheter](../../tags/ui/event-forwarding/secrets.md#google-oauth2) för att skicka data på serversidan säkert till [!DNL Google Ads] i realtid. |

{style="table-layout:auto"}

## Destinationer (uppdaterad 2 februari) {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud-publikanslutning](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Använd anslutningen [!UICONTROL (Beta) Adobe Experience Cloud Audiences] för att dela segment från Experience Platform till olika Experience Platform-lösningar, som Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target eller Marketo. |
| [Pega-profilanslutning](../../destinations/catalog/personalization/pega-profile.md) | Använd [!DNL Pega Profile Connector] i Adobe Experience Platform för att skapa en utgående liveanslutning till ditt [!DNL Amazon] S3-lagringsutrymme och exportera regelbundet profildata till CSV-filer från Adobe Experience Platform till dina egna S3-bucket. I [!DNL Pega Customer Decision Hub] kan du schemalägga datajobb för import av profildata från S3-lagring för att uppdatera profilen [!DNL Pega Customer Decision Hub]. |
| [(Beta) Trade Desk CRM-anslutningen ](../../destinations/catalog/advertising/tradedesk-emails.md) | I och med lanseringen av EUID (European Unified ID) ser du nu två [!DNL The Trade Desk - CRM] mål i [målkatalogen](/help/destinations/catalog/overview.md). <ul><li> Använd målet **[!DNL The Trade Desk - CRM (EU)]** om du hämtar data i EU.</li><li> Använd målet **[!DNL The Trade Desk - CRM (NAMER & APAC)]** om du hämtar data i APAC- eller NAMER-regionerna. </li></ul> |

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Förbättrad policy för betald mediamarknadsföring för integrering med direktuppspelningsmål | En [förbättring av tvångsprincip](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) på [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations) för användningsfall för betald mediaaktivering. När profiler inte längre är kvalificerade för en samtyckespolicy kommunicerar Experience Platform nu aktivt sin policy till direktuppspelningsdestinationer. <br> <b>Obs!</b>: Den här funktionen är bara tillgänglig för kunder med **[!UICONTROL Privacy and Security Shield]** och för **[!UICONTROL Healthcare Shield]**. |
| Nya avgränsningsalternativ för målanslutningar för betmolnlagring | Tre nya avgränsaralternativ (Kolon `:`, Pipe, Semikolon `;`) är nu tillgängliga för de nya lagringsplatserna för betmolnet - [ (Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ (Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [ (Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud-lagring ](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [ (Beta) SFTP ](/help/destinations/catalog/cloud-storage/sftp.md) . <br> Läs om de [filformateringsalternativ](/help/destinations/ui/batch-destinations-file-formatting-options.md) som stöds för filbaserade mål. |
| Ny valfri parameter som är tillgänglig i [kunddatafält](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) konfigurationer i [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Använd den här parametern när du behöver skapa ett kunddatafält vars värde måste vara unikt för alla måldatafält som har konfigurerats av en användares organisation. <br> Fältet **[!UICONTROL Integration alias]** i målet [[!UICONTROL Custom Personalization]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) måste till exempel vara unikt, vilket innebär att två separata dataflöden till målet inte kan ha samma värde för det här fältet. |

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Korrigera eller förbättra</b></td>
        <td><b>Beskrivning</b></td>
    </tr>
    <tr>
        <td>Uppdaterat exportbeteende till filbaserade mål (PLAT-123316)</td>
        <td>Vi har åtgärdat ett fel i beteendet för <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">obligatoriska attribut</a> vid export av datafiler till gruppmål. <br> Tidigare kontrollerades alla poster i utdatafilerna att innehålla båda: <ol><li>Ett värde som inte är null för kolumnen <code>mandatoryField</code> och</li><li>Ett värde som inte är null i minst ett av de andra icke-obligatoriska fälten.</li></ol> Det andra villkoret har tagits bort. Det kan leda till att fler utdatarader visas i dina exporterade datafiler, vilket visas i exemplet nedan: <br> <b> Exempelbeteende före januari 2023-utgåvan </b> <br> Obligatoriskt fält: <code>emailAddress</code> <br> <b>Indata som ska aktiveras</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>noll</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>noll</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Aktiveringsutdata</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exempelbeteende efter januari 2023-utgåvan </b> <br> <b>Aktiveringsutdata</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>noll</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>noll</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Verifiering av gränssnitt och API för obligatoriska mappningar och dubblettmappningar (PLAT-123316)</td>
        <td>Valideringen tillämpas nu på följande sätt i gränssnittet och API när <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">mappningsfält</a> i arbetsflödet för aktiveringsmål:<ul><li><b>Nödvändiga mappningar</b>: Om målutvecklaren har konfigurerat det med nödvändiga mappningar (till exempel <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a> -målet) måste dessa obligatoriska mappningar läggas till av användaren när data aktiveras till målet. </li><li><b>Duplicerade mappningar</b>: I mappningssteget i aktiveringsarbetsflödet kan du lägga till dubblettvärden i källfälten, men inte i målfälten. I tabellen nedan finns ett exempel på tillåtna och förbjudna mappningskombinationer. <br><table><thead><tr><th>Tillåtet/förbjudet</th><th>Source</th><th>Målfält</th></tr></thead><tbody><tr><td>Tillåtet</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>e-postalias1</li><li>e-post   alias2</li></ul></td></tr><tr><td>Förbjuden</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>e-postalias1</li><li>e-postalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrat visningsnamn för schematräd | Tidigare visades fältnamn i användargränssnittet, men nu är visningsnamnen för schemafält på arbetsytan för schemat mer användarvänliga att läsa. |

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL Conversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | En klass för att spåra konverteringsdata, t.ex. valutakonverteringar. |
| Fältgrupp | [[!UICONTROL Currency Conversion Rate Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | En fältgrupp för klassen [!UICONTROL Conversion] som samlar in ytterligare information om valutakonvertering. |
| Fältgrupp | [[!UICONTROL Consent policies evaluation results map with metadata]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | Fångar information om utvärderingsresultatet av flera olika medgivandeprinciper, inklusive metadatainformation om medgivandeprincipingångar och finns. |

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Datatyp | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Fältet `ID` har bytt namn till `name` och det föregående `name`-fältet är nu `friendlyName`. |
| Datatyp | [[!UICONTROL Decision Proposition Details]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Ett `selectionStrategy`-fält har lagts till som innehåller information om en urvalsstrategi. |
| Fältgrupp | [[!UICONTROL Experience Event - Proposition Interactions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Fältgruppen är nu kompatibel med klassen [!UICONTROL Journey Step Event]. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Fältet `ID` har bytt namn till `name`. |
| Datatyp | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | Återställde en mönsterändring till videosegmentsegenskapen. |
| Datatyp | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Fältet `droppedFrameCount` har tagits bort. |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `isAuthorized`-fältet har bytt namn till `authorized` och dess `type` har uppdaterats till en sträng när det tidigare var ett booleskt värde. |
| Datatyp | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Flera nya fält har lagts till: `shipDate`, `trackingNumber` och `trackingURL`. |
| Fältgrupp | [[!UICONTROL AJO Entity Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Flera nya fält har lagts till: `journeyNodeID`, `journeyNodeName` och `journeyModeType`. |
| Fältgrupp | [[!UICONTROL Consumer Experience Event]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Fältgruppen är nu också kompatibel med klassen [!UICONTROL Summary Metrics]. |
| Fältgrupp | [[!UICONTROL Product Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Fältet `productTriggers` är nu kapslat under ett `weather`-objekt. |
| Fältgrupp | [[!UICONTROL Relative Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Fältet `relativeTriggers` är nu kapslat under ett `weather`-objekt. |
| Fältgrupp | [[!UICONTROL Severe Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Fältet `severeTriggers` är nu kapslat under ett `weather`-objekt. |
| Fältgrupp | [[!UICONTROL Weather Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Fältet `weatherTriggers` är nu kapslat under ett `weather`-objekt. |
| Fältgrupp | [[!UICONTROL XDM Related Business Accounts]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Fältgruppen är nu stabil. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Kommer att tas bort** {#deprecation}

För att ta bort redundans i segmentmedlemskapets livscykel kommer statusen `Existing` att bli inaktuell i [segmentmedlemskartan](../../xdm/field-groups/profile/segmentation.md) i slutet av mars 2023. Ett uppföljningsmeddelande kommer att innehålla det exakta datumet för borttagningen.

Med Post som föråldrad representeras profiler som är kvalificerade i ett segment som `Realized`, och de diskvalificerade profilerna kommer även fortsättningsvis att representeras som `Exited`. Detta skapar paritet med filbaserade mål med `Active`- och `Expired`-segmentstatus.

Den här ändringen kan påverka dig om du använder [företagsmål](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) och har automatiserade processer längre fram i kedjan baserat på statusen `Existing`. Granska dina integreringar längre fram i kedjan om så är fallet för dig. Om du är intresserad av att identifiera nyligen kvalificerade profiler mer än en viss tid kan du använda en kombination av `Realized`-status och `lastQualificationTime` i din segmentmedlemskarta. Mer information får du av Adobe.

Om du vill veta mer om kundprofilen i realtid, inklusive självstudiekurser och bästa praxis för arbete med profildata, börjar du med att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss delmängd av profiler genom att beskriva kriterierna som särskiljer en marknadsföringsbar grupp av personer inom din kundbas. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Import av massvärde i Segment Builder | Segment Builder har nu stöd för import av flera värden, antingen genom att en CSV- eller TSV-fil överförs eller genom att kommaavgränsade värden infogas manuellt. Mer information finns i guiden [Segment Builder](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Utgångsdatum för externt medlemskap | Som standard behålls medlemskap för externa målgrupper i 30 dagar. Om du vill behålla dem längre använder du fältet `validUntil` när målgruppsdata hämtas. |
| Utgångsdatum för plattformsgenererat segmentmedlemskap | Alla segmentmedlemskap som är i läget `Exited` i mer än 30 dagar, baserat på fältet `lastQualificationTime`, kan tas bort. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Tillåt användaråtkomst till undermappar för molnlagringskällor | Nu kan du definiera åtkomst till en viss undermapp i molnlagringskällan när du skapar ett nytt konto. När de har skapats kan användarna bara komma åt data från den tillåtna undermappen. Den här funktionen är tillgänglig för följande molnlagringskällor: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) och [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Beta-tillgänglighet för [!DNL SugarCRM] | [!DNL SugarCRM] källor är nu tillgängliga i betaversionen. Använd källorna [!DNL SugarCRM Accounts & Contacts] och [!DNL SugarCRM Events] för att hämta data från ditt [!DNL SugarCRM]-konto till Experience Platform. Mer information finns i [[!DNL SugarCRM] översikten](../../sources/connectors/crm/sugarcrm.md). |
