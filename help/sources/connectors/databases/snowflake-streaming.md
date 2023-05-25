---
title: Översikt över källkopplingen för direktuppspelning i Snowflake
description: Lär dig hur du skapar en källanslutning och ett dataflöde för att importera strömmande data från din Snowflake-instans till Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# [!DNL Snowflake] direktuppspelningskälla

>[!IMPORTANT]
>
>* The [!DNL Snowflake] strömningskällan är i betaversion. Läs [Översikt över källor](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.
>* The [!DNL Snowflake] Källa för direktuppspelning finns i källkatalogen för kunder som har köpt Real-Time CDP Ultimate.


Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för strömning av data från en [!DNL Snowflake] databas.

## Förstå [!DNL Snowflake] direktuppspelningskälla

The [!DNL Snowflake] direktuppspelningskälla fungerar genom att data läses in med jämna mellanrum genom att en SQL-fråga körs och en utdatapost skapas för varje rad i den resulterande uppsättningen.

Genom att använda [!DNL Kafka Connect], [!DNL Snowflake] direktuppspelningskälla spårar den senaste posten som tas emot från varje tabell, så att den kan börja på rätt plats för nästa iteration. Källan använder den här funktionen för att filtrera data och bara hämta uppdaterade rader från en tabell i varje iteration.

## Förutsättningar

I följande avsnitt beskrivs de nödvändiga stegen som måste utföras innan du kan strömma data från [!DNL Snowflake] databas till Experience Platform:

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Snowflake]måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Det fullständiga kontonamnet som är kopplat till ditt [!DNL Snowflake] konto. En fullständigt kvalificerad [!DNL Snowflake] kontonamnet innehåller ditt kontonamn, din region och din molnplattform. Exempel, `cj12345.east-us-2.azure`. Mer information om kontonamn finns i [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| `database` | The [!DNL Snowflake] databasen innehåller de data som du vill ta med plattformen. |
| `username` | Användarnamnet för [!DNL Snowflake] konto. |
| `password` | Lösenordet för [!DNL Snowflake] användarkonto. |
| `role` | (Valfritt) En anpassad definierad roll som kan anges för en användare för en viss anslutning. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Snowflake] är `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Mer information om autentisering finns i [[!DNL Snowflake] dokument](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Konfigurera rollinställningar {#configure-role-settings}

Du måste konfigurera behörigheter för en roll, även om den allmänna standardrollen har tilldelats, så att källanslutningen kan komma åt den relevanta rollen [!DNL Snowflake] databas, schema och tabell. De olika behörigheterna för olika [!DNL Snowflake] Enheter är följande:

| [!DNL Snowflake] enhet | Kräv rollprivilegium |
| --- | --- |
| Lagerställe | ANVÄNDA |
| Databas | ANVÄNDNING |
| Schema | ANVÄNDNING |
| Tabell | MARKERA |

>[!NOTE]
>
>Automatiskt återupptagande och automatiskt uppehåll måste vara aktiverat i den avancerade inställningskonfigurationen för ditt lagerställe.

Mer information om roll- och behörighetshantering finns i [[!DNL Snowflake] API-referens](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Begränsningar och vanliga frågor {#limitations-and-frequently-asked-questions}

* Datagenomströmningen för [!DNL Snowflake] källan är 2 000 poster per sekund.
* Priset kan variera beroende på hur lång tid ett lagerställe är aktivt och storleken på lagerstället. För [!DNL Snowflake] källintegration, den minsta storleken, det x-lilla lagret är tillräckligt. Det rekommenderas att du aktiverar automatisk uppehåll så att lagerstället kan göra uppehåll när det inte används.
* The [!DNL Snowflake] hämtar nya data var 10:e sekund från databasen.
* Konfigurationsalternativ:
   * Du kan aktivera en `backfill` boolesk flagga för [!DNL Snowflake] när du skapar en källanslutning.
      * Om backfill är true anges värdet för timestamp.initial till 0. Detta innebär att data med en tidsstämpelkolumn som är större än 0 epok-tid hämtas.
      * Om backfill är inställd på false anges värdet för timestamp.initial till -1. Detta innebär att data med en tidsstämpelkolumn som är större än den aktuella tiden (den tid då källan börjar inhämta) hämtas.
   * Tidsstämpelkolumnen ska formateras som typ: `TIMESTAMP_LTZ` eller `TIMESTAMP_NTZ`. Om tidsstämpelkolumnen är inställd på `TIMESTAMP_NTZ`, ska typerna lagras i UTC-tid i databasen.

## Nästa steg

I följande självstudiekurs beskrivs hur du kopplar samman [!DNL Snowflake] direktuppspelningskälla till Experience Platform med API:

* [Strömma data från en [!DNL Snowflake] databas till Experience Platform med API:t för Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)

