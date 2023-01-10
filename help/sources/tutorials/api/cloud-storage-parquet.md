---
keywords: Experience Platform;hem;populära ämnen;datakällanslutning
solution: Experience Platform
title: Infoga parquet-data från ett tredjeparts molnlagringssystem med API:t för flödestjänsten
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att importera Apache Parquet-data från ett molnlagringssystem från en annan leverantör.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 1%

---

# Infoga Parquet-data från ett molnlagringssystem från tredje part med [!DNL Flow Service] API

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används [!DNL Flow Service] API för att vägleda dig genom stegen för att importera Parquet-data från ett molnlagringssystem från tredje part.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
- [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna importera Parquet-data från ett molnlagringsutrymme från tredje part med hjälp av [!DNL Flow Service] API.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

- `Content-Type: application/json`

## Skapa en anslutning

För att kunna importera Parquet-data med [!DNL Platform] API:er måste du ha en giltig anslutning för den molnlagringskälla från tredje part som du använder. Om du inte redan har en anslutning till det lagringsutrymme du vill arbeta med kan du skapa en genom följande självstudier:

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Hämta och lagra den unika identifieraren (`$id`) av anslutningen och gå sedan vidare till nästa steg i den här självstudiekursen.

## Skapa ett målschema

För att källdata ska kunna användas i [!DNL Platform]måste ett målschema också skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en [!DNL Platform] datauppsättning i vilken källdata finns.

Om du föredrar att använda användargränssnittet i [!DNL Experience Platform], [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md) innehåller stegvisa instruktioner för att utföra liknande åtgärder i Schemaredigeraren.

**API-format**

```http
POST /schemaregistry/tenant/schemas
```

**Begäran**

I följande exempelbegäran skapas ett XDM-schema som utökar XDM [!DNL Individual Profile] klassen.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Svar**

Ett lyckat svar returnerar information om det nyligen skapade schemat inklusive dess unika identifierare (`$id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa en källanslutning {#source}

När ett mål-XDM-schema har skapats kan en källanslutning skapas med hjälp av en POST-begäran till [!DNL Flow Service] API. En källanslutning består av en anslutning för API:t, ett källdataformat och en referens till det mål-XDM-schema som hämtades i föregående steg.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `baseConnectionId` | Anslutningen till API:t som representerar din molnlagring. |
| `data.schema.id` | The (`$id`) om mål-xdm-schemat hämtades i föregående steg. |
| `params.path` | Källfilens sökväg. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Lagra det här värdet som det krävs i senare steg för att skapa en målanslutning.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Skapa en datauppsättningsbasanslutning

För att kunna importera externa data till [!DNL Platform], en [!DNL Experience Platform] Datauppsättningsbasanslutningen måste först hämtas.

Om du vill skapa en datauppsättningsbasanslutning följer du de steg som beskrivs i [självstudiekurs om grundläggande dataanslutning](./create-dataset-base-connection.md).

Fortsätt att följa stegen som beskrivs i utvecklarhandboken tills du har skapat en datauppsättningsbasanslutning. Hämta och lagra den unika identifieraren (`$id`) och fortsätta att använda det som bas-anslutnings-ID i nästa steg för att skapa en målanslutning.

## Skapa en måldatauppsättning

En måldatauppsättning kan skapas genom att en POST till [Katalogtjänstens API](https://www.adobe.io/experience-platform-apis/references/catalog/), med ID:t för målschemat i nyttolasten.

**API-format**

```http
POST /catalog/dataSets
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schemaRef.id` | ID:t för ditt mål-XDM-schema. |

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den nya datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop. Lagra måldatauppsättnings-ID som det krävs i senare steg för att skapa en målanslutning och ett dataflöde.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Skapa en målanslutning {#target}

Du har nu unika identifierare för en datauppsättningsbasanslutning, ett målschema och en måldatauppsättning. Med dessa identifierare kan du skapa en målanslutning med [!DNL Flow Service] API för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```http
POST /targetConnections
```

**Begäran**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `baseConnectionId` | ID:t för datauppsättningsbasanslutningen. |
| `data.schema.id` | The `$id` av mål-XDM-schemat. |
| `params.dataSetId` | ID för måldatauppsättningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för ditt molnlagringsutrymme. |

**Svar**

Ett godkänt svar returnerar den nya målanslutningens unika identifierare (`id`). Lagra det här värdet som det behövs i senare steg.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Skapa ett dataflöde

Det sista steget mot att importera Parquet-data från ett molnlagringsutrymme från tredje part är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

- [Källanslutnings-ID](#source)
- [Målanslutnings-ID](#target)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

**API-format**

```http
POST /flows
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sourceConnectionIds` | Källanslutnings-ID som hämtades i ett tidigare steg. |
| `targetConnectionIds` | Målanslutnings-ID som hämtades i ett tidigare steg. |

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en källanslutning för att samla in Parquet-data från ditt molnlagringssystem från tredje part på schemalagd basis. Inkommande data kan nu användas av underordnade [!DNL Platform] tjänster som [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../data-science-workspace/home.md)
