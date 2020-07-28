---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Experience Platform
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 15 juli 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datastyrning](#governance)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Automatisk policytillämpning i [!DNL Real-time Customer Data Platform] | Dataanvändningspolicyer används nu automatiskt i [!DNL Real-time CDP] när åtgärder överträds, inklusive aktivering av segment till mål. När en principöverträdelse utlöses får användarna synlighet i realtid i användningsbegränsningarna i aktiveringsarbetsflödet, vilket anger vilka data de inte kan använda och varför.<br><br>Mer information finns i avsnittet om hur du [kontrollerar efterlevnad](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) av dataanvändning i översikten [!DNL Data Governance] i [!DNL Real-time CDP] . |
| Integrering med Adobe Audience Manager | Alla segment som delas med [!DNL Audience Manager] från [!DNL Platform] ärver tillämpade dataanvändningsetiketter som [!DNL Data Export Controls]och vice versa. Se [!DNL Audience Manager] dokumentationen för specifika [mappningar mellan användningsetiketter och dataexportkontroller](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Anpassade etiketter för dataanvändning | Nu kan du skapa anpassade etiketter för dataanvändning med hjälp av principtjänstens API eller i användargränssnittet. Mer information finns i översikten över [](../../data-governance/labels/overview.md) etiketter. |

Mer information om tjänsten finns i översikten över [](../../data-governance/home.md) datastyrning.

## [!DNL Real-time Customer Profile] {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]det kan ni få en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Tillämpning av policyer för dataanvändning | I [!DNL Real-time Customer Data Platform]så fall uppstår automatiskt överträdelser av dataanvändningsprinciper när en överträdelse görs i arbetsytan. [!UICONTROL Profile] . Mer information om automatisk policytillämpning finns i [versionsinformationen om datastyrning](#governance) . |

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment konfigureras och underhålls centralt [!DNL Platform]så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Direktuppspelningssegmentering | Strömmande segmentering kan nu kvalificera sig som en användare i ett segment när data når [!DNL Platform]och därmed dramatiskt minska tiden för godkännande av segment. Direktuppspelningssegmentering eliminerar också behovet av att köra segmenteringsjobb manuellt. |
| Tillämpning av policyer för dataanvändning | I [!DNL Real-time Customer Data Platform]så fall uppstår automatiskt överträdelser av dataanvändningsprinciper när en överträdelse görs i arbetsytan. [!UICONTROL Segments] . Mer information om automatisk policytillämpning finns i [versionsinformationen om datastyrning](#governance) . |

Mer information om [!DNL Segmentation Service]segmentering finns i [segmenteringsöversikten](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Gränssnittsstöd för borttagning av dataflöden | Dataflöden som har gjorts med fel eller blivit onödiga kan nu tas bort via användargränssnittet. |
| API- och gränssnittsstöd för engångsbruk | Engångsinmatning för dataflöden, där endast startdatumet anges och inget framtida intag är schemalagt, kan nu utföras via API:er eller med användargränssnittet. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
