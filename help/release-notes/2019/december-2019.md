---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 11 december 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 december 2019**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL-segmenteringstjänst]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL-källor]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment konfigureras och underhålls centralt [!DNL Platform]så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Fliken Sammanfogade målgrupper i [!DNL Segment Builder] | Flikarna [!UICONTROL Segments] och [!UICONTROL Audiences] i [!DNL Segment Builder] har kombinerats till en enda [!UICONTROL Audiences] flik. På den här fliken kan du bläddra och söka efter befintliga målgrupper, som du sedan kan dra och släppa på arbetsytan i regelbyggaren för att skapa en ny segmentdefinition. Referenser till en målgrupp kan lägga till en av följande uppsättningar regellogik i den nya segmentdefinitionen: Målgruppsmedlemskap som regel, den fullständiga uppsättningen regellogik som definierar den refererade målgruppen. |
| Ny plats för kopplingsprincipväljaren | Platsen för sammanslagningsprincipväljaren i [!DNL Segment Builder] har ändrats. Om du vill välja en sammanfogningsprincip för en segmentdefinition klickar du på kugghjulsikonen på **[!UICONTROL Fields]** fliken och väljer sedan den **[!UICONTROL Merge Policy]** nedrullningsbara menyn som du vill använda. |

**Kända fel**

* Ingen

Mer information finns i Översikt över [segmenteringstjänsten](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Med Adobe Experience Platform [!DNL Decisioning Service] kan du programmatiskt och intelligent välja&quot;Nästa bästa upplevelse&quot; bland en uppsättning tillgängliga alternativ för en viss individ, leverera dem till valfri kanal eller tillämpning samt utföra rapportering och analys.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Rankningsfunktioner | Erbjudandeordningen för profiler hämtas nu via en rangordningsfunktion, i stället för en fast uppsättning erbjudanden för alla profiler. |

**Kända fel**

* Ingen.

En fullständig introduktion till tjänsten finns i översikten över [](../../decisioning-service/home.md) beslutstjänsten.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dig mot dina lagringssystem och CRM-tjänster, ange tider för hur mycket information som ska matas in och hantera dataöverföringshastigheten.

**Nya funktioner**

| Funktion | Beskrivning |
| ---------- | ------------ |
| Strömmande anslutning | Med direktuppspelning kan ni skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. Versionen innehåller ett nytt användargränssnitt för direktuppspelad anslutning. |
| Anslutningsstöd för [!DNL Google Cloud Store] | Stöd för datainsamling från [!DNL Google Cloud Store]. |

**Kända fel**

* Ingen.

Mer information om källor finns i [Källöversikt](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga koncept som ligger bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
|--- | ---|
| Förbättrad schemavalidering | Nya kontroller för att se till att referenser tolkas i ytterligare fält som förväntat. Ytterligare kontroller har lagts till i fält som definierats som en array med objekt för att säkerställa att objekten är helt definierade. Förbättrade felmeddelanden som hjälper till att identifiera och åtgärda problem. |

**Felkorrigeringar**

* Underhåll och förbättringar relaterade till åtkomstkontroll och sandlådor.
* Stöd `eTag` för `/descriptors` slutpunkten i [!DNL Schema Registry] API:t.

**Kända fel**

* Ingen

Mer information om hur du arbetar med XDM med [!DNL Schema Registry] API:t och [!DNL Schema Editor] användargränssnittet finns i [XDM-systemdokumentationen](../../xdm/home.md).