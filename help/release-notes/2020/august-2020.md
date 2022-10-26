---
title: Versionsinformation om Adobe Experience Platform, augusti 2020
description: Versionsinformation från augusti 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 4%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 12 augusti 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från era data. Integrerat i Adobe Experience Platform, [!DNL Data Science Workspace] hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över olika Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av virtuella maskiner i [!DNL JupyterLab] | Förbättrad stabilitet för långvarig körning [!DNL JupyterLab notebook] virtuella datorer. |

Mer information om [!DNL JupyterLab], se [[!DNL JupyterLab] användarhandbok](../../data-science-workspace/jupyterlab/overview.md).

## Mål  {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| [!DNL Google Customer Match] | Med Google Customer Match kan ni använda era online- och offlinedata för att nå ut till och återengagera era kunder via Google egna och driftsatta egendomar, som: [!DNL Search], [!DNL Shopping], Gmail och YouTube. <br><br> Besök [!DNL Google Customer Match] [page](../../destinations/catalog/advertising/google-customer-match.md) i målkatalogen om du vill ha mer information om destinationen och hur du konfigurerar den i Real-Time CDP. |

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Anpassad filnamnsredigerare | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål där du kan redigera namnet på de exporterade filerna. Mer information finns i [ Konfigurera steg](../../destinations/ui/activate-batch-profile-destinations.md) i aktiveringsarbetsflödet. |
| Rekommenderade attribut | Uppdatera till arbetsflödet för dataaktivering för e-postmarknadsföringsmål och molnlagringsmål som visar rekommenderade attribut som du kan lägga till i de exporterade filerna. Mer information finns i [Välj attributsteg](../../destinations/ui/activate-batch-profile-destinations.md) i aktiveringsarbetsflödet. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Built on Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor för företag för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för IAB TCF 2.0 | [!DNL Real-Time CDP] är nu en registrerad leverantör för version 2.0 av [!DNL Transparency & Consent Framework] (TCF), enligt riktlinjerna i [!DNL Interactive Advertising Bureau] (IAB). Du kan konfigurera dataåtgärder och profilscheman så att de accepterar kundmedgivandedata som genereras av en CMP och tillämpa kundernas medgivandeinställningar när du aktiverar segment till underordnade mål. |

Mer information om [!DNL Real-Time CDP], se [[!DNL Real-Time CDP] översikt](../../rtcdp/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av flödeskörning | Användarna kan övervaka alla flödeskörningar och se en detaljerad vy över varje körning, inklusive slutförandestatus, körvaraktighet, lista över filer som bearbetas, fel och mätvärden. Se [övervaka dataflöden](../../sources/tutorials/ui/monitor.md) för mer information. |
| Flödeskörningsmeddelanden | Användare kan prenumerera på händelser och registrera webhooks för att få meddelanden i realtid om status, mått och fel för flödeskörningar. |
| Förbättringar av gränssnittskatalogen | Uppdateringar av källkatalogskärmen för enklare åtkomst till primära åtgärder för markerade objekt. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
