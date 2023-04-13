---
title: Versionsinformation om Adobe Experience Platform, februari 2021
description: Versionsinformation från februari 2021 för Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 februari 2021**

Nya funktioner i Adobe Experience Platform:

- [(Beta) Kontrollpaneler](#dashboards)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera kontrollpaneler där du kan visa viktig information om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Profiler, segment, destinationer och kontrollpaneler för licensanvändning (beta) | **Obs! Instrumentpanelsfunktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.**<br/><br/> Instrumentpaneler ger användningsklara rapporter om organisationens data och är inbyggda direkt i marknadsföringsarbetsflödet inom Platform. Dessa instrumentpaneler är tillgängliga utan behov av ytterligare IT-support eller den tid och ansträngning som annars skulle behövas för att exportera och bearbeta data med ytterligare design och implementering av datalagerhantering. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| JupyterLab EDA-anteckningsbok | Den experimentella dataanalysen (EDA) Python-anteckningsboken finns nu tillgänglig i Jupyterlab. Den här bärbara datorn är utformad för att hjälpa dig att upptäcka datamönster, kontrollera datavården och sammanfatta relevanta data för prediktiva modeller. Se självstudiekursen om [utforska webbaserade data för prediktiva modeller](../../data-science-workspace/jupyterlab/eda-notebook.md) för mer information. |

Mer allmän information om arbetsytan Datavetenskap finns i [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

I Adobe Experience Platform hämtas data från en mängd olika källor, som analyseras i Experience Platform och aktiveras till en mängd olika destinationer. Plattformen gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av [!DNL Identity Service] och [!DNL Real-Time Customer Profile] innan den aktiveras [!DNL Destinations].

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny kontrollpanel | Nu kan du använda kontrollpanelen för genomskinlighet mellan tjänster och åtgärdbara insikter för källdatainhämtning. Den nya kontrollpanelen ger en heltäckande bild av data som bearbetats från [!DNL Data Lake] till [!DNL Identity Service] och till [!DNL Profile], samtidigt som du kan övervaka hur många gånger du har fått tag på produkten, hur många gånger det har gått och hur många fel som har uppstått. Se självstudiekursen om [övervaka källdataflöden i användargränssnittet](../../dataflows/ui/monitor-sources.md) för mer information. |

Mer allmän information om dataflöden finns i [dataflödesöversikt](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | The [!DNL LinkedIn Matched Audiences] kan du aktivera målgrupper i [!DNL LinkedIn] social plattform. |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppgraderat sökgränssnitt | Förbättrade sökfunktioner finns nu i [!UICONTROL Browse] i [!UICONTROL Schemas] arbetsytan och dialogrutan för val av schemafältgrupp i [!DNL Schema Editor].<br><br>När du söker efter en term tidigare innehåller resultatet bara XDM-resurser vars namn matchar sökfrågan. Förutom resurser vars namn matchar frågan kommer resurser som innehåller enskilda attribut som matchar termen att tas med. På så sätt kan du söka efter XDM-resurser baserat på de attribut de innehåller i stället för efter resursnamn.<br><br>Se dokumenten på [utforska XDM-resurser](../../xdm/ui/explore.md) och [hantera scheman](../../xdm/ui/resources/schemas.md) i användargränssnittet om du vill ha mer information. |

Mer allmän information om XDM finns i [XDM - systemöversikt](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Identitetsdiagramvisningsprogram | Med identitetsdiagramvisningsprogrammet kan du validera och visualisera identiteter som sammanfogats i användargränssnittet, vilket ger förbättrad felsökning och genomskinlighet. Se [dokument för identitetsdiagramvisningsprogram](../../identity-service/ui/identity-graph-viewer.md) för mer information. |

Mer allmän information om [!DNL Identity Service], se [Översikt över identitetstjänsten](../../identity-service/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] gör att ni kan sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Beräknade attribut (alfa) | ***Obs! Den här funktionen är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.*** <br/><br/>Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Sedan kan ni använda aggregaten för segmentering, aktivering och personalisering. Exempel på sådana funktioner är count, sum, Average, min, max, true/false. Beräknade attribut är för närvarande bara tillgängliga via API. |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data, kan du börja med att läsa [Översikt över kundprofiler i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Google PubSub] | Nu kan du ansluta [!DNL Google PubSub] till [!DNL Experience Platform] med [!DNL Flow Service] API eller gränssnittet. Se [[!DNL Google PubSub] anslutningsöversikt](../../sources/connectors/cloud-storage/google-pubsub.md) för mer information. |
| [!DNL Oracle Object Storage] | Nu kan du ansluta [!DNL Oracle Object Storage] till [!DNL Experience Platform] med [!DNL Flow Service] API eller gränssnittet. Se [[!DNL Oracle Object Storage] anslutningsöversikt](../../sources/connectors/cloud-storage/oracle-object-storage.md) för mer information. |

Mer allmän information om källor finns i [källöversikt](../../sources/home.md).
