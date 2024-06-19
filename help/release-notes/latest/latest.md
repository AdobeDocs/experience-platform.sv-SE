---
title: Adobe Experience Platform Versionsinformation juni 2024
description: Versionsinformation juni 2024 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e1b56c6150274748c35fedfc1e1b6bbbf66d1bfb
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: juni 2024**

>[!TIP]
>
>[AI Assistant i Experience Platform](https://platform.adobe.com) är nu tillgängligt. Använd AI Assistant för att snabba upp arbetsflödena i Adobe-programmen. [Läs mer](#ai-assistant) om de nya funktionerna.

Nya funktioner i Adobe Experience Platform:

- [AI-assistenten](#ai-assistant)
- [Autentisering till Experience Platform API:er](#authentication-platform-apis)
- [Dataförberedelse](#data-prep)
- [Mål ](#destinations)
- [Integritetstjänst](#privacy)
- [Segmenteringstjänst](#segmentation)
- [Spelböcker med användningsexempel](#use-case-playbooks)

## AI-assistenten {#ai-assistant}

AI Assistant i Adobe Experience Platform är en samtalsupplevelse som du kan använda för att snabba upp arbetsflödena i Adobe-program. Du kan använda AI Assistant för att få en bättre förståelse för produktkunskaper, felsöka problem eller söka i information och hitta operativa insikter. AI Assistant har stöd för Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

**Ny funktion**

| Funktion | Beskrivning |
| --- | --- |
| AI Assistant i Experience Platform | Nu kan du använda AI Assistant i Experience Platform. AI Assistant har stöd för Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics. <br> ![AI Assistant i Experience Platform.](../2024/assets/june/ai-assistant-full.png "AI Assistant i Experience Platform."){width="100" zoomable="yes"} <br> Mer information om den här funktionen finns i [Användargränssnittshandbok för AI Assistant](../../ai-assistant/ui-guide.md). |
| Stöd för frågor om produktkunskap | [Produktkunskap](../../ai-assistant/home.md#product-knowledge) är begrepp och ämnen som bygger på Experience League dokumentation och kan användas för spetsiga kunskaper, öppen upptäckt och felsökning. Du kan ställa frågor om produktkunskap för AI Assistant som: <ul><li>Vad är lookalike-målgrupper?</li><li>Hur beräknas profilrikedomen?</li><li> Kan jag ta bort ett profilaktiverat schema efter att data har importerats?</li></ul> |
| [!BADGE Beta]{type=Informative} Stöd för frågor om driftsinsikter | [Driftsinsikter](../../ai-assistant/home.md#operational-insights) är svar på frågor som AI Assistant genererar om dina metadataobjekt, inklusive antal, uppslag och linjepåverkan. Användningsinsikter tittar inte på några data i din sandlåda. Du kan ställa frågor om driftsinsikter i AI Assistant, som: <ul><li>Vilka destinationer befinner sig i ett aktivt läge?</li><li>Hur många datauppsättningar har jag?</li><li>Ange de målgrupper som används i direktresor.</li></ul> Operativa insikter stöds i följande domäner: attribut, målgrupper, dataflöden, datauppsättningar, destinationer, resor, scheman och källor. |
| Access AI Assistant | För att få tillgång till AI Assistant för Experience Platform, Real-Time CDP och Journey Optimizer måste du lägga till en roll som innehåller **Aktivera AI-assistenten** och **Visa användningsinformation** behörigheter. Mer information finns i [guide för funktionsåtkomst](../../ai-assistant/access.md). Du måste använda Admin Console för [åtkomst i Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

Mer information om AI Assistant finns i [Översikt över AI Assistant](../../ai-assistant/home.md).

## Autentisering till Experience Platform API:er {#authentication-platform-apis}

JWT-metoden för att hämta åtkomsttoken är nu föråldrad för nya integreringar och ersatt av en enklare OAuth Server-till-Server-autentiseringsmetod.<p>![Ny OAuth-autentiseringsmetod för att få åtkomsttokens markerade.](/help/landing/images/api-authentication/oauth-authentication-method.png "Ny OAuth-autentiseringsmetod för att få åtkomsttokens markerade."){width="100" zoomable="yes"}</p>

Befintliga API-integrationer som använder JWT-autentiseringsmetoden fortsätter att fungera fram till 1 januari 2025, men Adobe rekommenderar starkt att du migrerar befintliga integreringar till den nya OAuth Server-till-Server-metoden före detta datum. Läs guiden på [migrera från JWT-autentiseringsuppgifter (Service Account) till OAuth Server-till-Server-autentiseringsuppgifter](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

## Dataprep (#data-prep)

Använd dataprep för att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tillägg i listan med reserverade nyckelord | Följande ord har lagts till i listan över reserverade nyckelord för dataprep:<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul>. Mer information finns i [guide för preflight-funktioner](../../data-prep/functions.md). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Förbättring av ad hoc-export-API för export av externa målgrupper | Nu kan du använda export-API:t för ad hoc för att exportera externa (anpassade uppladdningar) målgrupper. [Läs mer](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta) Ytterligare funktioner som stöds i betafasen av stöd för exportarrayer | När du tidigare aktiverade målgrupper till filbaserade mål och valde Använd beräkningsfält begränsades du till att använda en delmängd av de målgrupper som var tillgängliga via datapreturen. Den begränsningen har nu hävts och kunderna har tillgång till alla funktioner som är tillgängliga via datapresentation när de exporterar målgrupper till filbaserade destinationer. [Läs mer](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions). |
| Visa endast fält med data i mappningssteget | När du mappar profilattribut till dina mål kan du nu växla mellan alla profilattribut eller endast de som innehåller data. Som standard visas bara fält med data. Se aktiveringsguiden för [batch](../../destinations/ui/activate-batch-profile-destinations.md#mapping) och [direktuppspelning](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) mål för mer information. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessregler.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Privacy Service support för Adobe Journey Optimizer | Privacy Servicen är nu kompatibel med Adobe Journey Optimizer protokoll för bearbetning av borttagningsbegäranden. Se [Dokumentation om sekretessförfrågningar från Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) om du vill ha mer information, eller Experience Platform-dokumentationen om du vill se en lista över [Experience Cloud-program som är integrerade med Privacy Servicen](../../privacy-service/experience-cloud-apps.md). |

Se [Översikt över Privacy Servicen](../../privacy-service/home.md) om du vill ha mer information om tjänsten.

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatering av tidsbegränsningar | Beteendet för&quot;Den här månaden&quot; och&quot;Det här året&quot; har uppdaterats och representerar nu&quot;månad till datum&quot; respektive&quot;år till datum&quot;. Mer information om den här ändringen finns i [Segment Builder Guide](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service], se [Översikt över segment](../../segmentation/home.md).

## Spelböcker med användningsexempel {#use-case-playbooks}

[!DNL Use Case Playbooks] utan extra kostnad för alla Adobe Experience Platform-kunder. Om du vill få tillgång till ett omfattande galleri med fallspelningsböcker i användargränssnittet för Experience Platform kan du nu välja **[!UICONTROL Playbooks]** från vänster navigering.

[!DNL Use Case Playbooks] är utformade för att hjälpa dig att klara utmaningar när du börjar med Real-time Customer Data Platform eller Adobe Journey Optimizer. De ger vägledning och genererar olika resurser som du kan testa och importera till produktionsmiljöer när du är redo, även om du inte vet var du ska börja eller hur du ska producera rätt resurser för det avsedda användningsområdet.

Läs mer i [Använd fallspelningsböcker - översikt](/help/use-case-playbooks/playbooks/overview.md), som ger en översikt över spelbokens funktion, syfte och en heltäckande demonstration, inklusive hur du skapar instanser och importerar genererade resurser till andra sandlådemiljöer.

Om du vill veta hur du kan komma åt och konfigurera en inspirerande sandlåda för att experimentera och utforska olika fallspelningsböcker kan du läsa [Upptäck rätt spelningsbok](/help/use-case-playbooks/playbooks/discover.md) -dokument.

Mer information om [!DNL Use Case Playbooks]kan du läsa följande dokumentationssidor:

- Hämta en lista med alla [tillgängliga spelböcker](/help/use-case-playbooks/playbooks/playbooks-list.md), grupperade efter produkt (Real-Time CDP eller Journey Optimizer).
- Läs mer om vad [behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) är nödvändiga för att du ska kunna använda spelböcker och de resurser som de skapar.
- Förstå [funktioner för datainlärning](/help/use-case-playbooks/playbooks/data-awareness.md) som gör att du kan duplicera genererade resurser till andra sandlådemiljöer.
