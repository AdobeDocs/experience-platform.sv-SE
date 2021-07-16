---
title: Sorteringssvar i Reaktors-API
description: Lär dig hur du filtrerar resultat när du visar resurser i Reactor API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Sortera svar i Reactor API

Genom att visa slutpunkter i Reaktors API kan du sortera returnerade resurser baserat på angivna attribut. Du kan konfigurera sorteringsordningen för svaret genom att ange en `sort`-parameter i sökvägen för begäran.

## Sortera stigande

Resurserna kan sorteras efter ett attribut i stigande ordning genom att ange
det attribut som ska sorteras och prefixera det med en `+`:

`GET /companies/:company_id/properties?sort=+name`

## Sortera fallande

Resurserna kan sorteras efter ett attribut i fallande ordning genom att ange
det attribut som ska sorteras och prefixera det med en `-`:

`GET /companies/:company_id/properties?sort=-name`

## Flera sorters

Om du vill sortera efter flera värden anger du sorteringsdirektiven som kommaavgränsade
lista:

`GET /companies/:company_id/properties?sort=+name,-org_id`
