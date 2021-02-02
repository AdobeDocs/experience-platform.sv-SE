---
keywords: Experience Platform;hem;populära ämnen;Apache hive;hive;Hive
solution: Experience Platform
title: Skapa en Apache Hive på Azure HDInsights-kontakten med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Apache Hive på Azure HDInsights till Experience Platform.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# Skapa en [!DNL Apache Hive] på [!DNL Azure HDInsights]-koppling med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>Anslutningen [!DNL Apache Hive] för [!DNL Azure HDInsights] är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t [!DNL Flow Service] för att vägleda dig genom stegen för att ansluta [!DNL Apache Hive] på [!DNL Azure HDInsights] till [!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Hive] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Hive] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adress eller värdnamn för [!DNL Hive]-servern. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Hive]-servern. |
| `password` | Lösenordet som motsvarar användaren. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Hive] är: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

Mer information om hur du kommer igång finns i [det här Hive-dokumentet](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

#### Läser exempel-API-anrop

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

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per Hive-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Hive]-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Hive] är `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som är associerad med ditt [!DNL Hive]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Hive]: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Hive]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig att [utforska databaser med API:t för Flow Service](../../explore/database-nosql.md).
