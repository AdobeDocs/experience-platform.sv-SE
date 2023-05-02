---
solution: Experience Platform
title: Redigera målanslutningar med API:t för Flow Service
type: Tutorial
description: Lär dig hur du redigerar olika komponenter i en målanslutning med API:t för Flow Service.
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Redigera målanslutningar med API:t för Flow Service

I den här självstudiekursen beskrivs stegen för redigering av olika komponenter i en målanslutning. Lär dig hur du uppdaterar inloggningsuppgifter, exporterar plats med mera med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> De redigeringsåtgärder som beskrivs i den här självstudiekursen stöds för närvarande bara via API:t för Flow Service.

## Komma igång {#get-started}

Den här självstudien kräver att du har ett giltigt dataflödes-ID. Om du inte har något giltigt dataflödes-ID väljer du önskat mål på menyn [målkatalog](../catalog/overview.md) och följa de steg som beskrivs nedan för att [ansluta till målet](../ui/connect-destination.md) och [aktivera data](../ui/activation-overview.md) innan du provar den här självstudiekursen.

>[!NOTE]
>
> Villkoren *flöde* och *dataflöde* används omväxlande i den här självstudiekursen. I den här självstudiekursen har de samma betydelse.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna uppdatera ditt dataflöde med [!DNL Flow Service] API.

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i Experience Platform, inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om `x-sandbox-name` ingen rubrik har angetts, begäranden har lösts under `prod` sandlåda.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Söka efter dataflödesdetaljer {#look-up-dataflow-details}

Det första steget i att redigera målanslutningen är att hämta dataflödesinformation med ditt flödes-ID. Du kan visa den aktuella informationen om ett befintligt dataflöde genom att göra en GET-förfrågan till `/flows` slutpunkt.

>[!TIP]
>
>Du kan använda användargränssnittet i Experience Platform för att hämta det önskade dataflödes-ID:t för ett mål. Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** väljer du måldataflöde och söker efter mål-ID i den högra listen. Mål-ID är det värde som du kommer att använda som flödes-ID i nästa steg.
>
> ![Hämta mål-ID med Experience Platform-användargränssnittet](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API-format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för måldataflödet som du vill hämta. |

**Begäran**

Följande begäran hämtar information om ditt flödes-ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar aktuell information om dataflödet, inklusive version, unik identifierare (`id`) och annan relevant information. Det viktigaste för den här självstudiekursen är de ID:n för målanslutning och basanslutning som markeras i svaret nedan. Du använder dessa ID:n i nästa avsnitt för att uppdatera olika komponenter i målanslutningen.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Redigera målanslutningskomponenter (lagringsplats och andra komponenter) {#patch-target-connection}

Komponenterna för en målanslutning skiljer sig åt beroende på mål. Till exempel [!DNL Amazon S3] -mål kan du uppdatera den bucket och sökväg dit filerna exporteras. För [!DNL Pinterest] mål kan du uppdatera [!DNL Pinterest Advertiser ID] och for [!DNL Google Customer Match] du kan uppdatera [!DNL Pinterest Account ID].

Om du vill uppdatera komponenter för en målanslutning utför du en PATCH-begäran till `/targetConnections/{TARGET_CONNECTION_ID}` slutpunkt när du anger ditt anslutnings-ID, version och de nya värden som du vill använda. Kom ihåg att du fick ditt målanslutnings-ID i föregående steg när du inspekterade ett befintligt dataflöde till önskat mål.

>[!IMPORTANT]
>
>The `If-Match` måste anges när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av målanslutningen som du vill uppdatera. Taggen-värdet uppdateras med alla lyckade uppdateringar av en flödenhet som dataflöde, målanslutning och andra.
>
> Om du vill hämta den senaste versionen av taggvärdet gör du en GET-förfrågan till `/targetConnections/{TARGET_CONNECTION_ID}` slutpunkt, där `{TARGET_CONNECTION_ID}` är det målanslutnings-ID som du vill uppdatera.

Nedan visas några exempel på hur du uppdaterar parametrar i målanslutningsspecifikationen för olika typer av destinationer. Men den allmänna regeln för uppdatering av parametrar för alla mål är följande:

Hämta dataflödes-ID för anslutningen > hämta målanslutnings-ID > PATCH för målanslutningen med uppdaterade värden för de önskade parametrarna.

>[!BEGINSHADEBOX]

**API-format**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Begäran**

Följande begäran uppdaterar `bucketName` och `path` parametrar för en [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) målanslutning.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt målanslutnings-ID och en uppdaterad Etag. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt målanslutnings-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager och Google Ad Manager 360]

**Begäran**

Följande begäran uppdaterar parametrarna för en [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) eller [[!DNL Google Ad Manager 360] mål](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) anslutning för att lägga till den nya [**[!UICONTROL Append segment ID to segment name]**](/help/release-notes/2023/april-2023.md#destinations) fält.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt målanslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt målanslutnings-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Begäran**

Följande begäran uppdaterar `advertiserId` parameter för en [[!DNL Pinterest] målanslutning](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt målanslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt målanslutnings-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Redigera grundläggande anslutningskomponenter (autentiseringsparametrar och andra komponenter) {#patch-base-connection}

Komponenterna i en basanslutning skiljer sig åt beroende på mål. Till exempel [!DNL Amazon S3] mål kan du uppdatera åtkomstnyckeln och den hemliga nyckeln till [!DNL Amazon S3] plats.

Om du vill uppdatera komponenterna för en basanslutning utför du en PATCH-förfrågan till `/connections` slutpunkt när du anger ditt grundläggande anslutnings-ID, version och de nya värden som du vill använda.

Kom ihåg att du fick ditt grundläggande anslutnings-ID i ett tidigare steg när du inspekterade ett befintligt dataflöde till önskat mål.

>[!IMPORTANT]
>
>The `If-Match` måste anges när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av basanslutningen som du vill uppdatera. Värdet för etag uppdateras med varje lyckad uppdatering av en flödenhet, till exempel dataflöde, basanslutning och andra.
>
> Om du vill hämta den senaste versionen av Etag-värdet gör du en GET-förfrågan till `/connections/{BASE_CONNECTION_ID}` slutpunkt, där `{BASE_CONNECTION_ID}` är det grundläggande anslutnings-ID som du vill uppdatera.

Nedan visas några exempel på hur du uppdaterar parametrar i basanslutningsspecifikationen för olika typer av destinationer. Men den allmänna regeln för uppdatering av parametrar för alla mål är följande:

Hämta dataflödes-ID för anslutningen > hämta basanslutnings-ID > PATCH för basanslutningen med uppdaterade värden för de önskade parametrarna.

>[!BEGINSHADEBOX]

**API-format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Begäran**

Följande begäran uppdaterar `accessId` och `secretKey` parametrar för en [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) målanslutning.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt grundläggande anslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt grundläggande anslutnings-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Begäran**

Följande begäran uppdaterar parametrarna för en [[!DNL Azure Blob] mål](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) anslutning för att uppdatera den anslutningssträng som krävs för att ansluta till en Azure Blob-instans.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt grundläggande anslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt grundläggande anslutnings-ID.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudien följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](/help/landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](/help/landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen för mer information om hur du tolkar felsvar.

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du lärt dig hur du uppdaterar olika komponenter i en målanslutning med [!DNL Flow Service] API. Mer information om destinationer finns i [destinationer, översikt](../home.md).
