---
solution: Experience Platform
title: Strängfunktioner i PQL
description: Profile Query Language (PQL) har funktioner som underlättar interaktion med strängar.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 1%

---

# Strängfunktioner

[!DNL Profile Query Language] (PQL) erbjuder funktioner som gör det enklare att interagera med strängar. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Gilla

Funktionen `like` används för att avgöra om en sträng matchar ett angivet mönster som ett booleskt värde.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Det uttryck som ska matchas mot den första strängen. Det finns två specialtecken som stöds för att skapa ett uttryck: `%` och `_`. <ul><li>`%` används för att representera noll eller flera tecken.</li><li>`_` används för att representera exakt ett tecken.</li></ul> |

**Exempel**

Följande PQL-fråga hämtar alla städer som innehåller mönstret &quot;es&quot;.

```sql
city like "%es%"
```

## Börjar med

Funktionen `startsWith` används för att avgöra om en sträng börjar med en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens namn börjar med &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Börjar inte med

Funktionen `doesNotStartWith` används för att avgöra om en sträng inte börjar med en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens namn inte börjar med &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Slutar med

Funktionen `endsWith` används för att avgöra om en sträng avslutas med en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens e-postadress slutar med &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Slutar inte med

Funktionen `doesNotEndWith` används för att avgöra om en sträng inte avslutas med en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens e-postadress inte avslutas med &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Innehåller

Funktionen `contains` används för att avgöra om en sträng innehåller en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens e-postadress innehåller strängen &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Innehåller inte

Funktionen `doesNotContain` används för att avgöra om en sträng inte innehåller en angiven delsträng som boolesk.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Den sträng som ska sökas efter i den första strängen. |
| `{BOOLEAN}` | En valfri parameter som avgör om kontrollen är skiftlägeskänslig. Som standard är detta true. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens e-postadress inte innehåller strängen &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Lika med

Funktionen `equals` används för att avgöra om en sträng är lika med den angivna strängen som ett booleskt värde.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Strängen som ska jämföras med den första strängen. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens namn är &quot;John&quot;.

```sql
person.name.equals("John")
```

## Inte lika med

Funktionen `notEqualTo` används för att avgöra om en sträng inte är lika med den angivna strängen som ett booleskt värde.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{STRING_1}` | Strängen som kontrollen ska utföras på. |
| `{STRING_2}` | Strängen som ska jämföras med den första strängen. |

**Exempel**

Följande PQL-fråga avgör, med skiftlägeskänslighet, om personens namn inte är&quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Matchar

Funktionen `matches` används för att avgöra om en sträng matchar ett visst reguljärt uttryck. Mer information om att matcha mönster i reguljära uttryck som booleska uttryck finns i [det här dokumentet](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html).

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Exempel**

Följande PQL-fråga avgör, utan att vara skiftlägeskänslig, om personens namn börjar med &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Om du använder funktioner för reguljära uttryck som `\w`, måste **du** undvika det omvända snedstrecket. I stället för att bara skriva `\w` måste du inkludera ett extra omvänt snedstreck och skriva `\\w`.

## Grupp för reguljära uttryck

Funktionen `regexGroup` används för att extrahera specifik information baserat på det reguljära uttrycket som anges som en sträng.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exempel**

Följande PQL-fråga används för att extrahera domännamnet från en e-postadress.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Om du använder funktioner för reguljära uttryck som `\w`, måste **du** undvika det omvända snedstrecket. I stället för att bara skriva `\w` måste du inkludera ett extra omvänt snedstreck och skriva `\\w`.

## Nästa steg

Nu när du har lärt dig om strängfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
