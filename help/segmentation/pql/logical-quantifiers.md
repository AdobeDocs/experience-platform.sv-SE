---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profile Query Language;logiska kvantifierare;logisk kvantifierare;
solution: Experience Platform
title: PQL logiska kvantifierare
topic: developer guide
description: Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i PQL (Profile Query Language).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---


# Funktioner för logisk kvantifierare

Logiska kvantifierare kan användas för att bekräfta villkor med arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Finns

Funktionen `exists` avgör om det finns ett objekt i en array, förutsatt att den uppfyller det angivna villkoret.

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

Nu när du har lärt dig mer om logiska kvantifierare kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
