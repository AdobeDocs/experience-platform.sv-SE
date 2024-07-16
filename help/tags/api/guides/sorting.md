---
title: Sorteringssvar i Reaktors-API
description: Lär dig hur du filtrerar resultat när du visar resurser i Reactor API.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Sortera svar i Reactor API

Genom att visa slutpunkter i Reaktors API kan du sortera returnerade resurser baserat på angivna attribut. Du kan konfigurera sorteringsordningen för svaret genom att ange en `sort`-parameter i sökvägen för begäran.

## Sortera stigande

Resurserna kan sorteras efter ett attribut i stigande ordning genom att ange
attribut att sortera efter och prefixera det med en `+`:

`GET /companies/:company_id/properties?sort=+name`

## Sortera fallande

Resurserna kan sorteras efter ett attribut i fallande ordning genom att ange
attribut att sortera efter och prefixera det med en `-`:

`GET /companies/:company_id/properties?sort=-name`

## Flera sorters

Om du vill sortera efter flera värden anger du sorteringsdirektiven som kommaavgränsade
lista:

`GET /companies/:company_id/properties?sort=+name,-org_id`
