---
title: Aktivera registrering av ändringsdata för källanslutningar i API
description: Lär dig hur du aktiverar registrering av ändringsdata för källanslutningar i API:t
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 192e97c97ffcb2d695bcfa6269cc6920f5440832
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 0%

---

# Aktivera registrering av ändringsdata för källanslutningar i API

Använd datainhämtning från Adobe Experience Platform för att synkronisera käll- och målsystemen i nära realtid.

Experience Platform har för närvarande stöd för **inkrementell datakopia**, som regelbundet överför nyligen skapade eller uppdaterade poster från källsystemet till inkapslade datauppsättningar. Den här metoden förlitar sig på en **tidsstämpelkolumn** för att spåra ändringar, men den identifierar inte borttagningar, vilket kan leda till inkonsekventa data över tid.

Om du däremot ändrar datainhämtningen hämtas och infogas, uppdateras och tas bort nästan i realtid. Denna omfattande ändringsspårning säkerställer att datauppsättningarna är helt anpassade till källsystemet och ger en fullständig ändringshistorik utöver vad inkrementell kopia stöder. Borttagningsåtgärder kräver dock särskild hänsyn eftersom de påverkar alla program som använder måldatauppsättningarna.

För registrering av ändringsdata i Experience Platform krävs **[Data Mirror](../../../xdm/data-mirror/overview.md)** med [modellbaserade scheman](../../../xdm/schema/model-based.md) (kallas även relationsscheman). Du kan skicka ändringsdata till Data Mirror på två sätt:

