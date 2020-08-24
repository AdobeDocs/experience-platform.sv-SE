---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diverse funktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 2%

---


# Diverse funktioner

Följande funktion är en annan funktion för [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

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
