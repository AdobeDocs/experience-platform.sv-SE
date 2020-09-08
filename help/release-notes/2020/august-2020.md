---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 10 augusti 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b4ce4c2e5ff5083f663c2daf23c32a1cec32124c
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 12 augusti 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL-mål]](#destinations)
- [[!DNL Customer Data Platform i realtid]](#rtcdp)
- [[!DNL-källor]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från era data. Integrerat i Adobe Experience Platform och [!DNL Data Science Workspace] gör det enklare att förutse hur ni använder ert innehåll och era datatillgångar i olika Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av virtuella maskiner i [!DNL JupyterLab] | Förbättrade stabiliteten hos långvariga virtuella [!DNL JupyterLab notebook] datorer. |

Mer information om [!DNL JupyterLab]finns i [[!DNL JupyterLab] användarhandboken](../../data-science-workspace/jupyterlab/overview.md).

## Mål {#destinations}

I [Adobe kunddataplattform](../../rtcdp/overview.md)i realtid är destinationer färdigbyggda integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| [!DNL Google Customer Match] | Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egendomar, som: [!DNL Search], [!DNL Shopping], Gmail och YouTube. <br><br> På [!DNL Google Customer Match] sidan [](/help/rtcdp/destinations/google-customer-match-destination.md) i målkatalogen finns mer information om destinationen och hur du konfigurerar den i Adobe Real-time CDP. |

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Anpassad filnamnsredigerare | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål där du kan redigera namnet på de exporterade filerna. Mer information finns i [ konfigurationssteget](/help/rtcdp/destinations/activate-destinations.md#configure) i aktiveringsarbetsflödet. |
| Rekommenderade attribut | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål som visar rekommenderade attribut som du kan lägga till i de exporterade filerna. Mer information finns i steget [](/help/rtcdp/destinations/activate-destinations.md#select-attributes) Välj attribut i aktiveringsarbetsflödet. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Adobe Customer Data Platform ([!DNL Real-time CDP]) som bygger på Experience Platform hjälper företag att sammanföra kända och okända data i realtid för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-time CDP] kombinerar flera datakällor för företag för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för IAB TCF 2.0 | [!DNL Real-time CDP] är nu en registrerad leverantör för version 2.0 av [!DNL Transparency & Consent Framework] (TCF), enligt riktlinjerna i [!DNL Interactive Advertising Bureau] (IAB). Du kan konfigurera dataåtgärder och profilscheman så att de accepterar kundmedgivandedata som genereras av en CMP och tillämpa kundernas medgivandeinställningar när du aktiverar segment till underordnade mål. Mer information finns i översikten om stöd för [IAB TCF 2.0 i CDP](../../rtcdp/privacy/iab/overview.md) i realtid. |

Mer information om [!DNL Real-time CDP]finns i [[!DNL Real-time CDP] översikten](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av flödeskörning | Användarna kan övervaka alla flödeskörningar och se en detaljerad vy över varje körning, inklusive slutförandestatus, körvaraktighet, lista över filer som bearbetas, fel och mätvärden. Mer information finns i dokumentet [för övervakning av dataflöden](../../sources/tutorials/ui/monitor.md) . |
| Flödeskörningsmeddelanden | Användare kan prenumerera på händelser och registrera webhooks för att få meddelanden i realtid om status, mått och fel för flödeskörningar. |
| Förbättringar av gränssnittskatalogen | Uppdateringar av källkatalogskärmen för enklare åtkomst till primära åtgärder för markerade objekt. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).