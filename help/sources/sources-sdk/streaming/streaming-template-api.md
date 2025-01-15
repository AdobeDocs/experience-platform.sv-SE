---
title: Självbetjäningsmall för direktuppspelning av SDK API
description: Lär dig hur du hämtar strömmande data från en källa till Adobe Experience Platform med API:t för Flow Service.
exl-id: a06384a2-cd99-456d-9f00-babcf3f7b7d9
badge: Beta
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för att strömma *YOURCE*-data med API:t [!DNL Flow Service]

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från den här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Please ignore all instances of DNL on this page. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat den.*

## Översikt

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Ta med en länk till din produktdokumentationswebbplats för ytterligare läsning.*

>[!IMPORTANT]
>
>Den här källkopplingen och dokumentationssidan skapas och underhålls av *YOURSOURCE* -teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk eller e-postadress där du kan komma åt uppdateringar*.

## Förhandskrav

*Lägg till information i det här avsnittet om allt som kunderna behöver känna till innan de börjar konfigurera källan i Adobe Experience Platform användargränssnitt. Det här kan vara om:*

* *måste läggas till i en tillåtelselista*
* *krav för e-posthashning*
* *kontoinformation på din sida*
* *Så här hämtar du en API-nyckel för att ansluta till din plattform*

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta *YOURSOURCE* till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| *autentiseringsuppgifter en* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter två* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter tre* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |

Mer information om de här autentiseringsuppgifterna finns i *YOURSOURCE* -autentiseringsdokumentationen. *Lägg till en länk till din plattforms autentiseringsdokumentation här*.

### Integrera *DIN KÄLLA* med din webkrok

*Direktuppspelning av SDK kräver att din källa har stöd för webbböcker för att kunna kommunicera med Experience Platform. I det här avsnittet måste du ange de steg som användarna måste följa för att kunna integrera YOURSOURCE med en webkrok.*

## Anslut *DIN KÄLLA* till plattformen med API:t [!DNL Flow Service]

I följande självstudiekurs får du hjälp med att skapa en *YOURSOURCE* -källanslutning och skapa ett dataflöde för att överföra *YOURCE*-data till plattformen med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Skapa en källanslutning {#source-connection}

Skapa en källanslutning genom att göra en POST-förfrågan till [!DNL Flow Service]-API:t och ange källans anslutningsspec-ID, information som namn och beskrivning samt dataformatet.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för *YOURSOURCE*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de *YOURSOURCE*-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [schemats register-API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Skapa en måldatauppsättning {#target-dataset}

En måldatamängd kan skapas genom att utföra en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), som anger målschemats ID i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med hjälp av dessa identifierare kan du skapa en målanslutning med API:t [!DNL Flow Service] för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för *YOURSOURCE*:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på målanslutningen. Kontrollera att namnet på målanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om målanslutningen. |
| `description` | Ett valfritt värde som du kan inkludera för att ange mer information om målanslutningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar datasjön. Detta fasta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formatet för de *YOURSOURCE*-data som du vill hämta till plattformen. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |


**Svar**

Ett svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer. Detta uppnås genom att utföra en begäran om POST till [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) med datamappningar definierade i nyttolasten för begäran.

**API-format**

```http
POST /conversion/mappingSets
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdmSchema` | ID:t för [mål-XDM-schemat](#target-schema) genererades i ett tidigare steg. |
| `mappings.destinationXdmPath` | Mål-XDM-sökvägen dit källattributet mappas. |
| `mappings.sourceAttribute` | Källattributet som måste mappas till en mål-XDM-sökväg. |
| `mappings.identity` | Ett booleskt värde som anger om mappningsuppsättningen ska markeras för [!DNL Identity Service]. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta värde krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Skapa ett flöde {#flow}

Det sista steget mot att överföra data från *YOURSOURCE* till plattformen är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Source-anslutnings-ID](#source-connection)
* [Målanslutnings-ID](#target-connection)
* [Mappnings-ID](#mapping)

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
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på dataflödet. Kontrollera att namnet på dataflödet är beskrivande, eftersom du kan använda det för att söka efter information om dataflödet. |
| `description` | Ett valfritt värde som du kan inkludera för att få mer information om dataflödet. |
| `flowSpec.id` | Det ID för flödesspecifikation som krävs för att skapa ett dataflöde. Detta fasta ID är: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Motsvarande version av flödesspecifikations-ID. Standardvärdet är `1.0`. |
| `sourceConnectionIds` | [källanslutnings-ID](#source-connection) genererades i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target-connection) genererades i ett tidigare steg. |
| `transformations` | Den här egenskapen innehåller de olika omformningar som behövs för att dina data ska kunna användas. Den här egenskapen krävs när data som inte är XDM-kompatibla skickas till plattformen. |
| `transformations.name` | Det namn som tilldelats omformningen. |
| `transformations.params.mappingId` | [Mappnings-ID](#mapping) genererades i ett tidigare steg. |
| `transformations.params.mappingVersion` | Motsvarande version av mappnings-ID. Standardvärdet är `0`. |

**Svar**

Ett lyckat svar returnerar ID:t (`id`) för det nyskapade dataflödet. Du kan använda det här ID:t för att övervaka, uppdatera eller ta bort dataflödet.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Hämta din URL för direktuppspelningsslutpunkt

När dataflödet har skapats kan du nu hämta URL:en för direktuppspelningsslutpunkten. Du använder den här slutpunkts-URL:en för att prenumerera källan på en webkrok, vilket gör att källan kan kommunicera med Experience Platform.

Om du vill hämta URL:en för direktuppspelningsslutpunkten gör du en GET-förfrågan till `/flows`-slutpunkten och anger ID:t för dataflödet.

**API-format**

```http
GET /flows/{FLOW_ID}
```

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om ditt dataflöde, inklusive din slutpunkts-URL, markerad som `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## Bilaga

Följande avsnitt innehåller information om hur du övervakar, uppdaterar och tar bort dataflödet.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Fullständiga API-exempel finns i handboken om [att övervaka källans dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uppdatera ditt dataflöde

Uppdatera informationen om dataflödet, till exempel namn och beskrivning, samt körningsschema och associerade mappningsuppsättningar genom att göra en PATCH-begäran till `/flows`-slutpunkten i [!DNL Flow Service]-API:t, samtidigt som du anger ID:t för dataflödet. När du gör en PATCH-begäran måste du ange dataflödets unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken om att [uppdatera källkodsdataflöden med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uppdatera ditt konto

Uppdatera namn, beskrivning och autentiseringsuppgifter för källkontot genom att utföra en PATCH-begäran till [!DNL Flow Service]-API:t och ange ditt grundläggande anslutnings-ID som en frågeparameter. När du gör en PATCH-begäran måste du ange källkontots unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken [Uppdatera ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Ta bort ditt dataflöde

Ta bort dataflödet genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange ID:t för det dataflöde som du vill ta bort som en del av frågeparametern. Fullständiga API-exempel finns i guiden om att [ta bort dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Ta bort ditt konto

Ta bort ditt konto genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange det grundläggande anslutnings-ID:t för kontot som du vill ta bort. Fullständiga API-exempel finns i guiden om att [ta bort ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
