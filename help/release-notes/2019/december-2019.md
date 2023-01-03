---
title: Adobe Experience Platform Versionsinformation december 2019
description: Versionsinformation om december 2019 för Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 december 2019**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från din [!DNL Real-Time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Fliken Sammanfogade målgrupper i [!DNL Segment Builder] | The [!UICONTROL Segments] och [!UICONTROL Audiences] -flikar i [!DNL Segment Builder] har kombinerats till en enda [!UICONTROL Audiences] -fliken. På den här fliken kan du bläddra och söka efter befintliga målgrupper, som du sedan kan dra och släppa på arbetsytan i regelbyggaren för att skapa en ny segmentdefinition. Referenser till en målgrupp kan lägga till en av följande uppsättningar regellogik i den nya segmentdefinitionen: Målgruppsmedlemskap som regel, den fullständiga uppsättningen regellogik som definierar den refererade målgruppen. |
| Ny plats för kopplingsprincipväljaren | Platsen för sammanslagningsprincipväljaren i [!DNL Segment Builder] har ändrats. Välj en kopplingsprincip för en segmentdefinition genom att klicka på kugghjulsikonen på sidan **[!UICONTROL Fields]** -fliken och sedan använder du **[!UICONTROL Merge Policy]** i listrutan för att välja den sammanfogningsprincip som du vill använda. |

**Kända fel**

* Ingen

Mer information finns i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] ger möjlighet att programmatiskt och intelligent välja&quot;Nästa bästa upplevelse&quot; bland en uppsättning tillgängliga alternativ för en viss individ, leverera dem till valfri kanal eller tillämpning samt utföra rapportering och analys.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Rankningsfunktioner | Erbjudandeordningen för profiler hämtas nu via en rangordningsfunktion, i stället för en fast uppsättning erbjudanden för alla profiler. |

**Kända fel**

* Ingen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dig mot dina lagringssystem och CRM-tjänster, ange tider för hur mycket du får ta emot och hantera dataöverföringshastigheten.

**Nya funktioner**

| Funktion | Beskrivning |
| ---------- | ------------ |
| Strömmande anslutning | Med direktuppspelning kan du skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. Versionen innehåller ett nytt användargränssnitt för direktuppspelad anslutning. |
| Anslutningsstöd för [!DNL Google Cloud Store] | Stöd för datainsamling från [!DNL Google Cloud Store]. |

**Kända fel**

* Ingen.

Mer information om källor finns i [källöversikt](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Förbättrad schemavalidering | Nya kontroller för att se till att referenser tolkas i ytterligare fält som förväntat. Ytterligare kontroller har lagts till i fält som definierats som en array med objekt för att säkerställa att objekten är helt definierade. Förbättrade felmeddelanden som hjälper till att identifiera och åtgärda problem. |

**Felkorrigeringar**

* Underhåll och förbättringar relaterade till åtkomstkontroll och sandlådor.
* Stöd för `eTag` för `/descriptors` slutpunkt i [!DNL Schema Registry] API.

**Kända fel**

* Ingen

Mer information om hur du arbetar med XDM med [!DNL Schema Registry] API och [!DNL Schema Editor] användargränssnittet, läs [XDM-systemdokumentation](../../xdm/home.md).
