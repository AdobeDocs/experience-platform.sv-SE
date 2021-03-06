---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;diverse funktioner;misc;
solution: Experience Platform
title: PQL Övriga funktioner
topic-legacy: developer guide
description: Följande funktion är en annan funktion för PQL (Profile Query Language).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 2%

---

# Diverse funktioner

Följande funktion är en annan funktion för [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Låt

Med funktionen `let` kan ett uttryck lagras som en variabel som senare kan användas i en fråga.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exempel**

Följande PQL-fråga hämtar alla produktsummor med transaktionen i USD där summan är större än 100 och mindre än 1 000 USD.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Nästa steg

Nu när du har lärt dig mer om olika funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
