---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 10 september 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 10 september 2019**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [!DNL Data Ingestion](#ingestion)
* [!DNL Data Science Workspace](#dsw)
* [!DNL Query Service](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform har en mängd funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] erbjuder flera alternativ för inmatning av data, bland annat API:er för gruppbearbetning, API:er för direktuppspelning, Adobe-kopplingar, dataintegrationspartners och användargränssnittet för Adobe Experience Platform.

**Nya funktioner**

| Funktion | Beskrivning |
| ----------- | ---------- |
| Ny domän för direktuppspelning | Domänen har `dcs.data.adobe.net` flyttats till den nya gemensamma datainsamlingsdomänen `dcs.adobedc.net`. Användare måste uppdatera sina implementeringar enligt den reviderade dokumentationen för direktuppspelning i Adobe Experience Platform. All dokumentation som rör direktuppspelning i Adobe Experience Platform har uppdaterats för att använda den nya domänen. |

Mer information finns i dokumentationen för [datainmatning](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] är en helt hanterad tjänst inom [!DNL Experience Platform] vilken datavetare smidigt kan generera insikter från data och innehåll i olika Adobe-lösningar och tredjepartssystem genom att bygga och driftsätta Machine Learning-modeller. [!DNL Data Science Workspace] är nära integrerat med [!DNL Platform] och driver hela livscykeln för datavetenskap, inklusive utforskning och förberedelse av XDM-data, följt av utveckling och driftsättning av modeller som automatiskt berikar [!DNL Real-time Customer Profile] med maskininlärningsinsikter.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Schemaläggning av tjänster via användargränssnittet | Integrerat med [!DNL Platform] Orchestration Service för att automatisera modellutbildning och poängsättning med användardefinierade scheman med hjälp av användargränssnittet. |
| [!DNL Service Gallery] | Sök, övervaka och få tillgång till maskininlärningstjänster med möjlighet att schemalägga automatiska utbildnings- och poängsättningsjobb - allt i den omdesignade [!DNL Service Gallery]versionen. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Förbättrat användargränssnitt. |

**Kända fel**

* Det finns för närvarande inget sätt att ta bort en befintlig tjänst på i [!DNL Service Gallery] . Under tiden kan du läsa API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning om du vill ta bort en befintlig tjänst via API-anrop.
* Det finns [!DNL Service Gallery] inget stöd för sidnumrering för att filtrera en tjänsts utbildning och poängsättning.
* När schemalagd utbildning eller poängsättning konfigureras går igenom [!DNL Service Gallery]programmet och du anger frekvensen till en timme så att schemat inte kan tillämpas.

Mer information finns på [Data Science Workspace Overview](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] ger möjlighet att använda standard-SQL för att fråga data i Adobe Experience Platform som stöd för en mängd olika användningsfall för analys och datahantering. Det är ett serverlöst verktyg som gör att du kan koppla ihop datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning för användning vid rapportering [!DNL Data Science Workspace]eller för förtäring i [!DNL Real-time Customer Profile].

Ni kan använda [!DNL Query Service] för att skapa ekosystem för dataanalys och skapa en bild av kunderna över deras olika interaktionskanaler. Dessa kanaler kan omfatta försäljningssystem, webb-, mobil- eller CRM-system.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Förbättringar av [!DNL Query Editor] | En sparfunktion har lagts till som gör att du kan spara en fråga och arbeta med den senare. En flik för Bläddra har lagts till i användargränssnittet på Adobe Experience Platform och där visas frågor som sparats av användare i din organisation. [!DNL Query Service] Implementerade en frågeinformationspanel som visar användbara metadata om frågan som visas. |
| Nya attribueringsfunktioner | Adobe-definierade funktioner i [!DNL Query Service] för att fråga efter kanalattribuering med parametrar för förfallodatum. |
| Förbättringar av SQL-syntax | Stöd för iLike-syntax. |
| Generera datauppsättningar med ett definierat XDM-schema | En ny sats har lagts till i CTAS-frågor (Create Table as Select) som gör att du kan ange ett målschema. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).