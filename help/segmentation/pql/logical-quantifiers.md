---
solution: Experience Platform
title: PQL logiska kvantifierare
description: Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i Profile Query Language (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Funktioner för logisk kvantifierare

Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Finns

Funktionen `exists` avgör om ett objekt finns i en array, förutsatt att det uppfyller det angivna villkoret.

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

Följande PQL-fråga hämtar alla händelser som har ett pris som är högre än 50 USD eller som har SKU:n &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## För alla

Funktionen `forall` avgör alla objekt i en array som uppfyller alla angivna villkor.

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

Nu när du har lärt dig mer om logiska kvantifierare kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
