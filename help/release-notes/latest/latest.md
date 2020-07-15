---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Experience Platform
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 1e420d26f89150999f356f9cf5af94d434076c2b
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 15 juli 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

<!-- - [Data Governance](#governance) -->
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

<!-- ## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature    | Description  |
| -----------| ---------- |
| Automatic policy enforcement in [!DNL Real-time Customer Data Platform] | Data usage policies are now automatically enforced in [!DNL Real-time CDP] when violating actions occur, including activating segments to destinations. When a policy violation is triggered, users get real-time visibility into usage restrictions within the activation workflow, indicating what data they cannot use and why.<br><br>See the section on [enforcing data usage compliance](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) within the overview on [!DNL Data Governance] in [!DNL Real-time CDP] for more information. |
| Adobe Audience Manager integration | Any segments that are shared with [!DNL Audience Manager] from [!DNL Platform] inherit any applied data usage labels as [!DNL Data Export Controls], and vice versa. See the [!DNL Audience Manager] documentation for specific [mappings between usage labels and Data Export Controls](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Custom data usage labels | You can now create custom data usage labels using the Policy Service API or in the UI. See the [labels overview](../../data-governance/labels/overview.md) for more information. |

See the [Data Governance overview](../../data-governance/home.md) for more information on the service.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] allows you to consolidate your disparate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

**New features**

| Feature | Description |
| ------- | ----------- |
| Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Profile] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | 

-->

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment konfigureras och underhålls centralt [!DNL Platform]så att de är tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Direktuppspelningssegmentering | Strömmande segmentering kan nu kvalificera sig som en användare i ett segment när data når [!DNL Platform]och därmed dramatiskt minska tiden för godkännande av segment. Direktuppspelningssegmentering eliminerar också behovet av att köra segmenteringsjobb manuellt. |

<!-- | Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Segments] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | -->

Mer information om [!DNL Segmentation Service]segmentering finns i [segmenteringsöversikten](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, programvara från tredje part och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för borttagning av dataflöden | Dataflöden som har gjorts med fel eller blivit onödiga kan nu tas bort via API:er eller med användargränssnittet. |
| API- och gränssnittsstöd för engångsbruk | Engångsinmatning för dataflöden, där endast startdatumet anges och inget framtida intag är schemalagt, kan nu utföras via API:er eller med användargränssnittet. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
