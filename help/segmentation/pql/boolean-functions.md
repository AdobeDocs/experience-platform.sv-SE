---
solution: Experience Platform
title: PQL-booleska funktioner
description: Booleska funktioner används för att utföra boolesk logik för olika element i PQL (Profile Query Language).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Booleska funktioner

Booleska funktioner används för att utföra boolesk logik för olika element i [!DNL Profile Query Language] (PQL).  Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikt](./overview.md).

## Och

The `and` -funktionen används för att skapa en logisk koppling.

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

The `or` används för att skapa en logisk förskjutning.

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

The `not` (eller `!`) används för att skapa en logisk negation.

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

The `if` -funktionen används för att matcha ett uttryck beroende på om ett angivet villkor är sant.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Det booleska uttryck som testas. |
| `{TRUE_EXPRESSION}` | Det uttryck vars värde ska användas om `{TEST_EXPRESSION}` är sant. |
| `{FALSE_EXPRESSION}` | Det uttryck vars värde ska användas om `{TEST_EXPRESSION}` är false. |

**Exempel**

Följande PQL-fråga ställer in värdet som `1` om hemlandet är Kanada och `2` om hemlandet inte är Kanada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Nästa steg

Nu när du har lärt dig om booleska funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profilfrågespråk - översikt](./overview.md).
