---
keywords: Experience Platform;data prep;data prep api;felsökning;API
title: API-översikt för dataprep
topic: guide
description: Med Data Prep API kan du skapa mappningsuppsättningar och -funktioner programmatiskt, så att du kan omforma dina data mellan käll- och målscheman.
translation-type: tm+mt
source-git-commit: cae6dc80d0394db51dc97478b92459be64c64498
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# API-guide för mappningstjänst

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM). Dataförinställning visas som ett steg för&quot;Karta&quot; i dataöverföringsprocesserna, inklusive arbetsflödet för CSV-inmatning.

API:t för mappningstjänsten, som också kallas API:t för dataförberedelser, innehåller flera slutpunkter som beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guiden](./getting-started.md) finns viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

## Funktioner

Med mappningsfunktionerna kan du omforma data mellan käll- och målscheman. Du kan använda slutpunkten `/languages/el` för att validera dina uttryck och få en lista över alla tillgängliga mappningsfunktioner och -åtgärder.

Mer information om hur du använder mappningsmängdsfunktioner finns i [funktionsslutpunktshandboken](./functions.md).

## Mappningsuppsättning

Mappningsuppsättningar kan användas för att definiera hur data i ett källschema mappas till data i ett målschema. Du kan använda slutpunkten `/mappingSets` i API:t för dataprep för att hämta, skapa, uppdatera och validera mappningsuppsättningar programmatiskt.

Mer information om hur du använder mappningsuppsättningar finns i [guiden för mappningsuppsättning](./mapping-set.md).

## Nästa steg

Om du vill börja ringa anrop med API:t för mappningstjänsten ska du läsa [Komma igång-guiden](./getting-started.md) och sedan välja en av slutpunktshandböckerna för att lära dig hur du använder de specifika slutpunkterna.