---
title: Ange primära identiteter i en ad hoc-datauppsättning
description: Med Adobe Experience Platform Query Service kan du ange en identitet eller en primär identitet för ad hoc-schemadatasfält direkt via SQL ALTER TABLE-kommandot. Dokumentet förklarar hur du använder kommandot ALTER TABLE för att ange en primär identitet eller sekundär identitet.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Ställa in primära identiteter i en ad hoc-datauppsättning

Med Adobe Experience Platform Query Service kan du markera datauppsättningskolumner som antingen primära eller sekundära identiteter med begränsningar för SQL-kommandot `ALTER TABLE`. Du kan använda den här funktionen för att se till att flaggade fält är kompatibla med datasekretesskraven. Med det här kommandot kan du lägga till eller ta bort begränsningar för både primära och sekundära identitetstabellkolumner direkt via SQL.

## Komma igång

Om du anger att datamängdskolumner ska vara primära eller sekundära identiteter måste du känna till SQL-kommandot `ALTER TABLE` och förstå dataintegritetskraven ordentligt. Läs följande dokumentation innan du fortsätter med det här dokumentet:

* [SQL-syntaxguiden för `ALTER TABLE` command](../sql/syntax.md).
* [Datastyrningsöversikten](../../data-governance/home.md) innehåller mer information.

## Lägg till begränsningar {#add-constraints}

Med kommandot `ALTER TABLE` kan du etikettera en datauppsättningskolumn som en persons identitet och sedan använda den etiketten som primär identitet genom att uppdatera associerade metadata med SQL. Detta är särskilt användbart när datauppsättningar skapas via SQL i stället för direkt från ett schema via plattformsgränssnittet. Kommandot kan användas för att säkerställa att dataåtgärderna inom plattformen är kompatibla med dataanvändningsprinciper.

**Exempel**

I följande exempel läggs en begränsning till i den befintliga tabellen `t1`. Värdena för kolumnen `id` har nu markerats som primära identiteter under namnutrymmet `IDFA`. Ett identitetsnamnutrymme är ett nyckelord som deklarerar den typ av identitetsdata som fältet representerar.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Det andra exemplet ser till att kolumnen `id` markeras som en sekundär identitet.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Släpp begränsningar {#drop-constraints}

Begränsningar kan också tas bort från tabellkolumner med kommandot `ALTER TABLE`.

**Exempel**

Följande exempel tar bort kravet på att kolumnen `c1` ska ha en primär identitet i den befintliga tabellen `t1`.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Som framgår nedan används samma syntax för att ta bort en identitetsbegränsning.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Visa identiteter

Använd metadatakommandot `show identities` från kommandoradsgränssnittet för att visa en tabell med alla attribut som har tilldelats som en identitet.

```shell
> show identities;
```

Ett exempel på en returnerad tabell visas nedan.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM-begränsningar {#limitations}

I följande lista förklaras viktiga aspekter av att uppdatera identiteter i befintliga datauppsättningar när du använder XDM.

* Om du vill ange en kolumn som en identitet måste **du** också definiera det namnutrymme som ska bevaras som metadata för kolumnen.
* XDM har inte stöd för att ange ett kolumnnamn i namnutrymmesattributet.
* Om schemat använder `identityMap` XDM-fältet måste `identityMap`-objektet **på rotnivå eller översta nivån** märkas som en identitet eller primär identitet.
