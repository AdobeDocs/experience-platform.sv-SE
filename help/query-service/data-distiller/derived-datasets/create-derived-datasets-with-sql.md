---
title: Skapa härledda datauppsättningar med SQL
description: Lär dig hur du använder SQL för att skapa en härledd datauppsättning som är aktiverad för profilen och hur du använder datauppsättningen för kundprofil och segmenteringstjänst i realtid.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Skapa härledda datauppsättningar med SQL

Lär dig hur du använder SQL-frågor för att hantera och omvandla data från befintliga datauppsättningar och skapa en härledd datauppsättning som är aktiverad för profilen. Det här arbetsflödet är ett effektivt, alternativt sätt att skapa härledda datauppsättningar för era affärssituationer med kundprofiler i realtid.

I det här dokumentet beskrivs olika praktiska SQL-tillägg som genererar en härledd datauppsättning som kan användas med kundprofilen i realtid. Arbetsflödet förenklar den process som du annars skulle behöva utföra via olika API-anrop eller interaktioner för plattformsgränssnitt.

Generering och publicering av en härledd datauppsättning för kundprofil i realtid omfattar vanligtvis följande steg:

* Skapa ett identitetsnamnutrymme, om det inte redan finns ett.
* Skapa datatypen för att lagra den härledda datauppsättningen, om det behövs.
* Skapa en fältgrupp med den datatypen för att lagra den härledda datauppsättningsinformationen.
* Skapa eller tilldela en primär identitetskolumn med namnutrymmet som skapades tidigare.
* Skapa ett schema med fältgruppen och datatypen som skapades tidigare.
* Skapa en ny datauppsättning med ditt schema och aktivera den för profil, om det behövs.
* Du kan också markera en datauppsättning som profilaktiverad.

När du har slutfört stegen ovan kan du fylla i datauppsättningen. Om du har aktiverat datauppsättningen för profilen kan du även skapa segment som refererar till den nya datauppsättningen och börja skapa insikter.

Med frågetjänsten kan du utföra alla åtgärder som listas ovan med hjälp av SQL-frågor. Detta inkluderar att vid behov göra ändringar i datauppsättningar och fältgrupper.

## Skapa en tabell med ett alternativ för att aktivera den för profilen {#enable-dataset-for-profile}

>[!NOTE]
>
>SQL-frågan som anges nedan förutsätter att ett befintligt namnutrymme används.

Använd en CTAS-fråga (Create Table as Select) för att skapa en datauppsättning, tilldela datatyper, ange en primär identitet, skapa ett schema och markera den som profilaktiverad. SQL-satsen nedan skapar en datauppsättning och gör den tillgänglig för Real-time Customer Data Platform (Real-Time CDP). SQL-frågan kommer att följa formatet som visas i exemplet nedan:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

De datatyper som stöds är: boolesk, date, datetime, text, float, bigint, integer, map, array och structure/row.

