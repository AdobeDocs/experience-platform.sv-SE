---
keywords: Experience Platform;hem;populära ämnen;Google PubSub;google pubsub
solution: Experience Platform
title: Skapa en Google PubSub Source-anslutning med API:t för Flow Service
topic: översikt
type: Självstudiekurs
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google PubSub-konto med API:t för Flow Service.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Skapa en [!DNL Google PubSub]-källanslutning med API:t för Flow Service

>[!NOTE]
>
>[!DNL Google PubSub]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) för att vägleda dig genom stegen för att ansluta [!DNL Google PubSub] (kallas nedan &quot;[!DNL PubSub]&quot;) till Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL PubSub]-källanslutning med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL PubSub] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |

Mer information om dessa värden finns i följande [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication)-dokument.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL PubSub]-konto eftersom den kan användas för att skapa flera dataflöden för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL PubSub]-anslutning måste leverantörs-ID och anslutningsspecifikations-ID anges som en del av POSTEN. Leverantörs-ID är `521eee4d-8cbe-4906-bb48-fb6bd4450033` och anslutningsspecifikations-ID är `70116022-a743-464a-bbfe-e226a7f8210c`.

**API-format**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `auth.params.credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Svar**

Ett lyckat svar returnerar anslutnings-ID:t för den nyligen skapade [!DNL PubSub]-anslutningen. Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL PubSub]-anslutning med hjälp av API:t [!DNL Flow Service] och skaffat dess unika anslutnings-ID. Du kan använda detta anslutnings-ID för att [samla in strömmande data med API:t för flödestjänst](../../collect/streaming.md).
