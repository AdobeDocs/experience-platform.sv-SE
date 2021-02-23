---
keywords: Experience Platform;hem;populära ämnen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Skapa en Oracle Object Storage-källanslutning med API:t för Flow Service
topic: översikt
type: Självstudiekurs
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Object Storage med API:t för Flow Service.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# Skapa en [!DNL Oracle Object Storage]-källanslutning med hjälp av API:t [!DNL Flow Service]

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) för att vägleda dig genom stegen för att ansluta Adobe Experience Platform till [!DNL Oracle Object Storage].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Object Storage] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Oracle Object Storage] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUrl` | Slutpunkten [!DNL Oracle Object Storage] krävs för autentisering. Slutpunktsformatet är: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Åtkomstnyckel-ID för [!DNL Oracle Object Storage] krävs för autentisering. |
| `secretKey` | Lösenordet [!DNL Oracle Object Storage] krävs för autentisering. |
| `bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. Bucketnamnet måste innehålla mellan tre och 63 tecken, det måste börja och sluta med en bokstav eller en siffra och får bara innehålla gemena bokstäver, siffror eller bindestreck (`-`). Det går inte att formatera bucket-namnet som en IP-adress. |
| `folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |

Mer information om hur du hämtar dessa värden finns i [Autentiseringsguiden för Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Oracle Object Storage]-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Oracle Object Storage]-anslutning måste dess unika anslutningsspec-ID anges som en del av POSTEN. Anslutningens spec-ID för [!DNL Oracle Object Storage] är `c85f9425-fb21-426c-ad0b-405e9bd8a46c`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.serviceUrl` | Slutpunkten [!DNL Oracle Object Storage] krävs för autentisering. |
| `auth.params.accessKey` | Åtkomstnyckel-ID för [!DNL Oracle Object Storage] krävs för autentisering. |
| `auth.params.secretKey` | Lösenordet [!DNL Oracle Object Storage] krävs för autentisering. |
| `auth.params.bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. |
| `auth.params.folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Svar**

Ett lyckat svar returnerar anslutnings-ID:t för den nya anslutningen. Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Oracle Object Storage]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått ett unikt anslutnings-ID. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för flödestjänst](../../explore/cloud-storage.md).