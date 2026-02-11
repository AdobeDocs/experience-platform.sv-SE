---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 695b8486211c2fee03bc29243d65d5bbf6d561db
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 36%

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

**Releasedatum: februari 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Aviseringar](#alerts)
- [Datainsamling](#data-collection)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## Agent Orchestrator {#agent-orchestrator}

Med Agent Orchestrator kan ni bygga och driftsätta AI-baserade agenter som kan automatisera arbetsflöden och interagera med kunder över flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Dataintroduktionsagent | Använd Data Onboarding Agent för att konfigurera källanslutningar, validera datakvaliteten, tillämpa semantisk anrikning, granska och validera scheman och köra datainhämtning. Följ stegvisa arbetsflöden för både B2C- och B2B-flöden, granska förväntade utdata och felsöka vanliga problem. |
| Data Distiller Agent | Använd Data Distiller Agent för att skapa SQL-jobb av naturligt språk, optimera SQL-prestanda, återställa efter SQL-fel, schemalägga och hantera SQL-jobb samt övervaka jobbstatus. Granska säkerhetsutkast, nödvändiga behörigheter och felsökningsanvisningar för att komma igång. |
| Datainsamlingsagent | Använd agenten för datainsamling för att få kontextuell vägledning för komplexa datainsamlingskonfigurationer och för att utforska utbud, beroenden och relationer mellan datainsamlingsobjekten genom konversationsinsikter. |

{style="table-layout:auto"}

Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Integrering av [!DNL Slack] för kundtillvända aviseringar | Du kan nu leverera kundorienterade aviseringar till [!DNL Slack]. Följ den stegvisa självstudiekursen för att konfigurera [!DNL Slack]-integreringen och ta emot varningsmeddelanden direkt på arbetsytan i [!DNL Slack]. |

{style="table-layout:auto"}

Mer information finns i [[!DNL Observability Insights] översikten](../observability/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform Data Collection innehåller en uppsättning tekniker som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network och andra destinationer.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tilläggshantering för Adobe-plattformstaggar | Använd den nya funktionen för Extension Management för att ladda upp, paketera och frisläppa organisationens tillägg till utveckling, privat och offentlig distribution. Hitta delade privata tillägg tillsammans med egna tillägg i den översta företagsvyn. Den här funktionen har stöd för webbtillägg, edge-tillägg och mobiltillägg. |

{style="table-layout:auto"}

Mer information finns i [dokumentationen för datainsamling](https://experienceleague.adobe.com/sv/docs/experience-platform/collection/home).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| Kontomål för [!DNL ZoomInfo] | B2B CDP-användare kan nu aktivera kontonivådata till [!DNL ZoomInfo] via den nya målkopplingen för [!DNL ZoomInfo]-kontot. Konfigurera anslutningen för att börja skicka dina kontomålgrupper till [!DNL ZoomInfo]. |
| [!DNL Snowflake] grupp är allmänt tillgänglig | Batchmålet [!DNL Snowflake] har flyttats till allmän tillgänglighet. Nu kan du visa kolumnen med sammanfogningspolicy-ID i dina exporterade data tillsammans med befintliga kolumner som tidsstämpel, mappningsattribut och målgruppsmedlemskap. |
| Stöd för AES256-kryptering för [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) -mål | Nu kan du konfigurera AES256-kryptering för dina Amazon S3-exporter. Välj mellan två alternativ: <ul><li>**[!UICONTROL Default]**: Experience Platform krypterar vilande data med den standardkrypteringsalgoritm som är inställd på bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform lägger till rubriken `s3:x-amz-server-side-encryption": "AES256` i exporten och krypterar vilande data med AES256-algoritmen när den körs i S3. **Det här alternativet har högre prioritet än någon standardkrypteringsalgoritm som du konfigurerar på din S3-bucket**.</li></ul> |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Schemalagerorganisation och sökning | Bläddringssidan för scheman innehåller nu förbättrad sökning och filtrering, infogade åtgärder och stöd för användardefinierade taggar och mappar. Dessa uppdateringar gör det enklare att hitta, ordna och hantera scheman över sandlådor samtidigt som manuell navigering och underhåll minskar. |

Mer information finns i [[!DNL XDM] översikten](../xdm/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Data Distiller Annual compute reset date alignment (Limited Release) | Distiller årliga beräkningstimmar återställs nu på årsdatumet för ditt Data Distiller-kontrakt, baserat på när licensen köptes eller förnyades. Detta justerar licensanvändningsrapporteringen efter avtalsvillkoren och kan resultera i en engångsjustering till aktuella användningsvärden. |
| Data Distiller session management (Limited Release) | Som behörig administratör kan du visa och hantera aktiva Query Service- och Data Distiller-sessioner i din organisation och sandlåda via användargränssnittet. Använd sessionshantering för att identifiera inaktiva sessioner och avsluta dem för att frigöra kapacitet. Inbyggda säkerhetsfunktioner förhindrar att du avbryter sessioner med aktiva frågor. Funktionen loggar alla avlägsnandeåtgärder för revision och meddelar berörda användare. Du behöver behörigheten **Hantera frågesessioner** för att komma åt den här funktionen. |

{style="table-layout:auto"}

Mer information finns i [Översikt över frågetjänsten](../query-service/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| Stöd för Unity Catalog i [!DNL Databricks]-källanslutning | Källkopplingen [!DNL Databricks] har nu stöd för Unity Catalog. Läs den uppdaterade [[!DNL Databricks]](../sources/connectors/databases/databricks.md)-dokumentationen och lär dig hur du använder Unity Catalog när du konfigurerar källanslutningen. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../sources/home.md).
