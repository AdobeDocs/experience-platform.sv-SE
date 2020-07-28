---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM-scheman och -beskrivningar
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Arbeta med [!DNL Experience Data Model] XDM-scheman och relationsbeskrivningar

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering. Scheman är standardmetoden för att beskriva data i, [!DNL Experience Platform]vilket gör att alla data som uppfyller scheman kan återanvändas utan konflikter i en organisation och till och med delas mellan flera organisationer. Om du vill veta mer om XDM-scheman börjar du med att läsa [översikten över](../xdm/home.md)XDM-systemet.

## Skapa ett schema med schemaregistret

Schemaregistret innehåller ett användargränssnitt och RESTful API som du kan använda för att visa och hantera alla resurser i schemabiblioteket i Adobe Experience Platform. Schemabiblioteket innehåller resurser som du har fått av Adobe, [!DNL Experience Platform] partners och leverantörer vars program du använder, samt resurser som du definierar och sparar i schemaregistret. Om du vill lära dig hur du skapar scheman för din organisation kan du följa självstudiekurserna för att [skapa ett schema med API:t](../xdm/tutorials/create-schema-api.md) för schemaregister eller [skapa ett schema med användargränssnittet](../xdm/tutorials/create-schema-ui.md)för Schemaredigeraren.

## Definiera en relation mellan två scheman

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för era [!DNL Experience Data Model] (XDM) scheman kan ni få komplexa insikter i era kunddata. De här relationsbeskrivningarna kan definieras med API:t för schemaregister och gränssnittet för schemaredigeraren. Mer information finns i självstudiekurserna för att definiera relationer mellan två scheman [med API:t](../xdm/tutorials/relationship-api.md) eller [med gränssnittet](../xdm/tutorials/relationship-ui.md).

## Skapa ett ad hoc-schema

Under särskilda omständigheter kan det vara nödvändigt att skapa ett [!DNL Experience Data Model] (XDM)-schema med fält som namnges endast för användning av en enda datauppsättning. Detta kallas för ett ad hoc-schema. Ad-hoc-scheman används i olika arbetsflöden för [dataöverföring](../ingestion/home.md) för [!DNL Experience Platform], inklusive inmatning av CSV-filer och skapande av vissa typer av [källanslutningar](../sources/home.md). Ett ad hoc-schema skapas med API:t för schemaregister och är avsett att användas tillsammans med andra [!DNL Experience Platform] självstudiekurser som kräver att ett ad hoc-schema skapas som en del av arbetsflödet. Om du vill börja skapa ett ad hoc-schema ska du titta i självstudiekursen för att [skapa ett ad hoc-schema med API](../xdm/tutorials/ad-hoc.md).

## Nästa steg

När du har definierat scheman för din organisation kan du börja skapa datauppsättningar som data kan importeras till. Om du vill komma igång läser du följande dokumentation:

* [Översikt över datauppsättningar](../catalog/datasets/overview.md)
* [Översikt över datainmatning](../ingestion/home.md)