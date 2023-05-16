---
title: Adobe Experience Platform Release Notes januari 2023
description: Versionsinformation januari 2023 för Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2340'
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
| Redigera kolumner för extra poängdatauppsättning | Nu kan du lägga till eller ta bort ytterligare spaltdatakolumner (rapportkolumner) när du redigerar befintliga modeller. Detta utökar flexibiliteten i attribueringspoängen för att ge dig insikter om ytterligare dimensioner efter att en modell redan har skapats. Se [Användargränssnittshandbok för attribuering](../../intelligent-services/attribution-ai/user-guide.md) om du vill veta mer. |

{style="table-layout:auto"}

Se [AI-/ML-tjänster](../../intelligent-services/attribution-ai/overview.md) för mer information.

### Kund-AI

Kundens AI för Real-time Customer Data Platform används för att generera anpassade benägenhetspoäng som bortfall och konvertering för enskilda profiler i stor skala. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbilda eller distribuera.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| HIPAA-beredskap | Vårdsköldens kunder kan nu ta emot, använda, underhålla eller överföra skyddad hälsoinformation i Customer AI för Real-time Customer Data Platform och vissa andra Experience Platform-baserade tillämpningar. Sjukvården är avsedd för vårdkunder som antingen är en enhet som omfattas av avtalet eller en affärsassociation enligt HIPAA. Mer information finns i dokumentationen om [HIPAA och Adobe Products and Services](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Se [AI-/ML-tjänster](../../intelligent-services/customer-ai/overview.md) för mer information.

## Säkerhet {#assurance}

Med Adobe Assurance kan ni inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Valideringsredigerare | Nya förbättringar av valideringsredigeraren har lagts till. Dessa förbättringar omfattar valideringskolumner, nya kodbyggningsverktyg och förbättrade vyer. |

{style="table-layout:auto"}

Mer information om Assurance finns i [Assurance-dokumentation](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny hemskärm | Startsidan för användargränssnittet för datainsamling har uppdaterats med information om introduktion och länkar som effektiviserar produktiviteten. Det inkluderar:<ol><li>Dokumentation och rekommenderade arbetsflöden för att komma igång</li><li>Senaste egenskaper, regler och dataelement</li><li>Populära tillägg</li><li>Nya tilläggsuppdateringar med en snabbinstallationsfunktion</li></ol> |
| Skicka data till [!DNL Google Ads] använda händelsevidarebefordran | Nu kan du använda [[!DNL Google Ads Enhanced Conversions] API-tillägg](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) för vidarebefordran av händelser, i kombination med [Google Oauth 2 - hemligheter](../../tags/ui/event-forwarding/secrets.md#google-oauth2)för att på ett säkert sätt skicka data på serversidan till [!DNL Google Ads] i realtid. |

{style="table-layout:auto"}

## Destinationer (uppdaterad 2 februari) {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud Audiences-anslutning](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Använd [!UICONTROL (Beta) Adobe Experience Cloud Audiences] anslutning för att dela segment från Experience Platform till olika Experience Platform-lösningar, som Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target eller Marketo. |
| [Pega-profilanslutning](../../destinations/catalog/personalization/pega-profile.md) | Använd [!DNL Pega Profile Connector] i Adobe Experience Platform för att skapa en utgående liveanslutning till [!DNL Amazon] S3-lagring för att regelbundet exportera profildata till CSV-filer från Adobe Experience Platform till dina egna S3-butiker. I [!DNL Pega Customer Decision Hub]kan du schemalägga datajobb att importera profildata från S3-lagringsutrymmet för att uppdatera [!DNL Pega Customer Decision Hub] profil. |
| [(Beta) The Trade Desk CRM EU connection](../../destinations/catalog/advertising/tradedesk-emails.md) | I och med lanseringen av EUID (European Unified ID) ser du nu två [!DNL The Trade Desk - CRM] destinationer i [målkatalog](/help/destinations/catalog/overview.md). <ul><li> Om du hämtar data i EU ska du använda **[!DNL The Trade Desk - CRM (EU)]** mål.</li><li> Om du hämtar data i APAC- eller NAMER-regionerna använder du **[!DNL The Trade Desk - CRM (NAMER & APAC)]** mål. </li></ul> |

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Förbättrad policy för betald mediamarknadsföring för integrering med direktuppspelningsmål | An [förbättrat genomförande av godkännandepolicyer](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) på [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations) för aktivering av betalmedia. När profiler inte längre är kvalificerade för en samtyckespolicy kommunicerar Experience Platform nu aktivt sin policy till direktuppspelningsdestinationer. <br> <b>Anteckning</b>: Den här funktionen är endast tillgänglig för kunder som har **[!UICONTROL Privacy and Security Shield]** och **[!UICONTROL Healthcare Shield]**. |
| Nya avgränsningsalternativ för målanslutningar för betmolnlagring | Tre nya avgränsningsalternativ (Kolon `:`, rörform, semikolon `;`) finns nu för de nya lagringsplatserna i betmolnet - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure-blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud-lagring](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Läs om vilka funktioner som stöds [filformateringsalternativ](/help/destinations/ui/batch-destinations-file-formatting-options.md) för filbaserade mål. |
| Ny valfri parameter finns i [kunddatafält](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) konfigurationer i [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Använd den här parametern när du behöver skapa ett kunddatafält vars värde måste vara unikt för alla måldataflöden som har konfigurerats av en användares organisation. <br> Till exempel **[!UICONTROL Integration alias]** i [[!UICONTROL Custom Personalization]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) målet måste vara unikt, vilket innebär att två separata dataflöden till det här målet inte kan ha samma värde för det här fältet. |

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Korrigera eller förbättra</b></td>
        <td><b>Beskrivning</b></td>
    </tr>
    <tr>
        <td>Uppdaterat exportbeteende till filbaserade mål (PLAT-123316)</td>
        <td>Vi har åtgärdat ett problem med beteendet hos <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">obligatoriska attribut</a> när datafiler exporteras till gruppmål. <br> Tidigare kontrollerades alla poster i utdatafilerna att innehålla båda: <ol><li>Ett värde som inte är null för <code>mandatoryField</code> kolumn och</li><li>Ett värde som inte är null i minst ett av de andra icke-obligatoriska fälten.</li></ol> Det andra villkoret har tagits bort. Det kan leda till att fler utdatarader visas i dina exporterade datafiler, vilket visas i exemplet nedan:<br> <b> Exempelbeteende före januari 2023-versionen </b> <br> Obligatoriskt fält: <code>emailAddress</code> <br> <b>Indata som ska aktiveras</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Aktiveringsutdata</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exempelbeteende efter januari 2023-versionen </b> <br> <b>Aktiveringsutdata</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Verifiering av gränssnitt och API för obligatoriska mappningar och dubblettmappningar (PLAT-123316)</td>
        <td>Valideringen genomförs nu på följande sätt i gränssnittet och API när <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">mappningsfält</a> i arbetsflödet för aktivering av mål:<ul><li><b>Nödvändiga mappningar</b>: Om målet har konfigurerats av målutvecklaren med obligatoriska mappningar (till exempel <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> måste dessa obligatoriska mappningar läggas till av användaren när data aktiveras till målet. </li><li><b>Duplicera mappningar</b>: I mappningssteget i aktiveringsarbetsflödet kan du lägga till dubblettvärden i källfälten, men inte i målfälten. I tabellen nedan finns ett exempel på tillåtna och förbjudna mappningskombinationer. <br><table><thead><tr><th>Tillåtet/förbjudet</th><th>Källfält</th><th>Målfält</th></tr></thead><tbody><tr><td>Tillåtet</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>e-postalias2</li></ul></td></tr><tr><td>Förbjuden</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

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
| Fältgrupp | [[!UICONTROL Currency Conversion Rate Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | En fältgrupp för [!UICONTROL Conversion] klass, hämta ytterligare information om valutakonvertering. |
| Fältgrupp | [[!UICONTROL Consent policies evaluation results map with metadata]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Fångar information om utvärderingsresultatet av flera olika medgivandeprinciper, inklusive metadatainformation om medgivandeprincipingångar och finns. |

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Datatyp | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | The `ID` fältet har bytt namn till `name`och föregående `name` fältet är nu `friendlyName`. |
| Datatyp | [[!UICONTROL Decision Proposition Details]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Lagt till en `selectionStrategy` fält som hämtar information om en urvalsstrategi. |
| Fältgrupp | [[!UICONTROL Experience Event - Proposition Interactions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Fältgruppen är nu kompatibel med [!UICONTROL Journey Step Event] klassen. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | The `ID` fältet har bytt namn till `name`. |
| Datatyp | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Återställde en mönsterändring till videosegmentegenskapen. |
| Datatyp | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Borttagen `droppedFrameCount` fält. |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Bytt namn på `isAuthorized` fält till `authorized`och uppdaterade `type` till en sträng när den tidigare var en boolesk. |
| Datatyp | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Flera nya fält har lagts till: `shipDate`, `trackingNumber`och `trackingURL`. |
| Fältgrupp | [[!UICONTROL AJO Entity Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Flera nya fält har lagts till: `journeyNodeID`, `journeyNodeName`och `journeyModeType`. |
| Fältgrupp | [[!UICONTROL Consumer Experience Event]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Fältgruppen är nu också kompatibel med [!UICONTROL Summary Metrics] klassen. |
| Fältgrupp | [[!UICONTROL Product Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | The `productTriggers` fältet är nu kapslat under `weather` -objekt. |
| Fältgrupp | [[!UICONTROL Relative Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | The `relativeTriggers` fältet är nu kapslat under `weather` -objekt. |
| Fältgrupp | [[!UICONTROL Severe Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | The `severeTriggers` fältet är nu kapslat under `weather` -objekt. |
| Fältgrupp | [[!UICONTROL Weather Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | The `weatherTriggers` fältet är nu kapslat under `weather` -objekt. |
| Fältgrupp | [[!UICONTROL XDM Related Business Accounts]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Fältgruppen är nu stabil. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Kommande borttagning** {#deprecation}

För att ta bort redundans i segmentmedlemskapets livscykel `Existing` status kommer att bli inaktuell från [segmentmedlemskarta](../../xdm/field-groups/profile/segmentation.md) i slutet av mars 2023. Ett uppföljningsmeddelande kommer att innehålla det exakta datumet för borttagningen.

Efterborttagning representeras profiler som är kvalificerade i ett segment som `Realized` och de diskvalificerade profilerna kommer även fortsättningsvis att representeras som `Exited`. Detta kommer att skapa paritet med filbaserade mål med `Active` och `Expired` segmentstatus.

Den här ändringen kan påverka dig om du använder [företagsmål](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) och har automatiserade processer längre fram i kedjan baserade på `Existing` status. Granska dina integreringar längre fram i kedjan om så är fallet. Om du är intresserad av att identifiera nyligen kvalificerade profiler längre än en viss tid, vänligen väl använda en kombination av `Realized` status och `lastQualificationTime` i din medlemskarta. Mer information får du av Adobe.

Om du vill veta mer om kundprofilen i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med profildata, kan du börja med att läsa [Översikt över kundprofiler i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Import av massvärde i Segment Builder | Segment Builder har nu stöd för import av flera värden, antingen genom att en CSV- eller TSV-fil överförs eller genom att kommaavgränsade värden infogas manuellt. Mer information finns i [Segment Builder Guide](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Utgångsdatum för externt medlemskap | Som standard behålls medlemskap för externa målgrupper i 30 dagar. Om du vill behålla dem längre använder du `validUntil` när målgruppsdata hämtas. |
| Utgångsdatum för plattformsgenererat segmentmedlemskap | Alla segmentmedlemskap som finns i `Exited` i mer än 30 dagar, baserat på `lastQualificationTime` kan tas bort. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Tillåt användaråtkomst till undermappar för molnlagringskällor | Nu kan du definiera åtkomst till en viss undermapp i molnlagringskällan när du skapar ett nytt konto. När de har skapats kan användarna bara komma åt data från den tillåtna undermappen. Den här funktionen är tillgänglig för följande molnlagringskällor: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud-lagring](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)och [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Tillgänglighet för betaversion av [!DNL SugarCRM] | [!DNL SugarCRM] Nu finns källor i betaversionen. Använd [!DNL SugarCRM Accounts & Contacts] och [!DNL SugarCRM Events] källor som hämtar data från [!DNL SugarCRM] konto till Experience Platform. Mer information finns i [[!DNL SugarCRM] översikt](../../sources/connectors/crm/sugarcrm.md). |
