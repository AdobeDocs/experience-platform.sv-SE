---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform november 2020
doc-type: release notes
last-update: November, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: November 2020**

Nya funktioner i Adobe Experience Platform:

- [[!DNL Access control]](#access-control)
- [[!DNL-sandlådor]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] använder [Adobe Admin Console](https://adminconsole.adobe.com) produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Behörigheter | På fliken [!DNL Admin Console]i en [!DNL Platform] produktprofil kan du anpassa vilka [!DNL Platform] funktioner som är tillgängliga för användarna som är kopplade till profilen. Tillgängliga behörighetskategorier är: [!UICONTROL Data Modeling], [!UICONTROL Data Management], [!UICONTROL Profile Management], [!UICONTROL Identities], [!UICONTROL Data Monitoring], [!UICONTROL Sandbox Administration], [!UICONTROL Destinations], [!UICONTROL Sources]. |
| Åtkomst till sandlådor | Fliken **[!UICONTROL Permissions]** i en [!DNL Platform] produktprofil kan ge användare åtkomst till specifika sandlådor. Mer information finns i avsnittet om [sandlådor](#sandboxes) nedan. |

Mer information finns i översikten över [åtkomstkontrollen](../../access-control/home.md).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller sandlådor [!DNL Experience Platform] som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Viktiga funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Produktionssandlåda | [!DNL Experience Platform] innehåller en enda produktionssandlåda som inte kan tas bort eller återställas. |
| Sandlådor utan produktion | Du kan skapa flera icke-produktionssandlådor för en enda [!DNL Platform] instans, så att du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. |
| Sandlådeväxlare | I [!DNL Experience Platform] användargränssnittet gör sandlådeväxlaren i skärmens övre vänstra hörn att du kan växla mellan tillgängliga sandlådor via en nedrullningsbar meny. |
| `x-sandbox-name` header | Alla anrop till [!DNL Experience Platform] API:er måste nu inkludera det nya `x-sandbox-name` `name` huvudet, vars värde refererar till attributet för den sandlåda som åtgärden ska utföras i. |

Mer information finns i Översikt över [sandlådor](../../sandboxes/home.md).