SQl-kodlåset nedan innehåller exempel på hur du definierar datatyperna structure/row, map och array. Rad ett visar radsyntaxen. Rad två demonstrerar mappningssyntax och rad tre, matrissyntax.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Datamängder kan också aktiveras för profiler via plattformens användargränssnitt. Mer information om hur du markerar en datauppsättning som aktiverad för profil finns i [aktivera en datauppsättning för dokumentation av kundprofiler i realtid](../../../catalog/datasets/user-guide.md#enable-profile).

I exempelfrågan nedan skapas datamängden `decile_table` med `id` som primär identitetskolumn och har namnutrymmet `IDFA`. Den har också ett fält med namnet `decile1Month` för mappningsdatatypen. Tabellen som skapades (`decile_table`) är aktiverad för profilen.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

När frågan har körts returneras datauppsättnings-ID:t till konsolen, vilket visas i exemplet nedan.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Använd `label='PROFILE'` på ett `CREATE TABLE`-kommando för att skapa en profilaktiverad datauppsättning. Funktionen `upsert` är aktiverad som standard. Funktionen `upsert` kan skrivas över med kommandot `ALTER`, vilket visas i exemplet nedan.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Mer information om hur du använder kommandot [ALTER TABLE](../../sql/syntax.md#alter-table) och etiketten [som en del av en CTAS-fråga](../../sql/syntax.md#create-table-as-select) finns i dokumentationen för SQl-syntaxen.

## Konstruerar för hantering av härledda datauppsättningar via SQL

De funktioner som beskrivs nedan är till stor nytta när du hanterar härledda datauppsättningar via SQL.

### Ändra befintliga datauppsättningar som ska aktiveras för profilen {#enable-existing-dataset-for-profile}

SQL-konstruktionen ALTER TABLE kan användas för att göra befintliga datauppsättningar aktiverade för profilen. Detta kräver att en profilaktiverad tagg läggs till både i schemat och i motsvarande datauppsättning.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Konsolen returnerar `ALTER SUCCESS` när kommandot `ALTER TABLE` har körts.

### Lägga till en primär identitet i en befintlig datauppsättning {#add-primary-identity}

Markera en befintlig kolumn i en datauppsättning som en primär identitetsuppsättning, annars uppstår ett fel. Om du vill ange en primär identitet med SQL använder du frågeformatet som visas nedan.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Exempel:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

I det angivna exemplet är `id2` en befintlig kolumn i `test1_dataset`.

### Inaktivera en datauppsättning för profil {#disable-dataset-for-profile}

Om du vill inaktivera tabellen för profilanvändning måste du använda kommandot DROP. Ett exempel på en SQL-sats som ANVÄNDS `DROP` visas nedan.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Exempel:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Den här SQL-satsen är ett effektivt alternativ till att använda ett API-anrop. Mer information finns i dokumentationen om hur du [inaktiverar en datauppsättning för användning med Real-Time CDP via API:t för datauppsättningar](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

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

Den här SQL-satsen är ett effektivt alternativ till att använda ett API-anrop. Mer information finns i dokumentationen om hur du [aktiverar en datauppsättning för användning med Real-Time CDP och UPSERT med API:t för datauppsättningar](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

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

Ytterligare metadata sparas för profilaktiverade datauppsättningar. Använd kommandot `SHOW TABLES` om du vill visa en extra `labels`-kolumn som ger information om etiketter som är associerade med tabeller.

Ett exempel på det här kommandots utdata visas nedan:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

I exemplet kan du se att `table_with_a_decile` har aktiverats för profilen och tillämpats med etiketter som [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) som beskrivits ovan.

### Skapa en fältgrupp med SQL

Fältgrupper kan nu skapas med hjälp av SQL. Detta är ett alternativ till att använda Schemaredigeraren i plattformsgränssnittet eller göra ett API-anrop till schemaregistret.

Ett exempel på hur du skapar en fältgrupp visas nedan.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Det går inte att skapa fältgrupper via SQL om flaggan `label` inte anges i satsen eller om fältgruppen redan finns.
>Kontrollera att frågan innehåller en `IF NOT EXISTS`-sats för att undvika att frågan misslyckas eftersom fältgruppen redan finns.

Ett verkligt exempel kan se ut ungefär som det nedan.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Den här satsen returnerar det skapade fältgrupps-ID:t. Till exempel `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Mer information om alternativa metoder finns i dokumentationen om hur du [skapar en ny fältgrupp i Schemaredigeraren](../../../xdm/ui/resources/field-groups.md#create) eller om hur du använder [schemaregistrets API](../../../xdm/api/field-groups.md#create).

### Släpp en fältgrupp

Ibland kan det vara nödvändigt att ta bort en fältgrupp från schemaregistret. Detta görs genom att köra kommandot `DROP FIELDGROUP` med fältgrupps-ID:t.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Exempel:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Borttagning av en fältgrupp via SQL misslyckas om fältgruppen inte finns. Kontrollera att satsen innehåller en `IF EXISTS`-sats för att undvika att frågan misslyckas.

### Visa alla fältgruppsnamn och ID:n för tabellerna

Kommandot `SHOW FIELDGROUPS` returnerar en tabell som innehåller tabellens namn, fältgrupp-ID och ägare.

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

När du har läst det här dokumentet får du en bättre förståelse för hur du använder SQL för att skapa en profil och en datauppsättning som kan uppdateras baserat på härledda datauppsättningar. Du är nu redo att använda den här datauppsättningen med arbetsflöden för batchimport för att göra uppdateringar av dina profildata. Om du vill veta mer om hur du importerar data till Adobe Experience Platform börjar du med att läsa översikten över [dataimporten](../../../ingestion/home.md).
