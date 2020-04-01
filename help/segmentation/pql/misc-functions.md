---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diverse funktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# Diverse funktioner

Följande funktion är en annan funktion för PQL (Profile Query Language). Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

## Låt

Funktionen gör att ett uttryck kan lagras som en variabel som senare kan användas i en fråga. `let`

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

Nu när du har lärt dig mer om olika funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
