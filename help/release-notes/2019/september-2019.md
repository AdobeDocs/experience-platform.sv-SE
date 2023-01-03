---
title: Adobe Experience Platform Versionsinformation september 2019
description: Versionsinformation för september 2019 för Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 10 september 2019**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] innehåller flera alternativ för inmatning av data, bland annat API:er för grupper av filer, API:er för direktuppspelning, inbyggda Adobe-anslutningar, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Nya funktioner**

| Funktion | Beskrivning |
| ----------- | ---------- |
| Ny domän för direktuppspelning | The `dcs.data.adobe.net` domänen har flyttats till den nya gemensamma datainsamlingsdomänen `dcs.adobedc.net`. Användare måste uppdatera sina implementeringar enligt den reviderade dokumentationen för direktuppspelning från Adobe Experience Platform. All dokumentation som rör inhämtning av direktuppspelning från Adobe Experience Platform har uppdaterats för att använda den nya domänen. |

Mer information finns på [Dokumentation för datainmatning](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] är en helt hanterad tjänst inom [!DNL Experience Platform] som gör det möjligt för datavetare att sömlöst generera insikter från data och innehåll i olika Adobe-lösningar och tredjepartssystem genom att bygga och driftsätta Machine Learning-modeller. [!DNL Data Science Workspace] är nära integrerat med [!DNL Platform] och driver datavetenskapens hela livscykel, inklusive utforskning och förberedelse av XDM-data, följt av utveckling och driftsättning av modeller för att automatiskt berika [!DNL Real-Time Customer Profile] med maskininlärningsinsikter.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Schemaläggning av tjänster via användargränssnittet | Integrerat med [!DNL Platform] Orchestration Service för att automatisera modellutbildning och poängsättning med användardefinierade scheman med hjälp av användargränssnittet. |
| [!DNL Service Gallery] | Sök, övervaka och få tillgång till maskininlärningstjänster med möjlighet att schemalägga automatiska utbildnings- och poängsättningsjobb, allt i den omdesignade [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Förbättrat användargränssnitt. |

**Kända fel**

* Det finns för närvarande inget sätt att komma åt [!DNL Service Gallery] om du vill ta bort en befintlig tjänst. Under tiden kan du läsa [API-referens för Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) för att ta bort en befintlig tjänst via API-anrop.
* The [!DNL Service Gallery] saknar stöd för sidnumrering för att filtrera en tjänsts utbildning och poängsättning.
* När schemalagd utbildning eller poängsättning konfigureras körs den [!DNL Service Gallery], och genom att ställa in frekvensen på timvis förhindras schemat från att tillämpas.

Mer information finns på [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] ger möjlighet att använda standard-SQL för att fråga data i Adobe Experience Platform för att stödja en rad olika användningsfall för analys och datahantering. Det är ett serverlöst verktyg som gör att du kan koppla samman datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datamängd som kan användas vid rapportering, [!DNL Data Science Workspace]eller för förtäring i [!DNL Real-Time Customer Profile].

Du kan använda [!DNL Query Service] att bygga upp ekosystem för dataanalys och skapa en bild av kunderna över deras olika interaktionskanaler. Dessa kanaler kan omfatta försäljningssystem, webb-, mobil- eller CRM-system.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Förbättringar av [!DNL Query Editor] | En sparfunktion har lagts till som gör att du kan spara en fråga och arbeta med den senare. En bläddringsflik har lagts till i [!DNL Query Service] användargränssnitt i Adobe Experience Platform som visar frågor som sparats av användare i din organisation. Implementerade en frågeinformationspanel som visar användbara metadata om frågan som visas. |
| Nya attribueringsfunktioner | Adobe-definierade funktioner i [!DNL Query Service] för att fråga efter kanalattribuering med parametrar för förfallodatum. |
| Förbättringar av SQL-syntax | Stöd för iLike-syntax. |
| Generera datauppsättningar med ett definierat XDM-schema | En ny sats har lagts till i CTAS-frågor (Create Table as Select) som gör att du kan ange ett målschema. |

Mer information finns i [Dokumentation för frågetjänsten](../../query-service/home.md).
