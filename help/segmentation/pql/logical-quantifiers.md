---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Logiska kvantifierare
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 3%

---


# Funktioner för logisk kvantifierare

Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Finns

Funktionen avgör om ett objekt finns i en array, förutsatt att det uppfyller det angivna villkoret. `exists`

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beskrivning |
| ---------- | ----------- |
| `{VARIABLE}` | Ett namn på en variabel. |
| `{EXPRESSION}` | Arrayen som kontrolleras. |
| `{CONDITION}` | Ett valfritt uttryck som filtrerar värdena i arrayen returneras. |

**Exempel**

Följande PQL-fråga hämtar alla händelser som har ett pris som är större än 50 USD eller som har SKU:n &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## För alla

Funktionen avgör `forall` alla objekt i en array som uppfyller alla angivna villkor.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beskrivning |
| ---------- | ----------- |
| `{VARIABLE}` | Ett namn på en variabel. |
| `{EXPRESSION}` | Arrayen som kontrolleras. |
| `{CONDITION}` | Ett valfritt uttryck som filtrerar värdena i arrayen returneras. |

**Exempel**

Följande PQL-fråga hämtar alla händelser som har ett pris som är större än 50 USD och som har SKU:n &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Nästa steg

Nu när du har lärt dig mer om logiska kvantifierare kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
