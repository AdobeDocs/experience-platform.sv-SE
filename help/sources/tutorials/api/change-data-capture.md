---
title: Aktivera registrering av ändringsdata för källanslutningar i API
description: Lär dig hur du aktiverar registrering av ändringsdata för källanslutningar i API:t
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Aktivera registrering av ändringsdata för källanslutningar i API

Att hämta in data i Adobe Experience Platform-källor är en funktion som du kan använda för att upprätthålla datasynkronisering i realtid mellan käll- och målsystemen.

För närvarande stöder Experience Platform **inkrementell datakopia**, vilket garanterar att nyligen skapade eller uppdaterade poster i källsystemet regelbundet kopieras till de inkapslade datauppsättningarna. Den här processen är beroende av att **tidsstämpelkolumnen** används, till exempel `LastModified`, för att spåra ändringar och för att **endast samla in nyligen infogade eller uppdaterade data**. Den här metoden tar dock inte hänsyn till borttagna poster, vilket kan leda till inkonsekvenser i data över tiden.

Med datainhämtning hämtar och tillämpar ett givet flöde alla ändringar, inklusive infogningar, uppdateringar och borttagningar. På samma sätt förblir Experience Platform datamängder helt synkroniserade med källsystemet.

Du kan använda registrering av ändringsdata för följande källor:

## [!DNL Amazon S3]

Kontrollera att `_change_request_type` finns i filen [!DNL Amazon S3] som du vill importera till Experience Platform. Dessutom måste du se till att följande giltiga värden finns med i filen:

* `u`: för infogningar och uppdateringar
* `d`: för borttagningar.

Om `_change_request_type` inte finns i filen används standardvärdet `u`.

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Amazon S3]-källanslutning:

* [Skapa en [!DNL Amazon S3] basanslutning](../api/create/cloud-storage/s3.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Kontrollera att `_change_request_type` finns i filen [!DNL Azure Blob] som du vill importera till Experience Platform. Dessutom måste du se till att följande giltiga värden finns med i filen:

* `u`: för infogningar och uppdateringar
* `d`: för borttagningar.

Om `_change_request_type` inte finns i filen används standardvärdet `u`.

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Azure Blob]-källanslutning:

* [Skapa en [!DNL Azure Blob] basanslutning](../api/create/cloud-storage/blob.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

Du måste aktivera **ändra datafeed** i din [!DNL Azure Databricks]-tabell för att kunna använda datainhämtning i din källanslutning.

Använd följande kommandon för att explicit aktivera alternativet för att ändra datafeed i [!DNL Azure Databricks]

**Ny tabell**

Om du vill använda datautmatning för ändring av en ny tabell måste du ange tabellegenskapen `delta.enableChangeDataFeed` till `TRUE` i kommandot `CREATE TABLE`.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Befintlig tabell**

Om du vill använda datautmatning för ändring av en befintlig tabell måste du ange tabellegenskapen `delta.enableChangeDataFeed` till `TRUE` i kommandot `ALTER TABLE`.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Alla nya tabeller**

Om du vill använda datafeed för ändring i alla nya tabeller måste du ange standardegenskaperna till `TRUE`.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Mer information finns i [[!DNL Azure Databricks] handboken om hur du aktiverar feed för ändringsdata](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Azure Databricks]-källanslutning:

* [Skapa en [!DNL Azure Databricks] basanslutning](../api/create/databases/databricks.md).
* [Skapa en källanslutning för en databas](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

Du måste aktivera **ändra datafeed** i din [!DNL Data Landing Zone]-tabell för att kunna använda datainhämtning i din källanslutning.

Använd följande kommandon för att explicit aktivera alternativet för att ändra datafeed i [!DNL Data Landing Zone].

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Data Landing Zone]-källanslutning:

* [Skapa en [!DNL Data Landing Zone] basanslutning](../api/create/cloud-storage/data-landing-zone.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Om du vill använda registrering av ändringsdata i [!DNL Google BigQuery]-källanslutningen. Navigera till din [!DNL Google BigQuery]-sida i [!DNL Google Cloud]-konsolen och ange `enable_change_history` som `TRUE`. Den här egenskapen aktiverar ändringshistorik för datatabellen.

Mer information finns i handboken om [språksatser för datadefinitioner i  [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Google BigQuery]-källanslutning:

* [Skapa en [!DNL Google BigQuery] basanslutning](../api/create/databases/bigquery.md).
* [Skapa en källanslutning för en databas](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Kontrollera att `_change_request_type` finns i filen [!DNL Google Cloud Storage] som du vill importera till Experience Platform. Dessutom måste du se till att följande giltiga värden finns med i filen:

* `u`: för infogningar och uppdateringar
* `d`: för borttagningar.

Om `_change_request_type` inte finns i filen används standardvärdet `u`.

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Google Cloud Storage]-källanslutning:

* [Skapa en [!DNL Google Cloud Storage] basanslutning](../api/create/cloud-storage/google.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Kontrollera att `_change_request_type` finns i filen [!DNL SFTP] som du vill importera till Experience Platform. Dessutom måste du se till att följande giltiga värden finns med i filen:

* `u`: för infogningar och uppdateringar
* `d`: för borttagningar.

Om `_change_request_type` inte finns i filen används standardvärdet `u`.

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL SFTP]-källanslutning:

* [Skapa en [!DNL SFTP] basanslutning](../api/create/cloud-storage/sftp.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Du måste aktivera **ändringsspårning** i [!DNL Snowflake]-tabellerna för att kunna använda ändringsdatainhämtning i källanslutningarna.

Aktivera ändringsspårning i [!DNL Snowflake] genom att använda `ALTER TABLE` och ange `CHANGE_TRACKING` som `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Mer information finns i [[!DNL Snowflake] handboken om hur du använder ändringssatsen](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Snowflake]-källanslutning:

* [Skapa en [!DNL Snowflake] basanslutning](../api/create/databases/snowflake.md).
* [Skapa en källanslutning för en databas](../api/collect/database-nosql.md#create-a-source-connection).

