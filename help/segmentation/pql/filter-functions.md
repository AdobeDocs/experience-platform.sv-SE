---
solution: Experience Platform
title: PQL-filterfunktioner
description: Filterfunktioner används för att filtrera data inom arrayer i PQL (Profile Query Language).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---

# Filterfunktioner

Filterfunktioner som används för att filtrera data i arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikt](./overview.md).

## Filter

The `[]` (filter) gör att filter kan tillämpas på en array och returnera en delmängd av arrayen som matchar det angivna villkoret.

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

The `^` (upp) kan du referera till egenskaper på den övre filternivån.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beskrivning |
| -------- | ----------- |
| `{ARRAY}` | Arrayen som filtreras. |
| `{FILTER_1}` | Filtreringens yttre lager. |
| `{FILTER_2}` | Filtreringens inre lager |
| `^{PROPERTY}` | Den egenskap som också filtreras. På grund av `^`kontrollerar den en egenskap som baseras på filter1. |

**Exempel**

Följande PQL-fråga hämtar alla händelser som har minst ett produktobjekt med en SKU som är lika med &quot;PS&quot; **eller** har en person vars kön är kvinnlig.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Nästa steg

Nu när du har lärt dig mer om filterfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profilfrågespråk - översikt](./overview.md).
