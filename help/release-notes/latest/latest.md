---
title: Versionsinformation om Adobe Experience Platform – februari 2025
description: Versionsinformationen för Adobe Experience Platform från februari 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8786ac8ab42d2b9e0c43000bbc6604462ea06f64
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 94%

---

# Versionsinformation om Adobe Experience Platform

>[!TIP]
>
>Den här versionen innehåller förbättringar av tillägget Federerad målgruppssammansättning. Mer information finns i [Versionsinformationen om Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes).

**Releasedatum: 18 februari 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Katalogtjänst](#catalog-service)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Källor](#sources)
- [Dokumentationsuppdateringar](#documentation-updates)
   - [Jämförelse mellan Edge Network och Hub](#edge)
   - [Utökat API för flödestjänst för källor](#flow-service)
   - [Säkerhetskopiera objektkonfigurationer med sandlådeverktyg](#back-up-object-configurations)
   - [Aktivera ett kompetenscentrum med hjälp av sandlådeverktyg](#center-of-excellence)
   - [Upplev kvarhållande av händelsedatauppsättningar i datalagret](#experience-event-dataset-retention)

## AI-assistenten {#ai-assistant}

AI-assistenten i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att påskynda dina arbetsflöden i Adobe-programmen. Du kan använda AI-assistenten för att lära dig mer om produkter, felsöka problem eller söka efter information och få insikter om användningen. AI-assistenten stöder Experience Platform, plattformen för kunddata i realtid, Adobe Journey Optimizer och Customer Journey Analytics.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för automatisk ifyllnad av frågor | När du skickar in en fråga till AI-assistenten kan du nu välja från en lista över rekommenderade frågor som AI-assistenten tillhandahåller. Använd den här funktionen för att ytterligare snabba upp arbetsflödena med AI-assistenten. Mer information finns i guiden om [att använda den automatiska ifyllnaden av frågor med AI-assistenten](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Stöd för datauppsättningssynlighet | Du kan nu använda AI-assistenten för att besvara frågor om specifika datauppsättningsmått, som lagringsstorlekar och radantal. Frågor som rör datasynlighet stöder kvalificerare som du kan använda för att filtrera dina frågor under en viss tidsperiod. Mer information finns i [frågeguiden om AI-assistenten](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över AI-assistenten](../../ai-assistant/home.md).

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## Katalogtjänst {#catalog-service}

Catalog Service är det system som registrerar var data finns och hur de härstammar från Adobe Experience Platform. Alla data som tas in i Experience Platform lagras i datasjön som filer och kataloger medan katalogen innehåller metadata och beskrivningar av dessa filer och kataloger för sök- och övervakningsändamål.

| Funktion | Beskrivning |
| --- | --- |
| Ny API-slutpunkt | Hantera dina metadata för Adobe Experience Platform-datauppsättning effektivare med nya [slutpunkten Catalog Service API /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Uppdatera enkelt komplexa och djupt inkapslade datauppsättningsattribut när systemet automatiskt skapar saknade sökvägsnivåer för att spara tid, minska antalet manuella steg och minimera antalet fel. |

{style="table-layout:auto"}

Mer information om Katalogtjänsten finns i [översikten över Katalogtjänsten](../../catalog/home.md).

## Dataförberedelse {#data-prep}

Använd dataförberedelse för att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrat stöd för import och export av mappningar | Du kan nu exportera mappningar till en CSV-fil och konfigurera dem lokalt i ett kalkylblad. Du kan sedan importera dina uppdaterade mappningar till Experience Platform via mappningsgränssnittet i användargränssnittet. Du kan använda den här funktionen för att konfigurera ett stort antal mappningar utan att behöva bygga dem manuellt i användargränssnittet. När du skapar ett nytt dataflöde kan du dessutom ladda upp en kopia av dina mappningar direkt till Experience Platform för att snabba upp arbetsflödet. Mer information finns i guiden om att [importera och exportera mappningar](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Mer information finns i [översikten över Dataförberedelse](../../data-prep/home.md).

## Destinationer (uppdaterad 20 februari) {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [(Beta) Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Använd anslutningen [!DNL Marketo Engage Person Sync] för att strömma uppdateringar från personmålgrupper till motsvarande poster i instansen [!DNL Marketo Engage]. Den här destinationsanslutningen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få åtkomst. |
| [Allmän tillgänglighet för Trade Desk CRM-anslutningen](/help/destinations/catalog/advertising/tradedesk-emails.md) | Anslutningen [!DNL The Trade Desk CRM] är nu allmänt tillgänglig. Använd CRM-målet [!DNL The Trade Desk] för att aktivera profiler för ditt [!DNL Trade Desk]-konto för målgruppsanpassning och inaktivering baserat på CRM-data. |
| [Anslutning för deltagarprofiler i RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Använd målet [!DNL RainFocus Attendee Profiles] för att strömma kundprofiler från Adobe Experience Platform till plattformen [!DNL RainFocus] för att skapa och uppdatera deltagarprofiler. |
| [Anslutningen Criteos](/help/destinations/catalog/advertising/criteo.md) allmänna tillgänglighet | Anslutningen [!DNL Criteo] är nu allmänt tillgänglig. Criteo ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personanpassade för att nå kunder med rätt annons, vid rätt tidpunkt. |
| [[!DNL Amazon Ads] anslutning](../../destinations/catalog/advertising/amazon-ads.md) | Anslutningen [!DNL Amazon Ads], som tidigare var i betaversion, är nu allmänt tillgänglig. Anslutningen har också uppdaterats för att skicka en samtyckesbeviljad signal för alla profiler som har samtyckt till att få sina personuppgifter använda för annonsering. Läs mer om den nya kontrollen [Amazon Ads Consent Signal](../../destinations/catalog/advertising/amazon-ads.md#destination-details). |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| Använd åtkomstetiketter för att hantera användaråtkomst till destinationsdataflöden | Som en del av funktionen [[!UICONTROL attribute-based access control]](/help/access-control/abac/overview.md) i Real-Time CDP kan du nu tillämpa åtkomstetiketter i [destinationsdataflöden](/help/dataflows/ui/monitor-destinations.md). På så sätt kan du se till att bara en deluppsättning av användarna i organisationen får tillgång till specifika destinationsdataflöden. <br> **Viktigt**: När du söker efter destinationsdataflöden med sökrutan högst upp i användargränssnittet Experience Platform kan resultatet innehålla destinationsdataflöden som dina användaretiketter begränsar dig från att se. Detta beteende kommer att korrigeras i en framtida uppdatering. |
| [Rapportering på målgruppsnivå](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) för [anslutningen Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Du kan nu [visa information](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) om aktiverade, exkluderade eller misslyckade identiteter som har delats upp på en målgruppsnivå för varje målgrupp som ingår i dataflödena för den här destinationen. |
| Externa målgrupper har stöd för anslutningarna [TikTok](/help/destinations/catalog/social/tiktok.md) och [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Du kan aktivera externa målgrupper för dessa mål från [anpassade uppladdningar](../../segmentation/ui/audience-portal.md#import-audience) och [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/start/audiences). |
| Exportera arrayer, kartor och objekt till molnlagringsmål | Genom att använda den nya växlingsknappen **[!UICONTROL Export arrays, maps, objects]** när du ansluter till ett molnlagringsmål kan du exportera komplexa objekt till utvalda mål. [Läs mer](/help/destinations/ui/export-arrays-calculated-fields.md) om funktionaliteten. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Ett problem i testverktygen i Destination SDK har korrigerats. Vissa kunder eller partners stötte på problem med [verktyg för generering av provprofiler](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) på grund av ett format som inte stöds när det schema som används för att generera profiler innehöll datatyper med en `No format`-väljare.
- Ett problem när `targetConnection`-specifikationen för destinationer uppdaterades med API för flödestjänst har korrigerats. I vissa fall fungerar PATCH-åtgärden på ungefär samma sätt som en POST-åtgärd, vilket gör att befintliga dataflöden skadas. Problemet är nu åtgärdat och alla kunder kan använda API för flödestjänst för att uppdatera sin `targetConnection`-specifikation. [Läs mer](/help/destinations/api/edit-destination.md#patch-target-connection).
- När du exporterar profiler till filbaserade mål säkerställer borttagning av dubbletter att endast en profil exporteras när flera profiler delar samma nyckel för borttagning av dubbletter och samma referenstidstämpel. Den här versionen innehåller en uppdatering av processen för borttagning av dubbletter, vilket säkerställer att efterföljande körningar med samma koordinater alltid ger samma resultat, vilket förbättrar konsekvensen. [Läs mer](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för vyer i [!DNL Microsoft Dynamics] | Du kan nu fylla på `"entityType": "view"` när du använder källan [!DNL Microsoft Dynamics]. Mer information finns i guiden om att [ansluta en [!DNL Microsoft Dynamics] källa till Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

## Dokumentationsuppdateringar {#documentation-updates}

### Jämförelse mellan Edge Network och Hub {#edge}

I jämförelsen [Edge Network och hubben](../../landing/edge-and-hub-comparison.md) finns en översikt som beskriver skillnaderna mellan de två servertyperna för Adobe Experience Platform (hubb och Edge Network), inklusive vilka tjänster som är tillgängliga för varje servertyp, servrarnas platser samt rekommenderade scenarier för användning av varje servertyp.

### Utökad API-referens för flödestjänst för källor {#flow-service}

[[!DNL Flow Service] API-referensen](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) för källor har uppdaterats med nya API-exempel för begäran och svar. Använd den utökade API-referensen för att skapa och uppdatera anslutningsspecifikationer när du integrerar din egen källa till Experience Platform. Du kan också använda den utökade API-referensen för att utföra tillståndsövergångar på dina källenheter, uppdatera befintliga käll- och målanslutningar och hämta flöden och flödesspecifikationer med hjälp av specifika filtreringskriterier.

### Säkerhetskopiera objektkonfigurationer med sandlådeverktyg {#back-up-object-configurations}

Läs [konfigurationsguiden för säkerhetskopierade objekt](../../sandboxes/use-cases/backup-object-configuration.md) om du vill ha stegvisa instruktioner om hur du skapar ett säkerhetskopieringspaket med hjälp av sandlådeverktyg för att se till att dina objektkonfigurationer lagras och skyddas.

### Aktivera ett kompetenscentrum med hjälp av sandlådeverktyg {#center-of-excellence}

Läs guiden [Kompetenscentrum](../../sandboxes/use-cases/center-of-excellence.md) för stegvisa instruktioner om hur du skapar ett paket med en ”gyllene sandlåda” som fungerar som ett kompetenscentrum för effektiv delning av viktiga konfigurationer.

### Upplev kvarhållande av händelsedatauppsättningar i datalagret {#experience-event-dataset-retention}

Ta kontroll över lagring av datauppsättningar för upplevelsehändelser i Adobe Experience Platform med hjälp av Time-To-Live (TTL). Med [den här guiden](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) kan du utvärdera, konfigurera och hantera TTL-inställningar för att automatiskt ta bort föråldrade poster, optimera lagringsutrymmet och se till att dina data är relevanta. Upptäck bästa praxis, användningsexempel från verkligheten och viktiga överväganden för att förbättra livscykelhanteringen av data.
