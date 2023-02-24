---
title: Sömlöst SQL-flöde för härledda attribut
description: SQL för frågetjänsten har utökats för att ge sömlöst stöd för härledda attribut. Lär dig hur du använder det här SQL-tillägget för att skapa ett härlett attribut som är aktiverat för profilen och hur du använder attributet för kundprofil och segmenteringstjänst i realtid.
source-git-commit: 1ff66d0ac8e0491a6db518545d122555d9d54c75
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---

# Sömlöst SQL-flöde för härledda attribut

SQL för frågetjänsten har utökats för att ge sömlöst stöd för härledda attribut. Detta är en effektiv alternativ metod för att skapa härledda attribut för era affärssituationer med kundprofiler i realtid.

I det här dokumentet beskrivs olika praktiska SQL-tillägg som genererar ett härlett attribut som kan användas med kundprofilen i realtid. Arbetsflödet förenklar den process som du annars skulle behöva utföra via olika API-anrop eller interaktioner för plattformsgränssnitt.

Generering och publicering av ett attribut för kundprofil i realtid omfattar vanligtvis följande steg:

* Skapa ett identitetsnamnutrymme, om det inte redan finns ett.
* Skapa datatypen för att lagra det härledda attributet, om det behövs.
* Skapa en fältgrupp med den datatypen för att lagra den härledda attributinformationen.
* Skapa eller tilldela en primär identitetskolumn med namnutrymmet som skapades tidigare.
* Skapa ett schema med fältgruppen och datatypen som skapades tidigare.
* Skapa en ny datauppsättning med ditt schema och aktivera den för profil, om det behövs.
* Du kan också markera en datauppsättning som profilaktiverad.

När du har slutfört stegen ovan kan du fylla i datauppsättningen. Om du har aktiverat datauppsättningen för profilen kan du även skapa segment som refererar till det nya attributet och börja skapa insikter.

Med frågetjänsten kan du utföra alla åtgärder som listas ovan med hjälp av SQL-frågor. Detta inkluderar att vid behov göra ändringar i datauppsättningar och fältgrupper.

## Skapa en tabell med ett alternativ för att aktivera den för profilen {#enable-dataset-for-profile}

>[!NOTE]
>
>SQL-frågan som anges nedan förutsätter att ett befintligt namnutrymme används.

