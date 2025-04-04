---
title: Versionsinformation om Adobe Experience Platform från augusti 2020
description: Versionsinformation för augusti 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 22%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 12 augusti 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att frigöra insikter från dina data. [!DNL Data Science Workspace] är integrerat i Adobe Experience Platform och hjälper dig att göra förutsägelser med ditt innehåll och dina dataresurser över alla Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| VM-förbättringar i [!DNL JupyterLab] | Förbättrade stabiliteten för de [!DNL JupyterLab notebook] virtuella datorerna som körs länge. |

Mer information om [!DNL JupyterLab] finns i [[!DNL JupyterLab] användarhandboken](../../data-science-workspace/jupyterlab/overview.md).

## Mål {#destinations}

I [Real-Time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

**Nya mål**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Mål | Beskrivning |
|--- | ---|
| [!DNL Google Customer Match] | Med Google Customer Match kan du använda dina online- och offlinedata för att nå och återengagera dina kunder i olika egenskaper som ägs och hanteras av Google, till exempel: [!DNL Search], [!DNL Shopping], Gmail och YouTube. <br><br> Gå till [!DNL Google Customer Match] [sidan ](../../destinations/catalog/advertising/google-customer-match.md) i målkatalogen om du vill ha mer information om målet och hur du konfigurerar det i Real-Time CDP. |

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Anpassad filnamnsredigerare | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål där du kan redigera namnet på de exporterade filerna. Mer information finns i [konfigurationssteget](../../destinations/ui/activate-batch-profile-destinations.md) i aktiveringsarbetsflödet. |
| Rekommenderade attribut | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål som visar rekommenderade attribut som du kan lägga till i de exporterade filerna. Mer information finns i [Välj attribut-steget](../../destinations/ui/activate-batch-profile-destinations.md) i aktiveringsarbetsflödet. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Plattformen för kunddata i realtid ([!DNL Real-Time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligenta beslut under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor från företag för att skapa kundprofiler i realtid. Segment som byggs upp utifrån dessa profiler kan sedan skickas till mål i senare led för att ge personliga kundupplevelser i alla kanaler och på alla enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för IAB TCF 2.0 | [!DNL Real-Time CDP] är nu en registrerad leverantör för version 2.0 av [!DNL Transparency & Consent Framework] (TCF), enligt riktlinjerna från IAB ([!DNL Interactive Advertising Bureau]). Du kan konfigurera dataåtgärder och profilscheman så att de accepterar kundmedgivandedata som genereras av en CMP och tillämpa kundernas medgivandeinställningar när du aktiverar segment till underordnade mål. |

Mer information om [!DNL Real-Time CDP] finns i [[!DNL Real-Time CDP] översikten](../../rtcdp/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av flödeskörning | Användarna kan övervaka alla flödeskörningar och se en detaljerad vy över varje körning, inklusive slutförandestatus, körvaraktighet, lista över filer som bearbetas, fel och mätvärden. Mer information finns i dokumentet [Övervaka dataflöden](../../sources/tutorials/ui/monitor.md). |
| Flödeskörningsmeddelanden | Användare kan prenumerera på händelser och registrera webhooks för att få meddelanden i realtid om status, mått och fel för flödeskörningar. |
| Förbättringar av gränssnittskatalogen | Uppdateringar av källkatalogskärmen för enklare åtkomst till primära åtgärder för markerade objekt. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
