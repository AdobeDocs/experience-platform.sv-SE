---
title: Snowflake Streaming Source Connector - översikt
description: Lär dig hur du skapar en källanslutning och ett dataflöde för att importera strömmande data från din Snowflake-instans till Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# [!DNL Snowflake] direktuppspelningskälla

>[!IMPORTANT]
>
>* Direktuppspelningskällan [!DNL Snowflake] är tillgänglig i API:t för användare som har köpt Real-Time CDP Ultimate.
>
>* Du kan nu använda strömningskällan [!DNL Snowflake] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).


Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för strömning av data från en [!DNL Snowflake]-databas.

## Förstå den strömmande källan [!DNL Snowflake]

Strömmande [!DNL Snowflake]-källa fungerar genom att data läses in genom att en SQL-fråga körs regelbundet och en utdatapost skapas för varje rad i den resulterande uppsättningen.

Genom att använda [!DNL Kafka Connect] spårar den [!DNL Snowflake]-direktuppspelningskällan den senaste posten som den tar emot från varje tabell, så att den kan börja på rätt plats för nästa iteration. Källan använder den här funktionen för att filtrera data och bara hämta uppdaterade rader från en tabell i varje iteration.

## Förhandskrav

I följande avsnitt beskrivs de nödvändiga stegen som måste utföras innan du kan strömma data från din [!DNL Snowflake]-databas till Experience Platform:

### Uppdatera din IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources).

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Redshift] till Experience Platform med API:er eller användargränssnittet:

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Snowflake] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Fullständig kontoidentifierare (kontonamn eller kontopositionerare) för ditt [!DNL Snowflake]-konto har lagts till med suffixet `snowflakecomputing.com`. Kontots identifierare kan ha olika format: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (t.ex. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (t.ex. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (t.ex. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Mer information finns i [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |
| `database` | Databasen [!DNL Snowflake] innehåller de data som du vill hämta Experience Platform. |
| `username` | Användarnamnet för kontot [!DNL Snowflake]. |
| `password` | Lösenordet för användarkontot [!DNL Snowflake]. |
| `role` | (Valfritt) En anpassad definierad roll som kan anges för en användare för en viss anslutning. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Snowflake] är `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

### Konfigurera rollinställningar {#configure-role-settings}

Du måste konfigurera behörigheter för en roll, även om den allmänna standardrollen har tilldelats, så att källanslutningen kan komma åt den relevanta [!DNL Snowflake]-databasen, det aktuella -schemat och den aktuella tabellen. De olika behörigheterna för olika [!DNL Snowflake]-entiteter är följande:

| [!DNL Snowflake]-entitet | Kräv rollprivilegium |
| --- | --- |
| Lagerställe | ANVÄNDA |
| Databas | ANVÄNDNING |
| Schema | ANVÄNDNING |
| Tabell | MARKERA |

>[!NOTE]
>
>Automatiskt återupptagande och automatiskt uppehåll måste vara aktiverat i den avancerade inställningskonfigurationen för ditt lagerställe.

Mer information om roll- och behörighetshantering finns i [[!DNL Snowflake] API-referensen](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Begränsningar och vanliga frågor {#limitations-and-frequently-asked-questions}

* Datagenomströmningen för källan [!DNL Snowflake] är 2 000 poster per sekund.
* Priset kan variera beroende på hur lång tid ett lagerställe är aktivt och storleken på lagerstället. För [!DNL Snowflake]-källintegreringen räcker det med det minsta lagret med x-small. Det rekommenderas att du aktiverar automatisk uppehåll så att lagerstället kan göra uppehåll när det inte används.
* [!DNL Snowflake]-källan avsöker databasen efter nya data var 10:e sekund.
* Konfigurationsalternativ:
   * Du kan aktivera en `backfill` boolesk flagga för [!DNL Snowflake]-källan när du skapar en källanslutning.
      * Om backfill är true anges värdet för timestamp.initial till 0. Detta innebär att data med en tidsstämpelkolumn som är större än 0 epok-tid hämtas.
      * Om backfill är inställd på false anges värdet för timestamp.initial till -1. Detta innebär att data med en tidsstämpelkolumn som är större än den aktuella tiden (den tid då källan börjar inhämta) hämtas.
   * Tidsstämpelkolumnen ska formateras som typen: `TIMESTAMP_LTZ` eller `TIMESTAMP_NTZ`. Om tidsstämpelkolumnen är inställd på `TIMESTAMP_NTZ`, ska motsvarande tidszon som värdena lagras i skickas via parametern `timezoneValue`. Om det inte anges används UTC som standard.
      * `TIMESTAMP_TZ` kan inte användas som en tidsstämpelkolumn eller i en mappning.

## Nästa steg

I följande självstudie beskrivs hur du ansluter [!DNL Snowflake]-strömningskällan till Experience Platform med API:t:

* [Direktuppspela data från en [!DNL Snowflake] databas till Experience Platform med API:t för Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Direktuppspela data från en [!DNL Snowflake] databas till Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt](../../tutorials/ui/create/databases/snowflake-streaming.md)
