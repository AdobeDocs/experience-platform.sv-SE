---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 10 augusti 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 89531ad458bd41720090ef2c429376af4460d7c0
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 12 augusti 2020**

Den senaste versionsinformationen för Experience Platform

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL-källor]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från era data. Integrerat i Adobe Experience Platform och [!DNL Data Science Workspace] gör det enklare att förutse hur ni använder ert innehåll och era datatillgångar i olika Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av virtuella maskiner i [!DNL JupyterLab] | Förbättrade stabiliteten hos långvariga virtuella [!DNL JupyterLab notebook] datorer. |

Mer information om [!DNL JupyterLab]finns i [[!DNL JupyterLab] användarhandboken](../../data-science-workspace/jupyterlab/overview.md).

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av flödeskörning | Användarna kan övervaka alla flödeskörningar och se en detaljerad vy över varje körning, inklusive slutförandestatus, körvaraktighet, lista över filer som bearbetas, fel och mätvärden. Mer information finns i dokumentet [för övervakning av dataflöden](../../sources/tutorials/ui/monitor.md) . |
| Kontouppdatering | Användarna kan uppdatera inloggningsuppgifter, namn och beskrivning för alla befintliga konton för att ge mer meningsfull information och åtgärda eventuella fel som kan ha uppstått. |
| Flödeskörningsmeddelanden | Användare kan prenumerera på händelser och registrera webhooks för att få meddelanden i realtid om status, mått och fel för flödeskörningar. |
| Förbättringar av gränssnittskatalogen | Uppdateringar av källkatalogskärmen för enklare åtkomst till primära åtgärder för markerade objekt. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
