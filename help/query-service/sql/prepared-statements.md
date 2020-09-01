---
keywords: Experience Platform;home;popular topics;query service;Query service;prepared statements;prepared;sql;
solution: Experience Platform
title: Förberedda programsatser
topic: prepared statements
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 7%

---


# Förberedda programsatser

I SQL används förberedda satser för att mallatisera liknande frågor eller uppdateringar. Adobe Experience Platform [!DNL Query Service] stöder förberedda satser med hjälp av en parametriserad fråga. Detta kan användas för att optimera prestanda eftersom du inte längre behöver tolka en fråga om och om igen.

## Använda förberedda satser

Följande syntaxer stöds när förberedda satser används:

- [FÖRBEREDA](#prepare)
- [KÖR](#execute)
- [DEALOCATE](#deallocate)

### Förbered en programsats {#prepare}

Den här SQL-frågan sparar den skrivna SELECT-frågan med namnet som `PLAN_NAME`. Du kan använda variabler, till exempel `$1` i stället för faktiska värden. Den här förberedda satsen sparas under den aktuella sessionen. Observera att namn på planer **inte** är skiftlägeskänsliga.

#### SQL-format

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Exempel på SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Kör en förberett utdrag {#execute}

Den här SQL-frågan använder den förberedda satsen som skapades tidigare.

#### SQL-format

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Exempel på SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Frigör en förberedd sats {#deallocate}

Den här SQL-frågan används för att ta bort den namngivna förberedda satsen.

#### SQL-format

```sql
DEALLOCATE {PLAN_NAME}
```

#### Exempel på SQL

```sql
DEALLOCATE test;
```

## Exempelflöde med förberedda satser

Till att börja med kan du ha en SQL-fråga, som den nedan:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

SQL-frågan ovan returnerar följande svar:

| id | förnamn | efternamn | födelsedatum | e-post | stad | land |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Kanada |
| 10001 | antoin | dubois | 1967-03-14 | example2@example.com | Paris | Frankrike |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japan |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Sverige |
| 10004 | aasir | mithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Den här SQL-frågan kan parametriseras med följande förberedda sats:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Nu kan den förberedda programsatsen köras med följande anrop:

```sql
EXECUTE getIdRange(10000, 10005);
```

När det anropas ser du exakt samma resultat som tidigare:

| id | förnamn | efternamn | födelsedatum | e-post | stad | land |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Kanada |
| 10001 | antoin | dubois | 1967-03-14 | is | Paris | Japan |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japan |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Sverige |
| 10004 | aasir | mithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Chile |

När du är klar med den förberedda satsen kan du frigöra den med följande anrop:

```sql
DEALLOCATE getIdRange;
```
