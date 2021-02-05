---
keywords: Experience Platform;hem;populära ämnen;segmentering;segmentering;segmenteringstjänst;pql;PQL;profilfrågespråk;filterfunktioner;filter;
solution: Experience Platform
title: PQL-filterfunktioner
topic: developer guide
description: Filterfunktioner används för att filtrera data inom arrayer i PQL (Profile Query Language).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Filterfunktioner

Filterfunktioner används för att filtrera data inom arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Filter

Med funktionen `[]` (filter) kan filter tillämpas på en array och returnera en delmängd av arrayen som matchar det angivna villkoret.

**Format**

```sql
{ARRAY}[filter]
```

**Exempel**

Följande PQL-fråga hämtar alla händelser som har minst ett produktobjekt med en SKU som är lika med &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Upp, operator

Med `^`-operatorn (upp) kan du referera till egenskaper i de övre filternivåerna.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beskrivning |
| -------- | ----------- |
| `{ARRAY}` | Arrayen som filtreras. |
| `{FILTER_1}` | Filtreringens yttre lager. |
| `{FILTER_2}` | Filtreringens inre lager |
| `^{PROPERTY}` | Den egenskap som också filtreras. På grund av `^` kontrollerar den en egenskap som är baserad på filter1. |

**Exempel**

Följande PQL-fråga hämtar alla händelser som har minst ett produktobjekt med en SKU som är lika med &quot;PS&quot; **eller** har en person vars kön är kvinnlig.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Nästa steg

Nu när du har lärt dig mer om filterfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
