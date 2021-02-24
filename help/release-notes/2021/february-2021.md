---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform för 24 februari 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7142d13b144f34d92087affe101c5ccfcb52d90e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 februari 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| JupyterLab EDA-anteckningsbok | Den experimentella dataanalysen (EDA) Python-anteckningsboken finns nu tillgänglig i Jupyterlab. Den här bärbara datorn är utformad för att hjälpa dig att upptäcka datamönster, kontrollera datavården och sammanfatta relevanta data för prediktiva modeller. Se självstudiekursen [utforska webbaserade data för prediktiva modeller](../../data-science-workspace/jupyterlab/eda-notebook.md) för mer information. |

Mer allmän information om arbetsytan Datavetenskap finns i [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

I Adobe Experience Platform hämtas data från en mängd olika källor, som analyseras i Experience Platform och aktiveras till en mängd olika destinationer. Plattformen gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av [!DNL Identity Service] och [!DNL Real-time Customer Profile] innan de aktiveras till [!DNL Destinations].

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny kontrollpanel | Nu kan du använda kontrollpanelen för genomskinlighet mellan tjänster och åtgärdbara insikter för källdatainhämtning. Den nya kontrollpanelen ger en heltäckande bild av data som bearbetats från [!DNL Data Lake] till [!DNL Identity Service] och till [!DNL Profile], samtidigt som du kan övervaka hur många gånger du har fått tag på dem, hur många gånger de har lyckats och misslyckats. Mer information finns i självstudiekursen om [övervakning av källdataflöden i användargränssnittet](../../dataflows/ui/monitor-sources.md). |

Mer allmän information om dataflöden finns i [översikten över dataflöden](../../dataflows/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppgraderat sökgränssnitt | Förbättrade sökfunktioner finns nu på fliken [!UICONTROL Browse] på arbetsytan [!UICONTROL Schemas] och i dialogrutan för mixin-val i [!DNL Schema Editor].<br><br>När du söker efter en term tidigare innehåller resultatet bara XDM-resurser vars namn matchar sökfrågan. Förutom resurser vars namn matchar frågan kommer resurser som innehåller enskilda attribut som matchar termen att tas med. På så sätt kan du söka efter XDM-resurser baserat på de attribut de innehåller i stället för efter resursnamn.<br><br>Mer information finns i dokumenten om  [att utforska XDM-resurser ](../../xdm/ui/explore.md) och  [hantera ](../../xdm/ui/resources/schemas.md) scheman i användargränssnittet. |

Mer allmän information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Identitetsdiagramvisningsprogram | Med identitetsdiagramvisningsprogrammet kan du validera och visualisera identiteter som sammanfogats i användargränssnittet, vilket ger förbättrad felsökning och genomskinlighet. Mer information finns i [identitetsdiagramvisningsdokumentet](../../identity-service/ui/identity-graph-viewer.md). |

Mer allmän information om [!DNL Identity Service] finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Google PubSub] | Nu kan du ansluta [!DNL Google PubSub] till [!DNL Experience Platform] med hjälp av API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i [[!DNL Google PubSub] anslutningsöversikten](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Nu kan du ansluta [!DNL Oracle Object Storage] till [!DNL Experience Platform] med hjälp av API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i [[!DNL Oracle Object Storage] anslutningsöversikten](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Mer allmän information om källor finns i [Källor översikt](../../sources/home.md).
