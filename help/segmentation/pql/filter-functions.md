---
solution: Experience Platform
title: PQL filterfunktioner
description: Filterfunktioner används för att filtrera data i arrayer i Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 7c282594e66c8c7700471a94947448fd91596814
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Filterfunktioner

Filterfunktioner används för att filtrera data inom arrayer i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Filter

Funktionen `[]` (filter) tillåter att filter tillämpas på en array och returnerar en delmängd av arrayen som matchar det angivna villkoret. Därför returnerar den här funktionen en array.

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

Operatorn `^` (upp) gör att du kan referera till egenskaper på den övre filternivån.

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

Nu när du har lärt dig mer om filterfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
