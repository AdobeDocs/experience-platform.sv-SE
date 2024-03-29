---
keywords: Experience Platform;hem;populära ämnen;datauppsättning api;hantera dataanvändning;dataanvändning api
solution: Experience Platform
title: Hantera dataanvändningsetiketter för datauppsättningar med API:er
description: Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 0%

---

# Hantera dataanvändningsetiketter för datauppsättningar med API:er

The [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) gör att du kan använda och redigera användningsetiketter för datauppsättningar. Den är en del av Adobe Experience Platform funktioner för datakatalog, men skiljer sig från [!DNL Catalog Service] API som hanterar datauppsättningsmetadata.

>[!IMPORTANT]
>
>Användning av etiketter på datauppsättningsnivå stöds bara för datastyrningsanvändning. Om du försöker skapa åtkomstprofiler för data måste du [lägg till etiketter i schemat](../../xdm/tutorials/labels.md) som datauppsättningen baseras på. Se översikten på [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för mer information.

Det här dokumentet beskriver hur du hanterar etiketter för datauppsättningar och fält med hjälp av [!DNL Dataset Service API]. Anvisningar om hur du hanterar etiketter för dataanvändning i sig med API-anrop finns i [slutpunktshandbok för etiketter](../api/labels.md) för [!DNL Policy Service API].

## Komma igång

Innan du läser den här handboken följer du de steg som beskrivs i [komma igång, avsnitt](../../catalog/api/getting-started.md) i guiden för katalogutvecklare om du vill samla in de inloggningsuppgifter som krävs för att ringa till [!DNL Platform] API.

För att kunna anropa slutpunkterna som beskrivs i det här dokumentet måste du ha den unika `id` värde för en specifik datamängd. Om du inte har det här värdet läser du i guiden [lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Söka efter etiketter för en datauppsättning {#look-up}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-förfrågan till [!DNL Dataset Service] API.

**API-format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning vars etiketter du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar dataanvändningsetiketterna som har tillämpats på datauppsättningen.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `labels` | En lista över dataanvändningsetiketter som har tillämpats på datauppsättningen. |
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som har dataanvändningsetiketter tillämpade på sig. |

## Tillämpa etiketter på en datauppsättning {#apply}

Du kan använda en uppsättning etiketter för en hel datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran för [!DNL Dataset Service] API. Begärandetexten är densamma för båda anropen. Du kan inte lägga till etiketter i enskilda datauppsättningsfält.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning som du skapar etiketter för. |

**Begäran**

I exempelbegäran nedan uppdateras hela datauppsättningen med en `C1` etikett. Fälten i nyttolasten är desamma som skulle behövas för en PUT-begäran.

När API-anrop görs som uppdaterar befintliga etiketter för en datauppsättning (PUT), kan `If-Match` rubrik som anger den aktuella versionen av datauppsättningsetiketten i datauppsättningstjänsten måste inkluderas. För att förhindra datakonflikter uppdaterar tjänsten bara datauppsättningsentiteten om den inkluderade `If-Match` strängen matchar den senaste versionstaggen som genererats av systemet för den datauppsättningen.

>[!NOTE]
>
>Om det finns etiketter för den aktuella datauppsättningen kan nya etiketter bara läggas till via en PUT-begäran, vilket kräver en `If-Match` header. När etiketterna har lagts till i en datauppsättning är den senaste `etag` värdet krävs för att uppdatera eller ta bort etiketterna vid ett senare tillfälle<br>Innan du kör metoden PUT måste du utföra en GET-begäran på datauppsättningsrubrikerna. Se till att du bara uppdaterar de specifika fält som är avsedda att ändras i begäran, så att resten förblir oförändrad. Se dessutom till att samtalet från PUT upprätthåller samma överordnade enheter som samtalet till GET. Alla avvikelser resulterar i fel för kunden.

Om du vill hämta den senaste versionen av datauppsättningens etikett skapar du en [Begäran om GET](#look-up) till `/datasets/{DATASET_ID}/labels` slutpunkt. Det aktuella värdet returneras i svaret under ett `etag` header. När du uppdaterar befintliga datauppsättningsrubriker är det bästa sättet att först utföra en sökbegäran för datauppsättningen för att hämta den senaste `etag` värdet innan du använder värdet i `If-Match` huvud för din efterföljande begäran från PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Egenskap | Beskrivning |
| --- | --- |
| `entityId` | Detta identifierar den specifika datauppsättningsentiteten som ska uppdateras. |
| `entityId.namespace` | Detta används för att undvika ID-kollisioner. The `namespace` är `AEP`. |
| `entityId.id` | ID:t för resursen som uppdateras. Detta avser `datasetId`. |
| `entityId.type` | Typen för resursen som uppdateras. Det här kommer alltid att `dataset`. |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i hela datauppsättningen. |
| `parents` | The `parents` arrayen innehåller en lista med `entityId`är att den här datauppsättningen ärver etiketter från. Datauppsättningar kan ärva etiketter från scheman och/eller datauppsättningar. |

**Svar**

Ett lyckat svar returnerar den uppdaterade uppsättningen etiketter för datauppsättningen.

>[!IMPORTANT]
>
>The `optionalLabels` egenskapen har tagits bort för användning med POST-begäranden. Det går inte längre att lägga till dataetiketter i datauppsättningsfält. En POST genererar ett fel om `optionalLabel` värdet finns. Du kan emellertid ta bort etiketter från enskilda fält med hjälp av en PUT-begäran och `optionalLabels` -egenskap. Mer information finns i avsnittet [ta bort etiketter från en datauppsättning](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Ta bort etiketter från en datauppsättning {#remove}

Du kan ta bort tidigare använda fältetiketter genom att antingen uppdatera de befintliga `optionalLabels` värden med en delmängd av de befintliga fältetiketterna, eller en tom lista som helt tar bort dem. Gör en PUT-förfrågan till [!DNL Dataset Service] API för att uppdatera eller ta bort tidigare använda etiketter.

**API-format**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning som du skapar etiketter för. |

**Begäran**

The below dataset on which PUT operation is applied was C1 optionalLabel on properties/person/properties/address field and C1, C2 optionalLabels on /properties/person/properties/name/properties/fullName field. Efter placeringsåtgärden har det första fältet ingen etikett (C1-etiketten har tagits bort) och det andra fältet har bara C1-etikett (C2-etiketten har tagits bort)

I exemplet nedan används en PUT-begäran för att ta bort etiketter som lagts till i enskilda fält. Innan begäran gjordes `fullName` fältet hade `C1` och `C2` använda etiketter och `address` fältet har redan `C1` etikett används. PUT-begäran åsidosätter befintliga etiketter `C1, C2` etiketter från `fullName` fält med en `C1` etikett med `optionalLabels.labels` parameter. Begäran åsidosätter även `C1` etikett från `address` fält med en tom uppsättning fältetiketter.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parameter | Beskrivning |
| --- | --- |
| `entityId` | Detta identifierar den specifika datauppsättningsentiteten som ska uppdateras. The `entityId` måste innehålla följande tre värden:<br/><br/>`namespace`: Detta används för att undvika ID-kollisioner. The `namespace` är `AEP`.<br/>`id`: ID för resursen som uppdateras. Detta avser `datasetId`.<br/>`type`: Typen för resursen som uppdateras. Det här kommer alltid att `dataset`. |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i hela datauppsättningen. |
| `parents` | The `parents` arrayen innehåller en lista med `entityId`är att den här datauppsättningen ärver etiketter från. Datauppsättningar kan ärva etiketter från scheman och/eller datauppsättningar. |
| `optionalLabels` | Den här parametern används för att ta bort etiketter som tidigare använts i ett datauppsättningsfält. En lista över enskilda fält i datauppsättningen som du vill ta bort etiketterna från. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller [!DNL Experience Data Model] (XDM)-attribut för fältet. Följande tre egenskaper krävs:<ul><li><code>id</code>: URI <code>$id</code> värdet för schemat som är associerat med fältet.</li><li><code>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör ha formen av en av de giltiga <a href="../../xdm/api/getting-started.md#accept">Acceptera sidhuvuden</a> för en XDM-sökningsbegäran.</li><li><code>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: Det här värdet måste innehålla en delmängd av de befintliga fältetiketterna eller vara tomt om du vill ta bort alla befintliga fältetiketter. PUT eller POST returnerar nu ett fel om `optionalLabels` har nya eller ändrade etiketter. |

**Svar**

Ett lyckat svar returnerar den uppdaterade uppsättningen etiketter för datauppsättningen.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att hantera dataanvändningsetiketter för datauppsättningar och fält med [!DNL Dataset Service] API. Nu kan du definiera [dataanvändningsprinciper](../policies/overview.md) och [åtkomstkontrollprinciper](../../access-control/abac/ui/policies.md) baserat på de etiketter du har använt.

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform], se [datauppsättningar, översikt](../../catalog/datasets/overview.md).
