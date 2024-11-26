---
title: Versionsinformation om Adobe Experience Platform november 2024
description: Versionsinformation november 2024 för Adobe Experience Platform.
source-git-commit: d87747c2181f4ae378e1341c3c190cc6fa57d4b0
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 29%

---

# Versionsinformation om Adobe Experience Platform

>[!TIP]
>
>Landningssidan för den nya [AI Assistant-produktdokumentationen](../../ai-assistant/landing.md) är nu tillgänglig. Använd den här sidan som nav för alla AI Assistant-relaterade resurser.

**Releasedatum: 26 november 2024**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Mål ](#destinations)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Dokumentationsuppdateringar](#documentation-updates)
   - [Interaktiv Experience Platform API-dokumentation](#interactive-experience-platform-api-documentation)
   - [Ny innehållsförteckning på Experience League](#new-table-of-contents-on-experience-league)
   - [Ny startsida för AI Assistant](#new-ai-assistant-landing-page)

## AI-assistenten {#ai-assistant}

AI-assistenten i Adobe Experience Platform är en konversationsupplevelse som du kan använda för att påskynda dina arbetsflöden i Adobe-programmen. Du kan använda AI-assistenten för att lära dig mer om produkter, felsöka problem eller söka efter information och få insikter om användningen. AI-assistenten stöder Experience Platform, plattformen för kunddata i realtid, Adobe Journey Optimizer och Customer Journey Analytics.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Övervaka viktiga ändringar och prognostisera målgruppstillväxt | Använd AI Assistant för att övervaka betydande förändringar och tillhandahålla tillväxtprognoser för er målgrupp och era datauppsättningsstorlekar. Sedan kan ni använda den här informationen för att säkerställa integriteten för era målgruppsdata och erbjuda förutseende prognoser som stöder dataunderbyggda beslut. Mer information finns i guiden [Övervaka viktiga ändringar och prognostisera målgruppstillväxt](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Naturlig språkuppskattning | Använd AI Assistants naturliga funktioner för språkinskattning för att uppskatta målgruppsstorlekar och förutse målgruppernas egenskaper baserat på enkla, konversationsfrågor. Mer information finns i guiden om [att använda beräkning av naturligt språk med AI Assistant](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Direktuppspelning i realtid](/help/destinations/catalog/advertising/magnite-streaming.md) | Exportera målgrupper för aktivering, målgruppsanpassning eller nedtryckning i Magnite Streaming-plattformen. Observera att för att målgrupper ska kunna exporteras korrekt till Magnite måste du använda både realtids- och gruppmålen. |
| [Streaming Batch för drapport](/help/destinations/catalog/advertising/magnite-batch.md) | Exportera målgrupper för aktivering, målgruppsanpassning eller nedtryckning i Magnite Streaming-plattformen. Observera att för att målgrupper ska kunna exporteras korrekt till Magnite måste du använda både realtids- och gruppmålen. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| [Leta upp profilattribut i realtid på kanten](/help/destinations/ui/activate-edge-profile-lookup.md) | Lär dig hur du söker upp edge-profilattribut i realtid för att leverera personaliserade upplevelser eller informerar beslutsregler via program längre fram i kedjan med hjälp av API:t för anpassade Personalization-mål och Edge Network. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Frågetjänst {#query-service}

Frågedata i Adobe Experience Platform datasjön med hjälp av standard-SQL med Query Service. Kombinera enkelt datauppsättningar och generera nya från frågeresultaten till kraftfull rapportering, möjliggör arbetsflöden för datavetenskap eller underlättar inmatning i kundprofilen i realtid. Ni kan till exempel sammanfoga kundtransaktionsdata med beteendedata för att identifiera värdefulla målgrupper för riktade marknadsföringskampanjer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Dater Distiller Authorization API | Hantera och tillämpa IP-baserade åtkomstbegränsningar för frågetjänstsandlådor, för att förbättra datasäkerheten och säkerställa efterlevnad av organisationsprofiler. Mer information om nyckelfunktioner och -funktioner finns i [API-handboken för dataauktorisering](../../query-service/auth-api/overview.md), eller i [OpenAPI-dokumentationen](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/), som innehåller information om slutpunkter, parameterlistor, exempel på begäran/svar och testningsfunktioner. |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Platform-sinstans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Paketdelning med sandlådeverktygs-API | Använd två nya API-slutpunkter, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) och [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), för att hantera paketdelning i olika organisationer, till exempel begära godkännanden, paketsynlighet och importera paket, med sandlådeverktygets API. |

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Dokumentationsuppdateringar {#documentation-updates}

### Interaktiv Experience Platform API-dokumentation {#interactive-api-documentation}

[Experience Platform API-dokumentationen](https://developer.adobe.com/experience-platform-apis/) är nu helt interaktiv, vilket gör att du kan autentisera och utforska API:er direkt på API:ts referensdokumentationssida. Du kan nu gå till den önskade API-referensdokumentationssidan, skapa eller hämta dina API-autentiseringsuppgifter, klistra in dem i blocket **[!UICONTROL Try it]** och köra anropet. Allt på en sida. [Läs mer](/help/landing/api-authentication.md#get-credentials-functionality) om funktionerna.

### Ny innehållsförteckning på Experience League {#new-table-of-contents-on-experience-league}

Innehållsförteckningen på Experience League dokumentationssidor har förbättrats så att läsarna får en bättre upplevelse, bland annat ett nyckelordsfilter för att identifiera exakt vilken sida du behöver, möjligheten att expandera alla sidor med mera. <br> ![Ny innehållsförteckning, inklusive nyckelordsfilter och möjlighet att expandera alla sidor.](../2024/assets/november/new-toc-experience.gif "Ny upplevelse av innehållsförteckning, inklusive nyckelordsfilter och möjlighet att expandera alla sidor."){width="250" align="center" zoomable="yes"}

### Ny startsida för AI Assistant {#new-ai-assistant-landing-page}

Använd den nya produktdokumentationssidan för [AI Assistant](../../ai-assistant/landing.md) som nav för allt som AI Assistant. I produktdokumentationen finns videokurser, teknisk dokumentation, användningsfall och länkar till blogginlägg om AI Assistant.