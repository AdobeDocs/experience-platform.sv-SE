---
title: Sidindela svar i reaktors-API
description: Lär dig hur du numrerar resultat när du visar resurser i Reactor API.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Sidindela svar i reaktors-API

Svaren som returneras av Reaktors-API är numrerade. Standardsidstorleken är 25 element. Information om sidnumreringen finns i `meta.pagination `i API-svarsobjektet:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

Du kan hämta en viss sida och ändra storleken på en sida genom att ta med en `page` frågeparametern i sökvägen för begäran.

## Hämta en specifik sida

Så här hämtar du en specifik sida:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Ändra sidstorlek

Så här ändrar du sidstorlek:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

Olika alternativ kan kombineras:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
