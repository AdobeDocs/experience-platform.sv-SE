---
title: Versionsinformation om Adobe Experience Platform – februari 2025
description: Versionsinformationen för Adobe Experience Platform från februari 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 22%

---

# Versionsinformation om Adobe Experience Platform

>[!TIP]
>
>Den här versionen innehåller förbättringar av tillägget Federated Audience Composition. Mer information finns i [Versionsinformationen om sammansatt publikation för federerade användare](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes).

**Releasedatum: 18 februari 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Katalogtjänst](#catalog-service)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Källor](#sources)
- [Dokumentationsuppdateringar](#documentation-updates)
   - [Jämförelse mellan nätverk och nav i Edge](#edge)
   - [Utökat API för flödestjänst för källor](#flow-service)
   - [Säkerhetskopiera objektkonfigurationer med sandlådeverktyg](#back-up-object-configurations)
   - [Skapa ett högklassigt centrum med sandlådeverktyg](#center-of-excellence)
   - [Upplev kvarhållande av händelsedatauppsättningar i datasjön](#experience-event-dataset-retention)

## AI-assistenten {#ai-assistant}

AI-assistenten i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att påskynda dina arbetsflöden i Adobe-programmen. Du kan använda AI-assistenten för att lära dig mer om produkter, felsöka problem eller söka efter information och få insikter om användningen. AI Assistant stöder Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för automatisk ifyllnad av frågor | När du skickar in en fråga till AI Assistant kan du nu välja från en lista med rekommenderade frågor som finns i AI Assistant. Använd den här funktionen för att ytterligare snabba upp arbetsflödena med AI Assistant. Mer information finns i guiden om [att använda automatisk komplettering av frågor med AI Assistant](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Stöd för datauppsättningssynlighet | Nu kan du använda AI Assistant för att besvara frågor om specifika datamängdsmått, som lagringsstorlekar och radantal. Frågor som rör datasynkronisering stöder kvalificerare som du kan använda för att filtrera dina frågor under en viss tidsperiod. Mer information finns i [AI Assistant-frågeguiden](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Mer information finns i [AI Assistant-översikten](../../ai-assistant/home.md).

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## Katalogtjänst {#catalog-service}

Catalog Service är det system som registrerar var data finns och hur de härstammar från Adobe Experience Platform. Alla data som tas in i Experience Platform lagras i datasjön som filer och kataloger medan katalogen innehåller metadata och beskrivningar av dessa filer och kataloger för sök- och övervakningsändamål.

| Funktion | Beskrivning |
| --- | --- |
| Ny API-slutpunkt | Hantera dina Adobe Experience Platform-datauppsättningsmetadata effektivare med nya [katalogtjänstens API /v2/dataSets/{DATASET_ID} slutpunkt](../../catalog/api/update-object.md#patch-v2-notation). Uppdatera enkelt komplexa, djupt inkapslade datauppsättningsattribut när systemet automatiskt skapar saknade sökvägsnivåer för att spara tid, minska antalet manuella steg och minimera antalet fel. |

{style="table-layout:auto"}

Mer information om katalogtjänsten finns i [Katalogtjänstöversikt](../../catalog/home.md).

## Dataförberedelse {#data-prep}

Använd dataförberedelse för att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrat stöd för import och export av mappningar | Nu kan du exportera mappningar till en CSV-fil och konfigurera dem lokalt i ett kalkylblad. Du kan sedan importera dina uppdaterade mappningar till Experience Platform via mappningsgränssnittet i användargränssnittet. Du kan använda den här funktionen för att konfigurera ett stort antal mappningar utan att behöva bygga dem manuellt i användargränssnittet. När du skapar ett nytt dataflöde kan du dessutom överföra en kopia av dina mappningar direkt till Experience Platform för att snabba upp arbetsflödet. Mer information finns i handboken om [import och export av mappningar](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Mer information finns i [översikten över dataförberedelser](../../data-prep/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Använd [!DNL Marketo Engage Person Sync]-anslutningen för att strömma uppdateringar från personmålgrupper till motsvarande poster i [!DNL Marketo Engage]-instansen. Den här målanslutningen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant för att få åtkomst. |
| [Allmän tillgänglighet för Trade Desk CRM-anslutningen](/help/destinations/catalog/advertising/tradedesk-emails.md) | [!DNL The Trade Desk CRM]-anslutningen är nu allmänt tillgänglig. Använd CRM-målet [!DNL The Trade Desk] för att aktivera profiler för ditt [!DNL Trade Desk]-konto för målgruppsanpassning och inaktivering baserat på CRM-data. |
| [RainFocus Attendee Profiles-anslutning](/help/destinations/catalog/marketing-automation/rainfocus.md) | Använd målet [!DNL RainFocus Attendee Profiles] för att strömma kundprofiler från Adobe Experience Platform till plattformen [!DNL RainFocus] för att skapa och uppdatera deltagarprofiler. |
| [Villkorsanslutning](/help/destinations/catalog/advertising/criteo.md) allmän tillgänglighet | Anslutningen [!DNL Criteo] är nu allmänt tillgänglig. Kriteriet ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personaliserade för att nå kunder med rätt annons, vid rätt tidpunkt. |
| [[!DNL Amazon Ads] anslutning](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads]-anslutningen, som tidigare var i betaversion, är nu allmänt tillgänglig. Kopplaren har också uppdaterats för att skicka en medgivande signatur för alla profiler som har samtyckt till att få sina personuppgifter använda för annonsering. Läs mer om den nya kontrollen [Amazon Ads Consent Signal](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| Använd åtkomstetiketter för att hantera användaråtkomst till måldataflöden | Som en del av funktionen [[!UICONTROL attribute-based access control]](/help/access-control/abac/overview.md) i Real-Time CDP kan du nu använda åtkomstetiketter i [måldataflöden](/help/dataflows/ui/monitor-destinations.md). På så sätt kan du se till att bara en delmängd av användarna i organisationen får tillgång till specifika måldataflöden. <br> **Viktigt**: När du söker efter måldataflöden med sökrutan högst upp i Experience Platform användargränssnitt, kan resultatet innehålla måldataflöden som dina användaretiketter begränsar dig från att se. Detta beteende kommer att korrigeras i en framtida uppdatering. |
| [Målgruppsrapportering](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) för [Marketo Engage-anslutningen](/help/destinations/catalog/adobe/marketo-engage.md) | Du kan nu [visa information](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) om aktiverade, exkluderade eller misslyckade identiteter som har delats upp på en målgruppsnivå för varje målgrupp som ingår i dataflödena för det här målet. |
| Externa målgrupper har stöd för [TikTok](/help/destinations/catalog/social/tiktok.md)- och [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md)-anslutningar | Du kan aktivera externa målgrupper för dessa mål från [anpassade överföringar](../../segmentation/ui/audience-portal.md#import-audience) och [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Ett problem i Destination SDK testverktyg har åtgärdats. Vissa kunder eller partners stötte på problem med [exempelprofilgenereringsverktyget](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) på grund av ett format som inte stöds när det schema som används för att generera profiler innehöll datatyper med en `No format`-väljare.
- Ett problem har korrigerats när `targetConnection`-specifikationen för destinationer uppdaterades med API:t för Flow Service. I vissa fall fungerar PATCH-åtgärden på ungefär samma sätt som en POST-åtgärd, vilket gör att befintliga dataflöden skadas. Problemet är nu åtgärdat och alla kunder kan använda API:t för Flow Service för att uppdatera sin `targetConnection`-specifikation. [Läs mer](/help/destinations/api/edit-destination.md#patch-target-connection).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för vyer i [!DNL Microsoft Dynamics] | Du kan nu importera `"entityType": "view"` när du använder källan [!DNL Microsoft Dynamics]. Mer information finns i guiden om att [ansluta en [!DNL Microsoft Dynamics] källa till Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

## Dokumentationsuppdateringar {#documentation-updates}

### Edge Network och navet - jämförelse {#edge}

I jämförelsen [Edge Network och hubben](../../landing/edge-and-hub-comparison.md) finns en översikt som beskriver skillnaderna mellan de två servertyperna för Adobe Experience Platform (nav och Edge Network), inklusive vilka tjänster som är tillgängliga för varje servertyp, servrarnas platser samt rekommenderade scenarier för användning av varje servertyp.

### Utökad API-referens för Flow Service för källor {#flow-service}

[[!DNL Flow Service] API-referensen](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) för källor har uppdaterats med nya API-exempel för begäran och svar. Använd den utökade API-referensen för att skapa och uppdatera anslutningsspecifikationer när du integrerar din egen källa till Experience Platform. Du kan också använda den utökade API-referensen för att utföra tillståndsövergångar på källenheter, uppdatera befintliga käll- och målanslutningar samt hämta flöden och flödesspecifikationer utifrån ett visst filtervillkor.

### Säkerhetskopiera objektkonfigurationer med sandlådeverktyg {#back-up-object-configurations}

Läs [konfigurationsguiden för säkerhetskopierade objekt](../../sandboxes/use-cases/backup-object-configuration.md) om du vill ha stegvisa instruktioner om hur du skapar ett säkerhetskopieringspaket med hjälp av sandlådeverktyg för att se till att dina objektkonfigurationer lagras och skyddas.

### Skapa ett högklassigt centrum med sandlådeverktyg {#center-of-excellence}

I guiden [Center of Quality Guide](../../sandboxes/use-cases/center-of-excellence.md) finns stegvisa instruktioner om hur du skapar ett&quot;gyllene sandlådepaket&quot; som fungerar som ett center för hög kvalitet för att dela nyckelkonfigurationer på ett effektivt sätt.

### Upplev kvarhållande av händelsedatauppsättningar i datasjön {#experience-event-dataset-retention}

Ta kontrollen över Experience Event-datamängdens lagring i Adobe Experience Platform med hjälp av TTL (Time-To-Live). [Den här guiden](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) hjälper dig att utvärdera, konfigurera och hantera TTL-inställningar för att automatiskt ta bort föråldrade poster, optimera lagringsutrymmet och behålla dina data relevanta. Upptäck bästa praxis, användningsexempel från verkligheten och viktiga överväganden för att förbättra er livscykelhantering av data.