Använd en CTAS-fråga (Create Table as Select) för att skapa en datauppsättning, tilldela datatyper, ange en primär identitet, skapa ett schema och markera den som profilaktiverad. Exemplet med SQL-sats nedan skapar attribut och gör den tillgänglig för kunddataprofilen i realtid (Real-Time CDP). SQL-frågan kommer att följa formatet som visas i exemplet nedan:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Datamängder kan också aktiveras för profiler via plattformens användargränssnitt. Mer information om hur du markerar en datauppsättning som aktiverad för profilen finns i [aktivera en datauppsättning för kundprofildokumentation i realtid](../../../catalog/datasets/user-guide.md#enable-profile).

I exempelfrågan nedan visas `decile_table` datauppsättningen skapas med `id` som den primära identitetskolumnen och har namnutrymmet `IDFA`. Den har även ett fält med namnet `decile1Month` av kartdatatypen. Tabellen som skapades (`decile_table`) är aktiverat för profilen.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

<!--        decile3Month map<text, integer>,
            decile6Month map<text, integer>,
            decile9month map<text, integer>,
            decile12month map<text, integer>,
            decilelifetime map<text, integer> -->

När frågan har körts returneras datauppsättnings-ID:t till konsolen, vilket visas i exemplet nedan.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Använd `label='PROFILE'` på en `CREATE TABLE` för att skapa en profilaktiverad datauppsättning. The `upsert` funktionen är aktiverad som standard. The `upsert` kan skrivas över med `ALTER` som i exemplet nedan.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Mer information om hur du använder [ALTER TABLE](../../sql/syntax.md#alter-table) kommando och [etikett som en del av en CTAS-fråga](../../sql/syntax.md#create-table-as-select).

## Konstruerar för hantering av härledda attribut via SQL

De funktioner som beskrivs nedan är till stor nytta när du hanterar härledda attribut via SQL.

### Ändra befintliga datauppsättningar som ska aktiveras för profilen {#enable-existing-dataset-for-profile}

SQL-konstruktionen ALTER TABLE kan användas för att aktivera befintliga datauppsättningar för profilen. Detta kräver att en profilaktiverad tagg läggs till både i schemat och i motsvarande datauppsättning.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Vid slutfört körning av `ALTER TABLE` returnerar konsolen `ALTER SUCCESS`.

### Lägg till en primär identitet till en befintlig datauppsättning {#add-primary-identity}

Markera en befintlig kolumn i en datauppsättning som en primär identitetsuppsättning, annars uppstår ett fel. Om du vill ange en primär identitet med SQL använder du frågeformatet som visas nedan.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Exempel:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

I exemplet som anges `id2` är en befintlig kolumn i `test1_dataset`.

### Inaktivera en datauppsättning för profil {#disable-dataset-for-profile}

Om du vill inaktivera tabellen för profilanvändning måste du använda kommandot DROP. Ett exempel på en SQL-sats som ANVÄNDER `DROP` visas nedan.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Exempel:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Den här SQL-satsen är ett effektivt alternativ till att använda ett API-anrop. Mer information finns i dokumentationen om hur du [inaktivera en datauppsättning för användning med Real-Time CDP via API:t för datauppsättningar](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Tillåt uppdatering och infogningsfunktioner för datauppsättningen {#enable-upsert-functionality-for-dataset}

Med kommandot UPSERT kan du infoga en ny post eller uppdatera befintliga data i en tabell. Du kan uppdatera en befintlig rad om ett angivet värde redan finns i en tabell, eller infoga en ny rad om det angivna värdet inte redan finns.

En exempelprogramsats som använder rätt format visas nedan.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Exempel:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Den här SQL-satsen är ett effektivt alternativ till att använda ett API-anrop. Mer information finns i dokumentationen om hur du [aktivera en datauppsättning för användning med Real-Time CDP och UPSERT med API:t för datauppsättningar](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Inaktivera uppdaterings- och infogningsfunktioner för datauppsättningen {#disable-upsert-functionality-for-dataset}

Det här kommandot inaktiverar möjligheten att uppdatera och infoga rader i datauppsättningen.

En exempelprogramsats som använder rätt format visas nedan.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Exempel:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Visa ytterligare tabellinformation som är associerad med varje tabell {#show-labels-for-tables}

Ytterligare metadata sparas för profilaktiverade datauppsättningar. Använd `SHOW TABLES` för att visa ett extra `labels` kolumn som innehåller information om etiketter som är kopplade till tabeller.

Ett exempel på det här kommandots utdata visas nedan:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

I exemplet ser du att `table_with_a_decile` har aktiverats för profilen och används med etiketter som [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [PROFIL](#enable-existing-dataset-for-profile) enligt beskrivningen ovan.

### Skapa en fältgrupp med SQL

Fältgrupper kan nu skapas med hjälp av SQL. Detta är ett alternativ till att använda Schemaredigeraren i plattformsgränssnittet eller göra ett API-anrop till schemaregistret.

Ett exempel på hur du skapar en fältgrupp visas nedan.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Det går inte att skapa fältgrupper via SQL om `label` ingen flagga anges i satsen eller om fältgruppen redan finns.
>Kontrollera att frågan innehåller en `IF NOT EXISTS` för att undvika att frågan misslyckas eftersom fältgruppen redan finns.

Ett verkligt exempel kan se ut ungefär som det nedan.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Slutförd körning av den här satsen returnerar det skapade fältgrupps-ID:t. Exempel `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Läs dokumentationen om hur du [skapa en ny fältgrupp i Schemaredigeraren](../../../xdm/ui/resources/field-groups.md#create) eller med [API för schemaregister](../../../xdm/api/field-groups.md#create) för mer information om alternativa metoder.

### Släpp en fältgrupp

Ibland kan det vara nödvändigt att ta bort en fältgrupp från schemaregistret. Detta görs genom att köra `DROP FIELDGROUP` med fältgrupps-ID.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Exempel:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Borttagning av en fältgrupp via SQL misslyckas om fältgruppen inte finns. Kontrollera att programsatsen innehåller en `IF EXISTS` för att undvika att frågan misslyckas.

### Visa alla fältgruppsnamn och ID:n för tabellerna

The `SHOW FIELDGROUPS` returnerar en tabell som innehåller tabellens namn, fältgrupp-ID och ägare.

Ett exempel på det här kommandots utdata visas nedan:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Nästa steg

När du har läst det här dokumentet får du en bättre förståelse för hur du använder SQL för att skapa en profil och en datauppsättning som kan uppdateras baserat på härledda attribut. Du är nu redo att använda den här datauppsättningen med arbetsflöden för batchimport för att göra uppdateringar av dina profildata. Om du vill veta mer om inmatning av data i Adobe Experience Platform börjar du med att läsa [dataöverföring - översikt](../../../ingestion/home.md).
