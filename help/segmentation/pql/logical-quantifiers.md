---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Logiska kvantifierare
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funktioner för logisk kvantifierare

Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i PQL (Profile Query Language). Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

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
