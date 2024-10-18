---
title: Uppdatera konton med API:t för Flow Service
description: I den här självstudiekursen beskrivs stegen för hur du uppdaterar information och autentiseringsuppgifter för ett konto med API:t för Flow Service.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 9e1edaa4183a8025b8391f58d480063adc834616
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Uppdatera konton med API:t för Flow Service

Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för en befintlig basanslutning. [!DNL Flow Service] ger dig möjlighet att lägga till, redigera och ta bort information om en befintlig batch- eller direktuppspelningsanslutning, inklusive namn, beskrivning och autentiseringsuppgifter.

I den här självstudien beskrivs stegen för hur du uppdaterar information och autentiseringsuppgifter för en anslutning med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!TIP]
>
>Du behöver inte skapa en ny basanslutning när en uppdatering krävs. Alla ändringar du gör i din basanslutning återspeglas i det tillhörande dataflödet.

## Komma igång

Den här självstudien kräver att du har en befintlig anslutning och ett giltigt anslutnings-ID. Om du inte har någon befintlig anslutning väljer du källa bland [källorna i översikt](../../home.md) och följer instruktionerna innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Sök anslutningsinformation

Det första steget när du uppdaterar anslutningen är att hämta information om anslutningen med ditt anslutnings-ID. Om du vill hämta din anslutnings aktuella information skickar du en GET-förfrågan till [!DNL Flow Service]-API:t samtidigt som du anger anslutnings-ID:t för anslutningen som du vill uppdatera.

**API-format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Det unika `id`-värdet för anslutningen som du vill hämta. |

**Begäran**

Följande begäran hämtar information om din anslutning.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar aktuell information om anslutningen, inklusive autentiseringsuppgifter, unik identifierare (`id`) och version. Versionsvärdet krävs för att uppdatera anslutningen.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Uppdatera anslutning

Om du vill uppdatera anslutningsens namn, beskrivning och autentiseringsuppgifter utför du en PATCH-begäran till [!DNL Flow Service]-API:t och anger ditt anslutnings-ID, version och den nya informationen som du vill använda.

>[!IMPORTANT]
>
>Rubriken `If-Match` krävs när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av anslutningen som du vill uppdatera.

**API-format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Det unika `id`-värdet för anslutningen som du vill uppdatera. |

**Begäran**

Följande begäran innehåller ett nytt namn och en beskrivning samt en ny uppsättning autentiseringsuppgifter för att uppdatera anslutningen med.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera anslutningen. Åtgärderna omfattar: `add`, `replace` och `remove`. |
| `path` | Sökvägen till den parameter som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt anslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service]-API:t och samtidigt ange ditt anslutnings-ID.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du uppdaterat de autentiseringsuppgifter och den information som är kopplad till din anslutning med API:t [!DNL Flow Service]. Mer information om hur du använder källanslutningar finns i [källans översikt](../../home.md).
