---
keywords: Experience Platform;hem;populära ämnen;Oraclena objektlagring;oraclena objektlagring
solution: Experience Platform
title: Skapa en Oracle Object Storage-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Object Storage med API:t för Flow Service.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Skapa en [!DNL Oracle Object Storage] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Oracle Object Storage] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Object Storage] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta till [!DNL Oracle Object Storage]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUrl` | The [!DNL Oracle Object Storage] slutpunkt krävs för autentisering. Slutpunktsformatet är: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | The [!DNL Oracle Object Storage] ID för åtkomstnyckel krävs för autentisering. |
| `secretKey` | The [!DNL Oracle Object Storage] lösenord krävs för autentisering. |
| `bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. Bucket-namnet måste innehålla mellan 3 och 63 tecken, det måste börja och sluta med en bokstav eller en siffra och får bara innehålla gemena bokstäver, siffror eller bindestreck (`-`). Det går inte att formatera bucket-namnet som en IP-adress. |
| `folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Oracle Object Storage] är: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Mer information om hur du hämtar dessa värden finns i [Autentiseringsguide för Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Oracle Object Storage] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.serviceUrl` | The [!DNL Oracle Object Storage] slutpunkt krävs för autentisering. |
| `auth.params.accessKey` | The [!DNL Oracle Object Storage] ID för åtkomstnyckel krävs för autentisering. |
| `auth.params.secretKey` | The [!DNL Oracle Object Storage] lösenord krävs för autentisering. |
| `auth.params.bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. |
| `auth.params.folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |
| `connectionSpec.id` | The [!DNL Oracle Object Storage] anslutningsspec-ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Svar**

Ett lyckat svar returnerar anslutnings-ID:t för den nya anslutningen. Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Oracle Object Storage] anslutning med [!DNL Flow Service] API och har fått sitt unika anslutnings-ID. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
