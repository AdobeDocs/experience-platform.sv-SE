---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Apache Spark på Azure HDInsights-kontakten med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# Skapa en [!DNL Apache Spark] på [!DNL Azure] HDInsights-kontakten med [!DNL Flow Service] API

>[!NOTE]
>
>På- [!DNL Apache Spark] [!DNL Azure HDInsights] kontakten finns i beta. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom de steg som du ska koppla [!DNL Flow Service] till [!DNL Apache Spark] (kallas nedan&quot; [!DNL Azure HDInsights] &quot;)[!DNL Spark][!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Spark] med [!DNL Flow Service] API:t.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till [!DNL Spark]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Spark] servern. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Spark] servern. |
| `password` | Lösenordet som motsvarar användaren. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Spark] är: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Mer information om hur du kommer igång finns i [Spark-dokumentet](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Spark] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Spark] anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Spark] är `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Värden för [!DNL Spark] servern. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Spark] anslutning. |
| `auth.params.password` | Lösenordet som är kopplat till din [!DNL Spark] anslutning. |
| `connectionSpec.id` | ID för [!DNL Spark] anslutningsspecifikation: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Spark] anslutning med hjälp av [!DNL Flow Service] API:t och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar databaser med API:t](../../explore/database-nosql.md)för Flow Service.