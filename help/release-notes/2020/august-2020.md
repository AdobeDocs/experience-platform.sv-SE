---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 10 augusti 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 12 augusti 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från era data. [!DNL Data Science Workspace] är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med ert innehåll och era dataresurser över alla Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av virtuella datorer i [!DNL JupyterLab] | Förbättrade stabiliteten hos de virtuella datorerna med [!DNL JupyterLab notebook] som körs länge. |

Mer information om [!DNL JupyterLab] finns i [[!DNL JupyterLab] användarhandboken](../../data-science-workspace/jupyterlab/overview.md).

## Mål {#destinations}

I [Kunddataplattform för realtid](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| [!DNL Google Customer Match] | Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Googles egna och styrda egendomar, som: [!DNL Search], [!DNL Shopping], Gmail och YouTube. <br><br> På  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) sidan i målkatalogen finns mer information om destinationen och hur du konfigurerar den i CDP i realtid. |

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Anpassad filnamnsredigerare | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål där du kan redigera namnet på de exporterade filerna. Mer information finns i [ Konfigurera steg](../../destinations/ui/activate-destinations.md#configure) i aktiveringsarbetsflödet. |
| Rekommenderade attribut | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål som visar rekommenderade attribut som du kan lägga till i de exporterade filerna. Mer information finns i [Välj attribut-steget](../../destinations/ui/activate-destinations.md#select-attributes) i aktiveringsarbetsflödet. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Kunddataplattformen i realtid ([!DNL Real-time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-time CDP] kombinerar flera datakällor för företag för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för IAB TCF 2.0 | [!DNL Real-time CDP] är nu en registrerad leverantör för version 2.0 av  [!DNL Transparency & Consent Framework] (TCF) enligt riktlinjerna  [!DNL Interactive Advertising Bureau] (IAB). Du kan konfigurera dataåtgärder och profilscheman så att de accepterar kundmedgivandedata som genereras av en CMP och tillämpa kundernas medgivandeinställningar när du aktiverar segment till underordnade mål. |

Mer information om [!DNL Real-time CDP] finns i [[!DNL Real-time CDP] översikten](../../rtcdp/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av flödeskörning | Användarna kan övervaka alla flödeskörningar och se en detaljerad vy över varje körning, inklusive slutförandestatus, körvaraktighet, lista över filer som bearbetas, fel och mätvärden. Mer information finns i [dokumentet för övervakning av dataflöden](../../sources/tutorials/ui/monitor.md). |
| Flödeskörningsmeddelanden | Användare kan prenumerera på händelser och registrera webhooks för att få meddelanden i realtid om status, mått och fel för flödeskörningar. |
| Förbättringar av gränssnittskatalogen | Uppdateringar av källkatalogskärmen för enklare åtkomst till primära åtgärder för markerade objekt. |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).