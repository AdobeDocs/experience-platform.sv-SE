---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 41%

---


# Information om förhandsversionen av Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet är avsett som en **förhandsgranskning** av versionsinformationen för den aktuella månaden. Utgivningsobjekt kan ändras och kan läggas till eller tas bort i den slutliga versionen.

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 18 juni 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Åtkomstkontroll](#access-control)
- [Hantering av avancerad datalivscykel](#advanced-data-lifecycle-management)
- [Kontrollpaneler](#dashboards)
- [Dataförvaltning](#data-governance)
- [Mål ](#destinations)
- [Federerad målgruppssammansättning](#fac)
- [Integritetstjänst](#privacy-service)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Källor](#sources)

## Åtkomstkontroll {#access-control}

Experience Platform använder [Adobe Admin Console](https://adminconsole.adobe.com)-produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd olika Experience Platform-funktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera behörighet för instrumentpanelsdata | Alternativen **[!UICONTROL Download CSV]** och **[!UICONTROL Send as email]** på instrumentpaneler kräver nu behörighet **[!UICONTROL Export Dashboard Data]**. Denna behörighet säkerställer att endast behöriga användare kan exportera insiktsdata i tabellform, vilket ger bättre styrning och regler för dataåtkomstkontroll. |

Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Hantering av avancerad datalivscykel {#advanced-data-lifecycle-management}

Experience Platform har en rad funktioner för datahygien som gör att du kan hantera lagrade data genom att ta bort konsumentposter och datauppsättningar programmatiskt. Med hjälp av arbetsytan Data Lifecycle i användargränssnittet eller genom anrop till Data Hygiene API kan du hantera dina datalager på ett effektivt sätt. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

**Ny dokumentation**

| Ny dokumentation | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för radering av post | Nu kan du ta bort enskilda poster baserat på identitetsfält med hjälp av gränssnittet eller API:t. Den här funktionen hjälper till att minska lagring, framtvinga styrning och förbättra datahygien genom att tillåta borttagningar från en enda datauppsättning eller från alla datauppsättningar. Volymbegränsningar och behörighetskrav gäller. |

Mer information finns i [översikt över livscykelhantering för avancerade data](../hygiene/home.md).

## Kontrollpaneler {#dashboards}

Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportalternativ för Skicka som e-post | Du kan nu exportera upp till 10 000 poster från kontrollpaneler i läget Query Pro genom att välja **[!UICONTROL Send as email]** på menyn **[!UICONTROL View more]**. Det här alternativet skickar säkert en nedladdningslänk till ditt Adobe-relaterade e-postmeddelande för större exporter. |

Läs [översikt över kontrollpaneler](../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Dataförvaltning {#data-governance}

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom [!DNL Experience Platform] på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Azure CMK-aviseringar och konfiguration av IP Tillåtelselista | Du kan nu tillåtslista Adobe statiska IP-adress i Azure Key Vault för att säkerställa fortsatt åtkomst när nätverksbegränsningar är aktiverade. Detta förhindrar störningar i plattformstjänsterna på grund av begränsad nyckelåtkomst. |
| Konfigurationsvarningar och -lösningar för CMK | Experience Platform utlöser nu varningsmeddelanden när Adobe-tjänster förlorar åtkomst till ditt Azure Key Vault (till exempel på grund av borttagna IP tillåtelselista-poster eller inaktiverade nycklar). En ny guide hjälper dig att förstå varje varning och vidta korrigerande åtgärder. |

Mer information finns i [översikten över dataförvaltning](../data-governance/home.md).

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer**

| Mål | Beskrivning |
| --- | --- |
| Algoliet-användarsegment | Algoliets mål för användarsegment gör att marknadsförare kan leverera enhetlig personalisering på webbplatser från hemsidan till sökningen. Bygg multimediala målgrupper från flera datakällor och dela dem i olika kanaler för bättre målinriktningsstrategier och kampanjpersonalisering. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Förfalloinformation för LinkedIn-konto | Information om förfallodatum för konto för LinkedIn-mål är nu tillgänglig direkt i [!UICONTROL Browse]- och [!UICONTROL Accounts]-vyerna. Tidigare fanns denna information endast tillgänglig i dokumentationen. Den här förbättringen ger bättre synlighet i LinkedIn-autentiseringsstatus och autentiseringsuppgiftshantering. |
| Google kundmatchning + DV360 allmän tillgänglighet och förbättring | Google kundmatchning + DV360-destinationen är nu tillgänglig för alla Experience Platform-användare. Dokumentationen innehåller nu detaljerad vägledning för kontolänkning mellan Adobe och Google annonskonton. |
| Stöd för målkryptering med DLZ (Data Landing Zone) | Lagt till krypteringsstöd för Data Landing Zone-målet. Nu kan du bifoga RSA-formaterade offentliga nycklar för att lägga till kryptering till dina exporterade filer. |
| Målgruppsövervakning för företagsdestinationer | Övervakning på målgruppsnivå är nu tillgängligt för följande företagsmål: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Federerad målgruppssammansättning {#fac}

Med Federerad målgruppssammansättning kan företag sammanställa data för bättre användning i olika situationer. Med detta nya tillvägagångssätt, som Adobe Real-Time Customer Data Platform- och/eller Adobe Journey Optimizer-användare, kan ni federera datauppsättningar direkt från ert befintliga datalager för att skapa och berika Adobe Experience Platform-målgrupper och attribut i ett och samma system.

| Ny funktion | Beskrivning |
| ----------- | ----------- |
| HIPAA-beredskap | Federated Audience Composition är nu HIPAA-kompatibelt. Mer information om sekretess- och säkerhetsåtgärder för federerad målgruppskomposition finns i [sekretess- och säkerhetsöversikten för Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Mer information om HIPAA-kompatibilitet för Experience Platform-produkter i allmänhet finns i [HIPAA- och Adobe Products and Services-översikt](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Mer information finns i dokumentationen för [Federerad målgruppssammansättning (Federated Audience Composition)](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användare rätt att på begäran få tillgång till eller radera sina personuppgifter från dina datalager. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service] kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-applikationer, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Stöd för Tennessee och Minnesota Privacy Laws | Privacy Service stöder nu Tennessee Information Protection Act (`tipa_tn_usa`) och Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Du kan bearbeta begäranden om åtkomst och borttagning i enlighet med dessa nya regler på statusnivå. Mer information finns i [Regelöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview). |

Mer information om tjänsten finns i [översikten över Privacy Service](../privacy-service/home.md).

## Frågetjänst {#query-service}

Fråga efter data i Adobe Experience Platforms datasjö med hjälp av standard-SQL med Frågetjänst. Kombinera enkelt datauppsättningar och generera nya från frågeresultaten till kraftfull rapportering, möjliggör arbetsflöden för datavetenskap eller underlättar inmatning i kundprofilen i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Avancerade statistiska funktioner | **Theta-skissens skärningspunkt**: Ny funktion för att beräkna uppsättningsskärningar med hjälp av skisser för ungefärliga distinkta räknings- och uppsättningsåtgärder. **KLL-histogram**: Förbättrade histogramfunktioner med KLL-skisser (Kth small, L largest, Large items) för kvantitativ uppskattning och distributionsanalys. Dessa funktioner är tillgängliga för Data Distiller-kunder. |
| SQL-mallbibliotek | Nu finns ett omfattande bibliotek med SQL-mallar för vanliga användningsområden. Den här funktionen snabbar upp frågeutvecklingen genom att tillhandahålla mallar för metodtips för ofta förekommande analysmönster, vilket hjälper Data-Distiller-kunder att implementera komplexa analyser mer effektivt. |

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Exempel på RFM-modellering | Ett omfattande exempel på nyhet, frekvens och monetär modellering (RFM) har lagts till för Data Distiller-kunder. Detta inkluderar detaljerad dokumentation och implementeringsguider för kundsegmentering och värdeanalys med hjälp av RFM-tekniker. |

{style="table-layout:auto"}

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Migrering av uppdateringar av objektkonfiguration | Du kan nu migrera uppdateringar av konfiguration av iterativa objekt mellan sandlådor efter den inledande replikeringen. Den här förbättringen har stöd för utvecklingsarbetsflöden där konfigurationer behöver uppdateras och spridas över olika miljöer utan att hela sandlådekonfigurationen behöver återskapas. |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../sandboxes/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för ny autentiseringstyp för [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] stöder nu även autentisering av tjänstens huvudnamn, utöver den befintliga autentiseringen av anslutningssträngen. |

**Viktiga autentiseringsuppdateringar**

| Uppdatering | Beskrivning |
| --- | --- |
| [!DNL Salesforce] - borttagning av grundläggande autentisering | Grundläggande autentisering för Salesforce CRM och Salesforce Service Cloud kommer att vara inaktuellt i januari 2026. Kunder måste migrera till OAuth 2.0-autentisering för att kunna upprätthålla anslutningen. Den här ändringen påverkar både källanslutningar och säkerställer förbättrad säkerhet och överensstämmelse med Salesforce autentiseringsstandarder. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../sources/home.md).
