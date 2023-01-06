---
keywords: Experience Platform;data prep;data prep api;felsökning;API
title: API-översikt för dataprep
description: Med Data Prep API kan du skapa mappningsuppsättningar och -funktioner programmatiskt, så att du kan omforma dina data mellan käll- och målscheman.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# API-guide för mappningstjänst

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM). Dataförinställning visas som ett steg för&quot;Karta&quot; i dataöverföringsprocesserna, inklusive arbetsflödet för CSV-inmatning.

API:t för mappningstjänsten, som också kallas API:t för dataförberedelser, innehåller flera slutpunkter som beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

## Funktioner

Med mappningsfunktionerna kan du omforma data mellan käll- och målscheman. Du kan använda `/languages/el` slutpunkt för att validera dina uttryck och få en lista över alla tillgängliga mappningsfunktioner och -åtgärder.

Mer information om hur du använder mappningsfunktioner finns i [funktionsslutpunktsguide](./functions.md).

## Mappningsuppsättning

Mappningsuppsättningar kan användas för att definiera hur data i ett källschema mappas till data i ett målschema. Du kan använda `/mappingSets` slutpunkt i API:t för dataprep för att hämta, skapa, uppdatera och validera mappningsuppsättningar programmatiskt.

Mer information om hur du använder mappningsuppsättningar finns i [slutpunktshandbok för mappningsuppsättning](./mapping-set.md).

## Nästa steg

Läs mer om hur du börjar ringa anrop med API:t för mappningstjänsten [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktshandböckerna för att lära dig hur du använder de specifika slutpunkterna.
