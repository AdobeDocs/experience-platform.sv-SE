---
title: Versionsinformation om Adobe Experience Platform – februari 2021
description: Versionsinformationen för Adobe Experience Platform från februari 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 20%

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
| Profiler, segment, destinationer och kontrollpaneler för licensanvändning (Beta) | **Obs! Instrumentpanelsfunktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.**<br/><br/> Instrumentpaneler ger körklara rapporter om organisationens data och är inbyggda direkt i marknadsföringsarbetsflödet i Experience Platform. Dessa instrumentpaneler är tillgängliga utan behov av ytterligare IT-support eller den tid och ansträngning som annars skulle behövas för att exportera och bearbeta data med ytterligare design och implementering av datalagerhantering. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era datatillgångar i alla Adobe lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| JupyterLab EDA Notebook | Den experimentella dataanalysen (EDA) Python-anteckningsboken finns nu tillgänglig i Jupyterlab. Den här bärbara datorn är utformad för att hjälpa dig att upptäcka datamönster, kontrollera datavården och sammanfatta relevanta data för prediktiva modeller. Mer information finns i självstudiekursen [Utforska webbaserade data för prediktiva modeller](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Mer allmän information om Data Science Workspace finns i [Data Science Workspace overview](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

I Adobe Experience Platform hämtas data från en mängd olika källor, analyserade inom Experience Platform, och aktiverades för en mängd olika destinationer. Experience Platform gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av datajobb som flyttar data mellan Experience Platform. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av [!DNL Identity Service] och [!DNL Real-Time Customer Profile] innan de aktiveras till [!DNL Destinations].

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny kontrollpanel | Nu kan du använda kontrollpanelen för genomskinlighet mellan tjänster och åtgärdbara insikter för källdatainhämtning. Den nya kontrollpanelen ger en heltäckande vy över data som bearbetats från [!DNL Data Lake] till [!DNL Identity Service] och till [!DNL Profile], samtidigt som du kan övervaka hur många gånger användarna har fått, lyckats och misslyckats. Mer information finns i självstudiekursen [Övervaka källdataflöden i användargränssnittet](../../dataflows/ui/monitor-sources.md). |

Mer allmän information om dataflöden finns i [dataflödesöversikten](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | Med anslutningen [!DNL LinkedIn Matched Audiences] kan du aktivera målgrupper på den sociala plattformen [!DNL LinkedIn]. |

För mer allmän information om mål, se [översikt över mål](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppgraderat sökgränssnitt | Förbättrade sökfunktioner är nu tillgängliga på fliken [!UICONTROL Browse] på arbetsytan [!UICONTROL Schemas] och i dialogrutan för val av schemafältgrupp i [!DNL Schema Editor].<br><br>När du söker efter en term tidigare innehåller resultaten bara XDM-resurser vars namn matchar sökfrågan. Förutom resurser vars namn matchar frågan kommer resurser som innehåller enskilda attribut som matchar termen att tas med. På så sätt kan du söka efter XDM-resurser baserat på de attribut de innehåller i stället för efter resursnamn.<br><br>Mer information finns i dokumenten om att [utforska XDM-resurser](../../xdm/ui/explore.md) och [hantera scheman](../../xdm/ui/resources/schemas.md) i användargränssnittet. |

Mer allmän information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper dig att få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Identitetsdiagramvisningsprogram | Med identitetsdiagramvisningsprogrammet kan du validera och visualisera identiteter som sammanfogats i användargränssnittet, vilket ger förbättrad felsökning och genomskinlighet. Mer information finns i [identitetsdiagramvisningsdokumentet](../../identity-service/features/identity-graph-viewer.md). |

Mer allmän information om [!DNL Identity Service] finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med [!DNL Profile] kan du konsolidera kunddata i en enhetlig vy med ett åtgärdbart, tidsstämplat konto för varje kundinteraktion.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Beräknade attribut (Alpha) | ***Obs! Den här funktionen är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.*** <br/><br/>Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Sedan kan ni använda aggregaten för segmentering, aktivering och personalisering. Exempel på sådana funktioner är count, sum, Average, min, max, true/false. Beräknade attribut är för närvarande bara tillgängliga via API. |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa praxis för att arbeta med [!DNL Profile]-data, får du genom att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Google PubSub] | Du kan nu ansluta [!DNL Google PubSub] till [!DNL Experience Platform] med API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i [[!DNL Google PubSub] anslutningsöversikten](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Du kan nu ansluta [!DNL Oracle Object Storage] till [!DNL Experience Platform] med API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i [[!DNL Oracle Object Storage] anslutningsöversikten](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Mer allmän information om källor finns i [Källöversikt](../../sources/home.md).
