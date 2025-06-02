---
title: Versionsinformation om Adobe Experience Platform – maj 2025
description: Versionsinformation för maj 2025 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ab9302a40547349c8d0390baafd8591ed6859e1
workflow-type: ht
source-wordcount: '1522'
ht-degree: 100%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 20 maj 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Katalogtjänst](#catalog-service)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Identitetstjänst](#identity)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## AI-assistenten {#ai-assistant}

AI-assistenten i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att påskynda dina arbetsflöden i Adobe-programmen. Du kan använda AI-assistenten för att lära dig mer om produkter, felsöka problem eller söka efter information och få insikter om användningen. AI-assistenten stöder Experience Platform, plattformen för kunddata i realtid, Adobe Journey Optimizer och Customer Journey Analytics.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för Product Support Agent | Nu kan du använda Product Support Agent i AI-assistenten för att felsöka utan att lämna dina arbetsflöden. Supportadministratörer i din organisation kan nu använda Product Support Agent för att skapa kundsupportärenden med kontext- och sessionsinformation från dina interaktioner med AI-assistenten. <br><br>Åtkomst till Product Support Agent gäller till och med 30 november 2025. Du måste kontakta din Adobe-kontorepresentant för att få en licens till Product Support Agent och fortsätta använda funktionen efter detta datum. Mer information finns i dokumentationen för [Product Support Agent](../../ai-assistant/new-features/customer-support.md). |

Mer information finns i [översikten över AI-assistenten](../../ai-assistant/landing.md).

## Katalogtjänst {#catalog-service}

Catalog Service är det system som registrerar var data finns och hur de härstammar från Adobe Experience Platform. Alla data som tas in i Experience Platform lagras i datasjön som filer och kataloger medan katalogen innehåller metadata och beskrivningar av dessa filer och kataloger för sök- och övervakningsändamål.

| Funktion | Beskrivning |
| --- | --- |
| Optimera datalagring med regler för lagring på datauppsättningsnivå | Hantera datalagring effektivt med lagringspolicyer som tar bort inaktuella data baserat på en angiven tidsram. <ul><li>**Lagra datauppsättningar**: Ange datauppsättningsregler om du vill ta bort inaktuella data från datalagret och Profile Store.</li><li>**Lagringsinsikter**: Övervaka användningen och se till att det licensierade berättigandet följs via interna mätvärden.</li><li>**Förbättrad synlighet**: Spåra datauppsättningsaktivitet från inmatning till borttagning med förbättrad övervakning.</li><li>**Effektiv hantering**: Få åtkomst till lagringsinställningar, övervakning, granskningsloggar och insikter i en enda enhetlig vy.</li></ul> Läs guiden om [regler för lagring av datauppsättningar](../../catalog/datasets/user-guide.md#data-retention-policy) för mer information. |

{style="table-layout:auto"}

Mer information finns i [översikten över Katalogtjänsten](../../catalog/home.md).

## Dataförberedelse {#data-prep}

Använd dataförberedelse för att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för import- och exportmappningar för Adobe Analytics | Nu kan du använda import- och exportmappning för dina Adobe Analytics-rapportsvitsdata när du använder Adobe Analytics källanslutning. <br><br>Exportera dina mappningar till en CSV-fil och konfigurera dem lokalt i ett kalkylblad. Du kan sedan importera dina uppdaterade mappningar till Experience Platform via mappningsgränssnittet i användargränssnittet. Du kan använda den här funktionen för att konfigurera ett stort antal mappningar utan att behöva bygga dem manuellt i användargränssnittet. När du skapar ett nytt dataflöde kan du dessutom ladda upp en kopia av dina mappningar direkt till Experience Platform för att snabba upp arbetsflödet. <br><br>Mer information finns i guiden om att [ansluta Adobe Analytics till Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Mer information finns i [översikten över Dataförberedelse](../../data-prep/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| Uppgrading av [anpassad målgrupp för Facebook](../../destinations/catalog/social/facebook.md) och stöd för adressrelaterade identifierare | Från och med 23 maj 2025 och hela juni 2025 kan du tillfälligt se två målkort för **[!DNL Facebook Custom Audience]** i målkatalogen i upp till några timmar. Detta beror på en intern uppgradering av måltjänsten med stöd för nya fält som ger bättre målinriktning och matchning med profiler för Facebook-egenskaper. Mer information om de nya adressrelaterade fälten finns i avsnittet [identiteter som stöds](#supported-identities). <br><br>Om du ser ett kort med etiketten **[!UICONTROL (New) Facebook Custom Audience]** använder du det här kortet för nya dataflöden för aktivering. Befintliga dataflöden uppdateras automatiskt, vilket innebär att du inte behöver göra något. Alla ändringar du gör i befintliga dataflöden under den här perioden sparas efter uppgraderingen. När uppgraderingen är klar kommer målkortet **[!UICONTROL (New) Facebook Custom Audience]** att byta namn till **[!DNL Facebook Custom Audience]**. <br><br>Om du skapar dataflöden via [Flow Service-API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden: <ul><li>Flödesspecifikation-id: `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>Anslutningsspecifikation-id: `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Stöd för ID för mobilreklam för destinationen [Google Customer Match + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) | Du kan nu aktivera målgrupper för [Google kundmatchning + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) baserat på mobila annonserings-ID:n, som [!DNL GAID] och [!DNL IDFA]. |
| Stöd för ytterligare identifierare för [Google Kundmatchning](../../destinations/catalog/advertising/google-customer-match.md) | Destinationen för Google Kundmatchning har nu stöd för mappning av adressrelaterade fält för förbättrade matchningsfrekvenser på Googles plattform. <br><br>Om du vill vara säker på att Google matchar adressen måste du mappa alla fyra adressfälten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` och `address_info_postal_code`) och se till att inget av fälten saknar data i de exporterade profilerna. <br> Google matchar inte adressen om något fält antingen är omappat eller innehåller saknade data. |
| Kolumn med förfallodatum för konto för [Facebook](../../destinations/catalog/social/facebook.md)-anslutningar | Du kan nu se förfallodatum för token för Facebook-kontot på flikarna [Bläddra](../../destinations/ui/destinations-workspace.md#browse) och [Konton](../../destinations/ui/destinations-workspace.md#accounts). |
| Exportera datauppsättningar som skapats med API | Nu kan du exportera datauppsättningar som skapats med API. Den tidigare begränsningen där endast datauppsättningar som skapats i användargränssnittet var tillgängliga för export har hävts. Läs mer om [export av datauppsättningar](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Identitetstjänst {#identity}

Använd identitetstjänsten för Adobe Experience Platform för att skapa en heltäckande bild av dina kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] är nu allmänt tillgänglig. [!DNL Identity Graph Linking Rules] förhindrar diagramkollaps, vilket ger distinkta och korrekta kundprofiler för anpassad marknadsföring i Experience Platform och program. Viktiga funktioner inkluderar:<ul><li>[Diagramsimuleringsverktyg](../../identity-service/identity-graph-linking-rules/graph-simulation.md): utforska algoritmen och testa konfigurationer för identitetsinställningar.</li><li> [Identitetsinställningar](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md): konfigurera unika namnrymder och ställ in prioriteringar.</li><li>[Identitetspanelen](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs): bevaka diagram och validera identitetsinställningar.</li></ul> **Obs!** Det kommer inte att ske några ändringar i dina data fram tills att du konfigurerar dina identitetsinställningar manuellt. |

{style="table-layout:auto"}

Mer information finns i [översikten över identitetstjänsten](../../identity-service/home.md).

## Frågetjänst {#query-service}

Fråga efter data i Adobe Experience Platforms datasjö med hjälp av standard-SQL med Frågetjänst. Kombinera datauppsättningar sömlöst och generera nya från dina frågeresultat för att driva rapportering, aktivera datavetenskapliga arbetsflöden eller underlätta inmatning i kundprofil i realtid. Du kan till exempel sammanfoga kundtransaktionsdata med beteendedata för att identifiera värdefulla målgrupper för riktade marknadsföringskampanjer.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
|--------|-------------|
| Migrera inloggningsuppgifter för servicekonto (JWT) till inloggningsuppgifter för OAuth | JWT-inloggningsuppgifter som inte förfaller måste migreras till OAuth server-till-server senast 30 juni 2025 för att undvika avbrott i tjänsten. Den här ändringen förbättrar säkerheten och plattformens enhetlighet. Du hittar mer information i [guiden Migrera inloggningsuppgifter från JWT till OAuth server-till-server](../../query-service/ui/migrate-jwt-to-oauth.md). |
| Äldre resultattabell (begränsad tillgänglighet) | Användare som förlitar sig på dra för att markera-arbetsflöden kan begära åtkomst till en äldre resultattabell som har stöd för webbläsarbaserad markering och kopiering. Inklistrade utdata är flikavgränsade, vilket innebär att kolumnerna förblir anpassade och läsbara i Excel, vilket underlättar granskning av kalkylblad och QA-processer. Mer information finns i guiden för [användargränssnitt för frågeredigerare](../../query-service/ui/user-guide.md#legacy-results-table). |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Utökad support för plugin-program för verktyg i sandlådan | Kampanjer kan nu migreras med ytterligare beroende objekt via sandlådeverktyg, bland annat kanalkonfiguration, enhetliga beslut och experimentinställningar eller -varianter. I guiden för [sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects) hittar du en fullständig lista med kampanjobjekt och alla Adobe Journey Optimizer-objekt som stöds. |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatering av kriterier för segmentering av strömning | Från och med maj 2025-versionen har kriterierna för att dina målgrupper ska vara berättigade till segmentering av strömning uppdaterats. Mer information om de här ändringarna finns i [uppdatering av kriterier för strömningssegmentering](../../segmentation/eligibility-criteria-update.md). |

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för grundläggande autentisering för [!DNL MySQL] | Nu kan du använda grundläggande autentisering för att ansluta din [!DNL MySQL]-databas till Experience Platform. Läs [[!DNL MySQL] källöversikten](../../sources/connectors/databases/mysql.md) för mer information. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).