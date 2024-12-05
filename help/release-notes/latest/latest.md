---
title: Versionsinformation om Adobe Experience Platform – november 2024
description: Versionsinformationen för Adobe Experience Platform från november 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f43e120225bcca640cc46ebdce1e4d61100ad45
workflow-type: ht
source-wordcount: '850'
ht-degree: 100%

---

# Versionsinformation om Adobe Experience Platform

>[!TIP]
>
>Den nya [produktdokumentationen för AI-assistenten](../../ai-assistant/landing.md) är nu tillgänglig. Använd den här sidan som nav för alla AI-assistent-relaterade resurser.

**Versionens datum: 26 november 2024**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Mål ](#destinations)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Dokumentationsuppdateringar](#documentation-updates)
   - [Interaktiv Experience Platform API-dokumentation](#interactive-experience-platform-api-documentation)
   - [Ny innehållsförteckning i Experience League](#new-table-of-contents-on-experience-league)
   - [Ny landningssida för AI-assistenten](#new-ai-assistant-landing-page)

## AI-assistenten {#ai-assistant}

AI-assistenten i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att påskynda dina arbetsflöden i Adobe-programmen. Du kan använda AI-assistenten för att lära dig mer om produkter, felsöka problem eller söka efter information och få insikter om användningen. AI-assistenten stöder Experience Platform, plattformen för kunddata i realtid, Adobe Journey Optimizer och Customer Journey Analytics.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Övervaka viktiga ändringar och prognostisera målgruppstillväxt | Använd AI-assistenten för att övervaka betydande förändringar och tillhandahålla tillväxtprognoser för din målgrupp och dina datauppsättningsstorlekar. Sedan kan du använda den här informationen för att säkerställa integriteten för dina målgruppsdata och erbjuda förutseende prognoser som stöder dataunderbyggda beslut. Mer information finns i guiden om [att övervaka viktiga ändringar och prognostisera målgruppstillväxt](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Naturlig språkuppskattning | Använd AI-assistentens funktioner för naturlig språkuppskattning för att uppskatta målgruppsstorlekar och förutsäga målgruppsbenägenhet baserat på enkla samtalsfrågor. Mer information finns i guiden om [att använda naturlig språkuppskattning med AI-assistenten](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Magnite-strömning i realtid](/help/destinations/catalog/advertising/magnite-streaming.md) | Exportera målgrupper för aktivering, målgruppsanpassning eller nedtryckning i strömningsplattformen Magnite. Observera att för att målgrupper ska kunna exporteras korrekt till Magnite måste du använda både realtids- och gruppmålen. |
| [Strömningsgrupp för Magnite](/help/destinations/catalog/advertising/magnite-batch.md) | Exportera målgrupper för aktivering, målgruppsanpassning eller nedtryckning i strömningsplattformen Magnite. Observera att för att målgrupper ska kunna exporteras korrekt till Magnite måste du använda både realtids- och gruppmålen. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| [Leta upp profilattribut i realtid på Edge](/help/destinations/ui/activate-edge-profile-lookup.md) | Läs mer om hur du söker upp Edge-profilattribut i realtid för att leverera personanpassade upplevelser eller informerar beslutsregler via program i senare led med hjälp av API:et för personanpassade mål och Edge Network. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Frågetjänst {#query-service}

Fråga efter data i Adobe Experience Platforms datasjö med hjälp av standard-SQL med Frågetjänst. Kombinera datauppsättningar sömlöst och generera nya från dina frågeresultat för att driva rapportering, aktivera datavetenskapliga arbetsflöden eller underlätta inmatning i kundprofil i realtid. Du kan till exempel sammanfoga kundtransaktionsdata med beteendedata för att identifiera värdefulla målgrupper för riktade marknadsföringskampanjer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Auktoriserings-API för Data Distiller | Hantera och tillämpa IP-baserade åtkomstbegränsningar för frågetjänstsandlådor för att förbättra datasäkerheten och säkerställa efterlevnad av organisationspolicyer. Se [guiden om auktoriserings-API:et för Data Distiller](../../query-service/auth-api/overview.md) för mer information om dess nyckelfunktioner och möjligheter, eller [OpenAPI-dokumentationen](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) för omfattande information inklusive slutpunktsdetaljer, parameterlistor, begäran/ svarsexempel och testmöjligheter. |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Platform-sinstans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Paketdelning med API:et för verktyg i sandlådan | Använd två nya API-slutpunkter, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) och [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), för att hantera paketdelning i olika organisationer, till exempel begära godkännanden, paketsynlighet och importera paket, med API:et för verktyg i sandlådan. |

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Dokumentationsuppdateringar {#documentation-updates}

### Interaktiv Experience Platform API-dokumentation {#interactive-api-documentation}

[Dokumentationen om Experience Platform API](https://developer.adobe.com/experience-platform-apis/) är nu helt interaktiv, vilket gör att du kan autentisera och utforska API:er direkt på API:ets referensdokumentationssida. Du kan nu gå till den önskade API-referensdokumentationssidan, skapa eller hämta dina API-autentiseringsuppgifter, klistra in dem i blocket **[!UICONTROL Try it]** och köra anropet. Allt på en sida. [Läs mer](/help/landing/api-authentication.md#get-credentials-functionality) om funktionaliteten.

### Ny innehållsförteckning i Experience League {#new-table-of-contents-on-experience-league}

Innehållsförteckningen på Experience Leagues dokumentationssidor har förbättrats så att läsarna får en bättre upplevelse, bland annat ett nyckelordsfilter för att identifiera exakt vilken sida du behöver, möjligheten att expandera alla sidor med mera. <br> ![Ny upplevelse av innehållsförteckningen, inklusive nyckelordsfilter och möjligheten att expandera alla sidor.](../2024/assets/november/new-toc-experience.gif "Ny upplevelse av innehållsförteckningen, inklusive nyckelordsfilter och möjligheten att expandera alla sidor."){width="250" align="center" zoomable="yes"}

### Ny landningssida för AI-assistenten {#new-ai-assistant-landing-page}

Använd den nya [produktdokumentationssidan för AI-assistenten](../../ai-assistant/landing.md) som nav för allt som har med AI-assistenten att göra. I produktdokumentationen finns videosjälvstudiekurser, teknisk dokumentation, användningsfall och länkar till blogginlägg om AI-assistenten.