---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 11 december 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Versionsinformation om Adobe Experience Platform

**Releasedatum: 11 december 2019**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [Segmenteringstjänst](#segmentation)
* [Beslutstjänst](#decisioning)
* [Källor](#sources)
* [Experience Data Model (XDM) System](#xdm)

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform Segmentation Service tillhandahåller ett användargränssnitt och RESTful API som gör att ni kan skapa segment och generera målgrupper utifrån era kundprofildata i realtid. Dessa segment är centralt konfigurerade och underhållna på Platform, vilket gör dem tillgängliga för alla Adobe-program.

Segmenteringstjänsten definierar en viss delmängd av profiler genom att beskriva de kriterier som särskiljer en marknadsföringsbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Fliken Sammanfogade målgrupper i Segment Builder | Flikarna _Segment_ och _Publiker_ i Segment Builder har kombinerats till en enda flik för _Publiker_ . På den här fliken kan du bläddra och söka efter befintliga målgrupper, som du sedan kan dra och släppa på arbetsytan i regelbyggaren för att skapa en ny segmentdefinition. Referenser till en målgrupp kan lägga till en av följande uppsättningar regellogik i den nya segmentdefinitionen: Målgruppsmedlemskap som regel, den fullständiga uppsättningen regellogik som definierar den refererade målgruppen. |
| Ny plats för kopplingsprincipväljaren | Platsen för sammanslagningsprincipväljaren i segmentbyggaren har ändrats. Om du vill välja en sammanfogningsprincip för en segmentdefinition klickar du på kugghjulsikonen på fliken _Fält_ och använder sedan listrutan _Sammanfogningsprincip_ för att välja den sammanfogningsprincip som du vill använda. |

**Kända fel**

* Ingen

Mer information finns i Översikt över [segmenteringstjänsten](../../segmentation/home.md).

## Beslutstjänst {#decisioning}

Med Adobe Experience Platform Decisioning Service kan man programmatiskt och intelligent välja&quot;Nästa bästa upplevelse&quot; bland en uppsättning tillgängliga alternativ för en viss individ, leverera dem till valfri kanal eller tillämpning samt utföra rapportering och analys.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Rankningsfunktioner | Erbjudandeordningen för profiler hämtas nu via en rangordningsfunktion, i stället för en fast uppsättning erbjudanden för alla profiler. |

**Kända fel**

* Ingen.

En fullständig introduktion till tjänsten finns i översikten över [](../../decisioning-service/home.md) beslutstjänsten.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dig mot dina lagringssystem och CRM-tjänster, ange tider för hur mycket information som ska matas in och hantera dataöverföringshastigheten.

**Nya funktioner**

| Funktion | Beskrivning |
| ---------- | ------------ |
| Strömmande anslutning | Med direktuppspelning kan ni skicka data från klient- och serverenheter till Experience Platform i realtid. Versionen innehåller ett nytt användargränssnitt för direktuppspelad anslutning. |
| Anslutningsstöd för Google Cloud Store | Stöd för datainsamling från Google Cloud Store. |

**Kända fel**

* Ingen.

Mer information om källor finns i [Källöversikt](../../sources/home.md).

## Experience Data Model (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Förbättrad schemavalidering | Nya kontroller för att se till att referenser tolkas i ytterligare fält som förväntat. Ytterligare kontroller har lagts till i fält som definierats som en array med objekt för att säkerställa att objekten är helt definierade. Förbättrade felmeddelanden som hjälper till att identifiera och åtgärda problem. |

**Felkorrigeringar**

* Underhåll och förbättringar relaterade till åtkomstkontroll och sandlådor.
* Stöd `eTag` för `/descriptors` slutpunkten i API:t för schemaregistret.

**Kända fel**

* Ingen

Mer information om hur du arbetar med XDM med API:t för schemaregister och användargränssnittet för Schemaredigeraren finns i [XDM-systemdokumentationen](../../xdm/home.md).