---
keywords: Experience Platform;hem;populära ämnen;Microsoft SQL;microsoft sql;sql server;SQL server
solution: Experience Platform
title: Skapa en SQL Server-källanslutning med API:t för Flow Service
topic: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till en Microsoft SQL Server med API:t för Flow Service.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---


# Skapa en [!DNL Microsoft] SQL Server-källanslutning med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>SQL Server-kopplingen [!DNL Microsoft] är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t [!DNL Flow Service] för att vägleda dig genom stegen för att ansluta [!DNL Experience Platform] till en [!DNL Microsoft] SQL Server (nedan kallad SQL Server).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till SQL Server med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till SQL Server måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med ditt SQL Server-konto. SQL Server-anslutningssträngsmönstret är: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | Det ID som används för att skapa en anslutning. Det fasta anslutningens spec-ID för SQL Server är `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Mer information om hur du hämtar en anslutningssträng finns i [det här SQL Server-dokumentet](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per SQL Server-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att skapa en SQL Server-anslutning måste dess unika anslutningsspec-ID anges som en del av POSTEN. Anslutningens spec-ID för SQL Server är `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som är associerad med ditt SQL Server-konto. SQL Server-anslutningssträngsmönstret är: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | Anslutningens spec-ID för SQL-servern är: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska din databas i nästa självstudiekurs.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en SQL Server-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID i nästa självstudiekurs när du lär dig att [utforska databaser eller NoSQL-system med API:t för Flow Service](../../explore/database-nosql.md).