* **[Manuell ändringsspårning](#file-based-sources)**: Inkludera en `_change_request_type`-kolumn i datauppsättningen för källor som inte genererar poster för registrering av ändringsdata internt
* **[Inbyggd export av datainhämtning vid ändring](#database-sources)**: Använd poster för registrering av ändringsdata som exporterats direkt från källsystemet

Båda metoderna kräver att Data Mirror har modellbaserade scheman för att bevara relationer och genomdriva unika lösningar.

## Data Mirror med modellbaserade diagram

>[!AVAILABILITY]
>
>Data Mirror och modellbaserade scheman är tillgängliga för innehavare av Adobe Journey Optimizer **samordnade kampanjer**. De är också tillgängliga som en **begränsad version** för Customer Journey Analytics-användare, beroende på din licens och aktivering av funktioner. Kontakta din Adobe-representant för att få åtkomst.

>[!NOTE]
>
>**Orchestrerade kampanjanvändare**: Använd de Data Mirror-funktioner som beskrivs i det här dokumentet för att arbeta med kunddata som behåller referensintegriteten. Även om din källa inte använder formatering för registrering av ändringsdata, stöder Data Mirror relationsfunktioner som primärnyckel, postnivåuppdateringar och schemarelationer. Dessa funktioner säkerställer enhetlig och tillförlitlig datamodellering för alla anslutna datamängder.

Data Mirror använder modellbaserade scheman för att utöka datainhämtningen av ändringsdata och aktivera avancerade funktioner för databassynkronisering. En översikt över Data Mirror finns i [Data Mirror - översikt](../../../xdm/data-mirror/overview.md).

Modellbaserade scheman utökar Experience Platform för att framtvinga unika primärnycklar, spåra ändringar på radnivå och definiera relationer på schemanivå. Med datainhämtning kan man lägga in, uppdatera och radera data direkt i datasjön, vilket minskar behovet av Extract, Transform, Load (ETL) eller manuell avstämning.

Mer information finns i [Modellbaserade scheman - översikt](../../../xdm/schema/model-based.md).

### Modellbaserade schemakrav för registrering av ändringsdata

Konfigurera följande identifierare innan du använder ett modellbaserat schema med registrering av ändringsdata:

* Identifiera unikt varje post med en primärnyckel.
* Tillämpa uppdateringar sekventiellt med en versionsidentifierare.
* Lägg till en tidsstämpelidentifierare för tidsseriescheman.

### Styra kolumnhantering {#control-column-handling}

Använd kolumnen `_change_request_type` för att ange hur varje rad ska bearbetas:

* `u` — upsert (standard om kolumnen inte finns)
* `d` - ta bort

Den här kolumnen utvärderas endast vid förtäring och lagras eller mappas inte till XDM-fält.

### Arbetsflöde {#workflow}

Så här aktiverar du registrering av ändringsdata med ett modellbaserat schema:

1. Skapa ett modellbaserat schema.
2. Lägg till de beskrivningar som krävs:
   * [Primär nyckelbeskrivning](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Versionsbeskrivare](../../../xdm/api/descriptors.md#version-descriptor)
   * [Tidsstämpelbeskrivning](../../../xdm/api/descriptors.md#timestamp-descriptor) (endast tidsserie)
3. Skapa en datauppsättning från schemat och aktivera registrering av ändringsdata.
4. Endast för filbaserad inmatning: Lägg till kolumnen `_change_request_type` i källfilerna om du behöver ange borttagningsåtgärder explicit. CDC-exportkonfigurationer hanterar detta automatiskt för databaskällor.
5. Slutför konfigurationen av källanslutningen för att aktivera förtäring.

>[!NOTE]
>
>Kolumnen `_change_request_type` krävs bara för filbaserade källor (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) när du vill styra ändringsbeteendet på radnivå explicit. För databaskällor med inbyggda CDC-funktioner hanteras ändringsåtgärder automatiskt via CDC-exportkonfigurationer. Filbaserad inmatning förutsätter att du utför en överföring som standard. Du behöver bara lägga till den här kolumnen om du vill ange borttagningsåtgärder i filöverföringen.

>[!IMPORTANT]
>
>**Planering av borttagning av data krävs**. Alla program som använder modellbaserade scheman måste förstå borttagningskonsekvenserna innan ändringsdatainhämtningen implementeras. Planera för hur borttagningar påverkar relaterade datamängder, efterlevnadskrav och processerna längre fram i kedjan. Mer information finns i [Ta hänsyn till datahygien](../../../hygiene/ui/record-delete.md#model-based-record-delete).

## Erbjuda ändringsdata för filbaserade källor {#file-based-sources}

>[!IMPORTANT]
>
>Filbaserad datainhämtning av ändringsdata kräver Data Mirror med modellbaserade scheman. Innan du följer filformateringsstegen nedan kontrollerar du att du har slutfört det [Data Mirror-installationsarbetsflöde](#workflow) som beskrivs tidigare i det här dokumentet. Stegen nedan beskriver hur du formaterar dina datafiler så att de innehåller ändringsspårningsinformation som kommer att bearbetas av Data Mirror.

För filbaserade källor ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] och [!DNL SFTP]) tar du med en `_change_request_type`-kolumn i filerna.

Använd de `_change_request_type`-värden som definieras i avsnittet [Hantera kontrollkolumner](#control-column-handling) ovan.

>[!IMPORTANT]
>
>För **filbaserade källor endast** kan vissa program kräva en `_change_request_type`-kolumn med antingen `u` (upsert) eller `d` (delete) för att validera funktionerna för ändringsspårning. Adobe Journey Optimizer **orkestrerade kampanjer** kräver till exempel den här kolumnen för att aktivera alternativet för orkestrerad kampanj och tillåta val av datauppsättning för målinriktning. Programspecifika valideringskrav kan variera.

Följ de källspecifika stegen nedan.

### Lagringskällor i molnet {#cloud-storage-sources}

Aktivera datainhämtning för molnlagringskällor genom att följa dessa steg:

1. Skapa en basanslutning för källan:

   | Källa | Grundläggande anslutningsguide |
   |---|---|
   | [!DNL Amazon S3] | [Skapa en [!DNL Amazon S3] basanslutning](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Skapa en [!DNL Azure Blob] basanslutning](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Skapa en [!DNL Google Cloud Storage] basanslutning](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Skapa en [!DNL SFTP] basanslutning](../api/create/cloud-storage/sftp.md) |

2. [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).

Alla molnlagringskällor använder samma `_change_request_type`-kolumnformat som beskrivs i avsnittet [ Filbaserade källor ](#file-based-sources) ovan.

## Databaskällor {#database-sources}

### [!DNL Azure Databricks]

Om du vill använda registrering av ändringsdata med [!DNL Azure Databricks] måste du båda aktivera **Ändra datafeed** i källtabellerna och konfigurera Data Mirror med modellbaserade scheman i Experience Platform.

Använd följande kommandon om du vill aktivera dataöverföring i tabeller:

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

### [!DNL Data Landing Zone]

Om du vill använda registrering av ändringsdata med [!DNL Data Landing Zone] måste du båda aktivera **Ändra datafeed** i källtabellerna och konfigurera Data Mirror med modellbaserade scheman i Experience Platform.

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Data Landing Zone]-källanslutning:

* [Skapa en [!DNL Data Landing Zone] basanslutning](../api/create/cloud-storage/data-landing-zone.md).
* [Skapa en källanslutning för ett molnlagringsutrymme](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Om du vill använda registrering av ändringsdata med [!DNL Google BigQuery] måste du både aktivera ändringshistorik i källtabellerna och konfigurera Data Mirror med modellbaserade scheman i Experience Platform.

Om du vill aktivera ändringshistorik i [!DNL Google BigQuery]-källanslutningen navigerar du till [!DNL Google BigQuery]-sidan i [!DNL Google Cloud]-konsolen och anger `enable_change_history` som `TRUE`. Den här egenskapen aktiverar ändringshistorik för datatabellen.

Mer information finns i handboken om [språksatser för datadefinitioner i  [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Google BigQuery]-källanslutning:

* [Skapa en [!DNL Google BigQuery] basanslutning](../api/create/databases/bigquery.md).
* [Skapa en källanslutning för en databas](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Om du vill använda registrering av ändringsdata med [!DNL Snowflake] måste du båda aktivera **ändringsspårning** i källtabellerna och konfigurera Data Mirror med modellbaserade scheman i Experience Platform.

Aktivera ändringsspårning i [!DNL Snowflake] genom att använda `ALTER TABLE` och ange `CHANGE_TRACKING` som `TRUE`.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Mer information finns i [[!DNL Snowflake] handboken om hur du använder ändringssatsen](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Läs följande dokumentation om hur du aktiverar registrering av ändringsdata för din [!DNL Snowflake]-källanslutning:

* [Skapa en [!DNL Snowflake] basanslutning](../api/create/databases/snowflake.md).
* [Skapa en källanslutning för en databas](../api/collect/database-nosql.md#create-a-source-connection).
