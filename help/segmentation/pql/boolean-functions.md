---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: Booleska funktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%

---


# Booleska funktioner

Booleska funktioner används för att utföra boolesk logik för olika element i [!DNL Profile Query Language] (PQL).  Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Och

Funktionen `and` används för att skapa en logisk koppling.

**Format**

```sql
{QUERY} and {QUERY}
```

**Exempel**

Följande PQL-fråga returnerar alla personer med hemland som Kanada och födelseåret 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## eller

Funktionen `or` används för att skapa en logisk förskjutning.

**Format**

```sql
{QUERY} or {QUERY}
```

**Exempel**

Följande PQL-fråga returnerar alla personer med hemlandet som Kanada eller födelseåret 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Inte

Funktionen `not` (eller `!`) används för att skapa en logisk negation.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Exempel**

Följande PQL-fråga returnerar alla personer som inte har sitt hemland som Kanada.

```sql
not (homeAddress.countryISO = "CA")
```

## If

Funktionen används `if` för att matcha ett uttryck beroende på om ett angivet villkor är sant.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Det booleska uttryck som testas. |
| `{TRUE_EXPRESSION}` | Uttrycket vars värde ska användas om `{TEST_EXPRESSION}` är true. |
| `{FALSE_EXPRESSION}` | Uttrycket vars värde ska användas om `{TEST_EXPRESSION}` är false. |

**Exempel**

Följande PQL-fråga ställer in värdet som `1` om hemlandet är Kanada och `2` om hemlandet inte är Kanada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Nästa steg

Nu när du har lärt dig om booleska funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
