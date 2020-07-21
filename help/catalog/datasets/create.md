---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en datauppsättning med API:er
topic: datasets
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---


# Skapa en datauppsättning med API:er

Det här dokumentet innehåller allmänna steg för att skapa en datauppsättning med hjälp av Adobe Experience Platform-API:er och fylla i datauppsättningen med hjälp av en fil.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Batchförtäring](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] gör att du kan importera data som gruppfiler.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API: [!DNL Platform] erna.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Självstudiekurs

För att kunna skapa en datauppsättning måste ett schema först definieras. Ett schema är en uppsättning regler som hjälper till att representera data. Förutom att beskriva datastrukturen ger scheman även begränsningar och förväntningar som kan tillämpas och användas för att validera data när de flyttas mellan system.

Med dessa standarddefinitioner kan data tolkas på ett enhetligt sätt, oavsett ursprung, och behovet av översättning mellan olika program försvinner. Mer information om att komponera scheman finns i guiden om [grunderna för schemakomposition](../../xdm/schema/composition.md)

## Söka efter ett datauppsättningsschema

Den här självstudiekursen börjar där API-självstudiekursen [för](../../xdm/tutorials/create-schema-api.md) schematabellen avslutas och använder det schema för lojalitetsmedlemmar som skapades under den självstudiekursen.

Om du inte har slutfört [!DNL Schema Registry] självstudiekursen kan du börja där och fortsätta med den här självstudiekursen bara när du har komponerat det schema som krävs.

Följande anrop kan användas för att visa det bonusmedlemsschema som du skapade under [!DNL Schema Registry] API-självstudiekursen:

**API-format**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektets format beror på vilket accepteringshuvud som skickades i begäran. Enskilda egenskaper i det här svaret har minimerats för utrymme.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Skapa en datauppsättning

Med bonusmedlemschemat på plats kan du nu skapa en datauppsättning som refererar till schemat.

**API-format**

```HTTP
POST /dataSets
```

**Begäran**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

>[!NOTE]
>
>I den här självstudien används [parquet](https://parquet.apache.org/documentation/latest/) -filformatet för alla dess exempel. Ett exempel som använder JSON-filformatet finns i utvecklarhandboken för [batchfrågor](../../ingestion/batch-ingestion/api-overview.md)

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som består av en array som innehåller ID:t för den nyskapade datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Skapa en batch

Innan du kan lägga till data i en datauppsättning måste du skapa en batch som är länkad till datauppsättningen. Batchen kommer sedan att användas för överföring.

**API-format**

```HTTP
POST /batches
```

**Begäran**

Begärandetexten innehåller ett&quot;datasetId&quot;-fält vars värde är det som `{DATASET_ID}` genererades i föregående steg.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som innehåller information om den nyligen skapade gruppen, inklusive dess `id`skrivskyddade, systemgenererade sträng.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Överför filer till en grupp

När du har skapat en ny batch för överföring kan du nu överföra filer till den specifika datauppsättningen. Det är viktigt att komma ihåg att du angav filformatet som parquet när du definierade datauppsättningen. Filerna som du överför måste därför ha det formatet.

>[!NOTE]
>
>Den största dataöverföringsfilen som stöds är 512 MB. Om datafilen är större än detta måste den delas upp i segment som inte är större än 512 MB för att kunna överföras en åt gången. Du kan överföra varje fil i samma grupp genom att upprepa det här steget för varje fil med samma batch-ID. Det finns ingen gräns för hur många filer du kan överföra som en del av en grupp.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BATCH_ID}` | The `id` of the batch you are uploading to. |
| `{DATASET_ID}` | Datamängden `id` som gruppen sparas i. |
| `{FILE_NAME}` | Namnet på filen som du överför. |

**Begäran**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Svar**

En överförd fil returnerar en tom svarstext och HTTP-status 200 (OK).

## Slutförande av signalbatch

När du har överfört alla datafiler till gruppen kan du signalera att gruppen är slutförd. Signaleringsslutförande gör att tjänsten skapar [!DNL Catalog] poster `DataSetFile` för de överförda filerna och associerar dem med den batch som genererats tidigare. Batchen har markerats som slutförd, vilket utlöser eventuella efterföljande flöden som sedan kan användas för de data som nu är tillgängliga. [!DNL Catalog]

**API-format**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beskrivning |
| --- | --- |
| `{BATCH_ID}` | The `id` of the batch you are marked as complete. |

**Begäran**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Svar**

En slutförd batch returnerar en tom svarstext och HTTP-status 200 (OK).

## Bildskärmsingång

Beroende på storleken på data tar batcharna olika lång tid att importera. Du kan övervaka statusen för en batch genom att lägga till en begärandeparameter som innehåller batchens ID till en `batch` `GET /batches` begäran. API:t avsöker datauppsättningen för batchstatus från att hämtas tills `status` i svaret anger att åtgärden har slutförts (&quot;lyckats&quot; eller&quot;misslyckats&quot;).

**API-format**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BATCH_ID}` | The `id` of the batch you want to monitor. |

**Begäran**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Svar**

Ett positivt svar returnerar ett objekt med dess `status` attribut som innehåller värdet `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Ett negativt svar returnerar ett objekt med värdet för `"failed"` i `"status"` attributet och innehåller alla relevanta felmeddelanden:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>Ett rekommenderat avsökningsintervall är två minuter.

## Läs data från datauppsättningen

Med batch-ID kan du använda API:t för dataåtkomst för att läsa tillbaka och verifiera alla filer som överförts till gruppen. Svaret returnerar en array som innehåller en lista med fil-ID:n, där var och en refererar till en fil i gruppen.

Du kan också använda API:t för dataåtkomst för att returnera namn, storlek i byte och en länk för att hämta filen eller mappen.

Detaljerade steg för hur du arbetar med API:t för dataåtkomst finns i [utvecklarhandboken](../../data-access/home.md)för dataåtkomst.

## Uppdatera datauppsättningsschemat

Du kan lägga till fält och lägga in ytterligare data i datauppsättningar som du har skapat. För att göra detta måste du först uppdatera schemat genom att lägga till ytterligare egenskaper som definierar nya data. Detta kan göras med PATCH- och/eller PUT-åtgärder för att uppdatera det befintliga schemat.

Mer information om hur du uppdaterar scheman finns i Utvecklarhandbok [för](../../xdm/api/getting-started.md)schemaregister-API.

När du har uppdaterat schemat kan du följa stegen i den här självstudiekursen igen för att importera nya data som följer det reviderade schemat.

Det är viktigt att komma ihåg att schemautvecklingen är enbart additiv, vilket innebär att du inte kan införa en brytningsändring i ett schema när det har sparats i registret och använts för datahämtning. Mer information om de bästa sätten att komponera schema för användning med Adobe Experience Platform finns i guiden om [grunderna för schemakomposition](../../xdm/schema/composition.md).