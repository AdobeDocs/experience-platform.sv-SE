---
title: Metodtips för dataresursorganisation i frågetjänsten
description: I det här dokumentet beskrivs ett logiskt sätt att ordna data så att de blir lätta att använda med frågetjänsten.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 6e2be299e3c1c0dfa2832ead22cdeaea0ca83591
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Ordna dataresurser i frågetjänsten

Det här dokumentet innehåller riktlinjer för de effektivaste strategierna för att organisera datatillgångar, inklusive datauppsättningar, vyer och tillfälliga tabeller för användning med Adobe Experience Platform Query Service. Det handlar om hur du strukturerar dina data samt om hur du får tillgång till, uppdaterar och tar bort informationen.

Det är viktigt att organisera dina dataresurser logiskt inom plattformen [!DNL Data Lake] när de växer. Med frågetjänsten utökas SQL-konstruktioner som gör att du logiskt kan gruppera dataresurser i en sandlåda. Med den här organisationsmetoden kan du dela datatillgångar mellan scheman utan att behöva flytta dem fysiskt.

## Komma igång

Innan du fortsätter med det här dokumentet bör du ha god förståelse för [Frågetjänst](../home.md) funktioner och har läst [användargränssnittshandbok](../ui/user-guide.md).

## Ordna data i frågetjänsten

I följande exempel visas vilka konstruktioner som är tillgängliga via Adobe Experience Platform Query Service för att logiskt organisera dina data med hjälp av standardsyntaxen för SQL. Du bör börja med att skapa en databas som fungerar som en behållare för dina datapunkter. En databas kan innehålla ett eller flera scheman, och varje schema kan sedan ha en eller flera referenser till en dataresurs (datauppsättningar, vyer, tillfälliga tabeller osv.). Referenserna innehåller relationer eller associationer mellan datauppsättningarna.

Se [Användarhandbok för Frågeredigeraren](../ui/user-guide.md) om du vill ha detaljerad vägledning om hur du använder gränssnittet för frågetjänsten för att skapa SQL-frågor.

Följande SQL-konstruktioner för att logiskt organisera datauppsättningar i en sandlåda stöds.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Exemplet (något trunkerat för att vara kortfattat) visar den här metoden där `databaseA` innehåller schema `schema1`.

## Koppla dataresurser till ett schema

När ett schema har skapats för att fungera som en behållare för dataresurserna kan varje datauppsättning kopplas till ett eller flera scheman i databasen med hjälp av standardsyntaxen för SQL ALTER TABLE.

Följande exempel lägger till `dataset1`, `dataset2`, `dataset3` och `v1` till `databaseA.schema1` behållare som skapades i föregående exempel.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Åtkomst till dataresurser från databehållaren

Genom att kvalificera databasnamnet korrekt kan du [!DNL PostgreSQL] klienten kan ansluta till någon av de datastrukturer som du har skapat med nyckelordet SHOW. Mer information om nyckelordet SHOW finns i [VISA avsnitt i SQL-syntaxdokumentationen](../sql/syntax.md#show).

&quot;all&quot; är standarddatabasnamnet som innehåller alla databaser och schemabehållare i en sandlåda. När du skapar en [!DNL PostgreSQL] anslutning med `dbname="all"`kan du komma åt **alla** databas och schema som du har skapat för att logiskt organisera dina data.

Visar alla databaser under `dbname="all"` visar tre tillgängliga databaser.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Visar alla scheman under `dbname="all"` visar de tre scheman som är relaterade till varje databas i sandlådan.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

När du skapar en [!DNL PostgreSQL] anslutning med `dbname="databaseA"`får du åtkomst till alla scheman som är kopplade till den specifika databasen, vilket visas i exemplet nedan.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

Med punktnotation kan du komma åt alla tabeller som är kopplade till ett specifikt schema som är anslutet till den valda databasen. Genom att ansluta till `DBNAME = databaseA.schema1;`, alla tabeller som är associerade med det specifika schemat (`schema1`) visas. Detta ger information om vilken datauppsättning som innehåller vilket register.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Uppdatera eller ta bort dataresurser från en databehållare

När mängden dataresurser i organisationen (eller sandlådan) växer blir det nödvändigt att uppdatera eller ta bort dataresurser från en databehållare. Du kan ta bort enskilda resurser från organisationsbehållaren genom att referera till rätt databas- och schemanamn med punktnotation. Tabell och vy (`t1` och `v1` respektive) läggs till i `databaseA.schema1` i det första exemplet tas bort med syntaxen i följande exempel.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Ta bort dataresurser

The [DROP TABLE](../sql/syntax.md#drop-table) funktionen tar bara fysiskt bort en dataresurs från [!DNL Data Lake] när en enda referens till tabellen finns i alla databaser i organisationen.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Ta bort en dataresursbehållare

Både databasen och schemat kan också tas bort med standardfunktioner i SQL.

#### Ta bort en databas

Om det finns andra referenser till dataresurser som är associerade med databasen, kommer funktionen att få ett felmeddelande när den försöker ta bort databasen.

```sql
DROP DATABASE databaseA;
```

#### Ta bort ett schema

Det finns tre viktiga saker att tänka på när du tar bort ett schema:

- När du tar bort ett schema tas inga dataresurser som tabeller, vyer eller tillfälliga tabeller bort fysiskt.
- Om det finns några dataresurser som refereras i målschemat och läget är RESTRICT, genereras ett undantag.
- Om det finns några dataresurser som refereras till i målschemat och läget är CASCADE, tar systemet bort alla dataresurser som refereras av schemabehållaren och tar sedan bort schemabehållaren.

```sql
DROP SCHEMA databaseA.schema2;
```

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för de bästa metoderna för att organisera och strukturera dina dataresurser så att de kan användas med Adobe Experience Platform Query Service. Vi rekommenderar att du fortsätter att lära dig mer om hur frågetjänsten fungerar genom att läsa om [dokumentation om datadeduplicering](../essential-concepts/deduplication.md).
