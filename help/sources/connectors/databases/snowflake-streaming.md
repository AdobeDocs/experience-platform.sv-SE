---
title: Snowflake Streaming Source Connector - översikt
description: Lär dig hur du skapar en källanslutning och ett dataflöde för att importera strömmande data från din Snowflake-instans till Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1510'
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

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Redshift] till Experience Platform med API:er eller användargränssnittet:

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Snowflake] måste du ange följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Fullständig kontoidentifierare (kontonamn eller kontopositionerare) för ditt [!DNL Snowflake]-konto har lagts till med suffixet `snowflakecomputing.com`. Kontots identifierare kan ha olika format: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (t.ex. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (t.ex. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (t.ex. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Mer information finns i [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |
| `database` | Databasen [!DNL Snowflake] innehåller de data som du vill hämta Experience Platform. |
| `username` | Användarnamnet för kontot [!DNL Snowflake]. |
| `password` | Lösenordet för användarkontot [!DNL Snowflake]. |
| `role` | (Valfritt) En anpassad definierad roll som kan anges för en användare för en viss anslutning. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Snowflake] är `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Autentisering med nyckelpar]

Om du vill använda autentisering med nyckelpar måste du generera ett 2 048-bitars RSA-nyckelpar och sedan ange följande värden när du skapar ett konto för [!DNL Snowflake]-källan.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](./snowflake.md#retrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| `privateKey` | Den [!DNL Base64-]kodade privata nyckeln för ditt [!DNL Snowflake]-konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. Läs guiden om att [hämta din [!DNL Snowflake] privata nyckel](./snowflake.md) om du vill ha mer information. |
| `passphrase` | Lösenfrasen är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| `database` | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguiden för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Hämta din kontoidentifierare {#retrieve-your-account-identifier}

Om du vill autentisera din [!DNL Snowflake]-instans med Experience Platform måste du hämta din kontoidentifierare från [!DNL Snowflake] UI-instrumentpanelen.

Följ de här stegen för att hitta din kontoidentifierare:

* Navigera till ditt konto på [[!DNL Snowflake] programmets gränssnittspanel](https://app.snowflake.com/).
* I den vänstra navigeringen väljer du **[!DNL Accounts]** följt av **[!DNL Active Accounts]** i sidhuvudet.
* Välj sedan informationsikonen och markera och kopiera domännamnet för den aktuella URL:en.

### Hämta din privata nyckel {#retrieve-your-private-key}

Om du tänker använda nyckelpars-autentisering för din [!DNL Snowflake]-anslutning måste du generera en privat nyckel innan du ansluter till Experience Platform.

>[!BEGINTABS]

>[!TAB Skapa en krypterad privat nyckel]

Kör följande kommando på terminalen för att generera din krypterade privata nyckel [!DNL Snowflake]:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Om det lyckas bör du få din privata nyckel i PEM-format.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Skapa en okrypterad privat nyckel]

Om du vill generera din okrypterade privata [!DNL Snowflake]-nyckel kör du följande kommando på terminalen:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Om det lyckas bör du få din privata nyckel i PEM-format.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

När du har genererat din privata nyckel kodar du den direkt i [!DNL Base64] utan att göra några ändringar i dess format eller innehåll. Kontrollera att det inte finns några extra blanksteg eller tomma rader (inklusive efterföljande radmatningar) i slutet av den privata nyckeln innan du kodar.

### Verifiera konfigurationer

Innan du kan skapa en källanslutning för dina [!DNL Snowflake]-data måste du också se till att följande konfigurationer uppfylls:

* Det standardlagerställe som tilldelats en viss användare måste vara samma som det lagerställe som du angav vid autentisering till Experience Platform.
* Den standardroll som tilldelats en viss användare måste ha tillgång till samma databas som du anger när du autentiserar dig för Experience Platform.

Så här verifierar du din roll och ditt lager:

* Välj **[!DNL Admin]** till vänster och välj sedan **[!DNL Users & Roles]**.
* Välj lämplig användare och markera sedan ellipserna (`...`) i det övre högra hörnet.
* Navigera till [!DNL Edit user] i fönstret [!DNL Default Role] som visas för att visa rollen som är associerad med den angivna användaren.
* I samma fönster går du till [!DNL Default Warehouse] för att visa det lagerställe som är associerat med den angivna användaren.

När kodningen är klar kan du sedan använda den [!DNL Base64]-kodade privata nyckeln på Experience Platform för att autentisera ditt [!DNL Snowflake]-konto.

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

## Konvertera Unix-tid till datumfält

[!DNL Snowflake Streaming] tolkar och skriver ` DATE`-fält som antalet dagar sedan Unix-epoken (1970-01-01). Värdet `DATE` betyder till exempel 1 januari 1970, medan värdet 1 betyder 2 januari 1970. När du förbereder filen för att skapa mappningar i källan [!DNL Snowflake Streaming] måste du därför se till att kolumnen `DATE` representeras som ett heltal.

Du kan använda [Data Prep-data och tidsfunktioner](../../../data-prep/functions.md#date-and-time-functions) för att konvertera Unix-tid till datumfält som kan importeras till Experience Platform. Exempel:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

I den här funktionen:

* `{DATE_COLUMN}` är datumkolumnen som innehåller epokdagens heltal.
* Om du multiplicerar med 8640000 konverteras epokdagarna till millisekunder.
* åååå-MM-dd anger önskat datumformat.

Med den här konverteringen kan du vara säker på att datumet visas korrekt i datauppsättningen.


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

>[!NOTE]
>
>När du har skapat eller uppdaterat ett dataflöde för direktuppspelning krävs en kort 5-minuters paus i datainmatningen för att förhindra eventuella fall av dataförlust eller dataförlust.

I följande självstudie beskrivs hur du ansluter [!DNL Snowflake]-strömningskällan till Experience Platform med API:t:

* [Direktuppspela data från en [!DNL Snowflake] databas till Experience Platform med API:t för Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Direktuppspela data från en [!DNL Snowflake] databas till Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt](../../tutorials/ui/create/databases/snowflake-streaming.md)
