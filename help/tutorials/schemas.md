---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: XDM-scheman och -beskrivningar
topic-legacy: tutorial
type: Tutorial
description: Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering. Scheman är standardmetoden för att beskriva data i Experience Platform, vilket gör att alla data som överensstämmer med scheman kan återanvändas utan konflikter i en organisation och till och med delas mellan flera organisationer.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Arbeta med [!DNL Experience Data Model]-scheman (XDM) och relationsbeskrivningar

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering. Scheman är standardmetoden för att beskriva data i [!DNL Experience Platform], vilket gör att alla data som uppfyller scheman kan återanvändas utan konflikter i en organisation och till och med delas mellan flera organisationer. Om du vill veta mer om XDM-scheman börjar du med att läsa [systemöversikten för XDM](../xdm/home.md).

## Skapa ett schema med schemaregistret

Schemaregistret innehåller ett användargränssnitt och RESTful API som du kan använda för att visa och hantera alla resurser i Adobe Experience Platform Schema Library. Schemabiblioteket innehåller resurser som Adobe, [!DNL Experience Platform] partners och leverantörer har gjort tillgängliga för dig, samt resurser som du definierar och sparar i schemaregistret. Om du vill lära dig hur du skapar scheman för din organisation kan du följa självstudiekurserna för [att skapa ett schema med API:t för schemaregister](../xdm/tutorials/create-schema-api.md) eller [skapa ett schema med användargränssnittet för Schemaredigeraren](../xdm/tutorials/create-schema-ui.md).

## Definiera en relation mellan två scheman

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för dina [!DNL Experience Data Model] (XDM)-scheman kan du få komplexa insikter i dina kunddata. De här relationsbeskrivningarna kan definieras med API:t för schemaregister och gränssnittet för schemaredigeraren. Mer information finns i självstudiekurserna för att definiera relationer mellan två scheman [med API](../xdm/tutorials/relationship-api.md) eller [med gränssnittet](../xdm/tutorials/relationship-ui.md).

## Skapa ett ad hoc-schema

Under särskilda omständigheter kan det vara nödvändigt att skapa ett [!DNL Experience Data Model]-schema (XDM) med fält som bara namnges av en enda datauppsättning. Detta kallas för ett ad hoc-schema. Ad-hoc-scheman används i olika [arbetsflöden för datainmatning](../ingestion/home.md) för [!DNL Experience Platform], inklusive inhämtning av CSV-filer och skapande av vissa typer av [källanslutningar](../sources/home.md). Ett ad hoc-schema skapas med API:t för schemaregister och är avsett att användas tillsammans med andra [!DNL Experience Platform]-självstudier som kräver att ett ad hoc-schema skapas som en del av arbetsflödet. Om du vill börja skapa ett ad hoc-schema ska du titta i självstudiekursen för [att skapa ett ad hoc-schema med API](../xdm/tutorials/ad-hoc.md).

## Nästa steg

När du har definierat scheman för din organisation kan du börja skapa datauppsättningar som data kan importeras till. Om du vill komma igång läser du följande dokumentation:

* [Översikt över datauppsättningar](../catalog/datasets/overview.md)
* [Översikt över datainmatning](../ingestion/home.md)
