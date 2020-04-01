---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 10 september 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 28a8fc496c85b334e89d0f0a130d3cc5c8956399

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 10 september 2019

## Dataintag

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och latens. Adobe Experience Platform Data Ingtake erbjuder flera alternativ för inmatning av data, bland annat API:er för batch, API:er för direktuppspelning, inbyggda Adobe-anslutningar, dataintegreringspartners eller användargränssnittet för Adobe Experience Platform.

**Nya funktioner**

| Funktion | Beskrivning |
| ----------- | ---------- |
| Ny domän för direktuppspelning | Domänen har `dcs.data.adobe.net` flyttats till den nya gemensamma datainsamlingsdomänen `dcs.adobedc.net`. Användare måste uppdatera sina implementeringar enligt den reviderade dokumentationen för direktuppspelning i Adobe Experience Platform. All dokumentation som rör direktuppspelning i Adobe Experience Platform har uppdaterats för att använda den nya domänen. |

Mer information finns i dokumentationen för [datainmatning](../../ingestion/home.md).

## Datavetenskapens arbetsyta

Adobe Experience Platform Data Science Workspace är en helt hanterad tjänst inom Experience Platform som gör det möjligt för datavetare att sömlöst generera insikter från data och innehåll i Adobes lösningar och tredjepartssystem genom att bygga och driftsätta Machine Learning-modeller. Data Science Workspace är nära integrerat med Platform och är en drivkraft för datavetenskapens hela livscykel, inklusive utforskning och förberedelse av XDM-data, följt av utveckling och driftsättning av modeller för att automatiskt berika kundprofilen i realtid med maskininlärningsinsikter.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Schemaläggning av tjänster via användargränssnittet | Integrerat med Platform Orchestration Service för att automatisera modellutbildning och poängsättning med användardefinierade scheman med hjälp av användargränssnittet. |
| Tjänstgalleri | Sök, övervaka och få tillgång till maskininlärningstjänster med möjlighet att schemalägga automatiska utbildnings- och poängsättningsjobb - allt i det omdesignade servicegalleriet. |
| JupyterLab 5.0.0 | Förbättringar av användargränssnittet för JupyterLab. |

**Kända fel**

* Det finns för närvarande inget tillgängligt sätt i tjänstgalleriet att ta bort en befintlig tjänst. Under tiden kan du läsa API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning om du vill ta bort en befintlig tjänst via API-anrop.
* Service Gallery saknar stöd för sidnumrering för att filtrera en tjänsts utbildning och poängsättning.
* När du konfigurerar schemalagd utbildning eller poängsättning körs via tjänstgalleriet kan du ange att frekvensen ska vara timt för att förhindra att schemat tillämpas.

Mer information finns på [Data Science Workspace Overview](../../data-science-workspace/home.md).

## Frågetjänst

Med frågetjänsten kan du använda standard-SQL för att fråga efter data i Adobe Experience Platform som stöd för en rad olika användningsfall för analys och datahantering. Det är ett serverlöst verktyg som gör att du kan koppla ihop datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att lägga in dem i kundprofilen i realtid.

Du kan använda frågetjänsten för att bygga dataanalysekosystem och skapa en bild av kunderna över deras olika interaktionskanaler. Dessa kanaler kan omfatta försäljningssystem, webb-, mobil- eller CRM-system.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Förbättringar av Frågeredigeraren | En sparfunktion har lagts till som gör att du kan spara en fråga och arbeta med den senare. En bläddringsflik har lagts till i användargränssnittet för frågetjänsten på Adobe Experience Platform där frågor som sparats av användare i organisationen visas. Implementerade en frågeinformationspanel som visar användbara metadata om frågan som visas. |
| Nya attribueringsfunktioner | Adobe-definierade funktioner i Query Service för att fråga efter kanalattribuering med parametrar för förfallodatum. |
| Förbättringar av SQL-syntax | Stöd för iLike-syntax. |
| Generera datauppsättningar med ett definierat XDM-schema | En ny sats har lagts till i CTAS-frågor (Create Table as Select) som gör att du kan ange ett målschema. |

Mer information finns i dokumentationen [till](../../query-service/home.md)frågetjänsten.