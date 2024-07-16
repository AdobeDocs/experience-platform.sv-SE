---
title: Snowflake Streaming Source Connector - översikt
description: Lär dig hur du skapar en källanslutning och ett dataflöde för att importera strömmande data från din Snowflake-instans till Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# [!DNL Snowflake] direktuppspelningskälla

>[!IMPORTANT]
>
>* Strömningskällan [!DNL Snowflake] är i betaversion. Läs [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.
>* Direktuppspelningskällan [!DNL Snowflake] är tillgänglig i API:t för användare som har köpt Real-time Customer Data Platform Ultimate.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder direktuppspelning av data från en [!DNL Snowflake]-databas.

## Förstå den strömmande källan [!DNL Snowflake]

Strömmande [!DNL Snowflake]-källa fungerar genom att data läses in genom att en SQL-fråga körs regelbundet och en utdatapost skapas för varje rad i den resulterande uppsättningen.

Genom att använda [!DNL Kafka Connect] spårar den [!DNL Snowflake]-direktuppspelningskällan den senaste posten som den tar emot från varje tabell, så att den kan börja på rätt plats för nästa iteration. Källan använder den här funktionen för att filtrera data och bara hämta uppdaterade rader från en tabell i varje iteration.

## Förhandskrav

I följande avsnitt beskrivs de nödvändiga stegen som måste utföras innan du kan strömma data från din [!DNL Snowflake]-databas till Experience Platform:

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Snowflake] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Det fullständiga kontonamnet som är kopplat till ditt [!DNL Snowflake]-konto. Ett fullständigt kvalificerat [!DNL Snowflake]-kontonamn innehåller ditt kontonamn, din region och din molnplattform. Exempel: `cj12345.east-us-2.azure`. Mer information om kontonamn finns i [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| `database` | Databasen [!DNL Snowflake] innehåller de data som du vill ta med plattformen. |
| `username` | Användarnamnet för kontot [!DNL Snowflake]. |
| `password` | Lösenordet för användarkontot [!DNL Snowflake]. |
| `role` | (Valfritt) En anpassad definierad roll som kan anges för en användare för en viss anslutning. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Snowflake] är `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |


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
* [Strömma data från en [!DNL Snowflake] databas till Experience Platform med hjälp av källarbetsytan i användargränssnittet i Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
