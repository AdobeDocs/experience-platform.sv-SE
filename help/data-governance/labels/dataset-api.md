---
keywords: Experience Platform;hem;populära ämnen;datauppsättning api;hantera dataanvändning;dataanvändning api
solution: Experience Platform
title: Hantera dataanvändningsetiketter för datauppsättningar med API:er
description: Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---

# Hantera dataanvändningsetiketter för datauppsättningar med API:er

Med [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) kan du använda och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från [!DNL Catalog Service]-API:t som hanterar datauppsättningsmetadata.

>[!IMPORTANT]
>
>Användning av etiketter på datauppsättningsnivå stöds bara för datastyrningsanvändning. Om du försöker skapa åtkomstprinciper för data måste du [använda etiketter i schemat](../../xdm/tutorials/labels.md) som datauppsättningen baseras på. Mer information finns i översikten om [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md).

Det här dokumentet beskriver hur du hanterar etiketter för datauppsättningar och fält med hjälp av [!DNL Dataset Service API]. Anvisningar om hur du hanterar själva dataanvändningsetiketter med API-anrop finns i [etikettens slutpunktshandbok](../api/labels.md) för [!DNL Policy Service API].

## Komma igång

Innan du läser den här guiden följer du de steg som beskrivs i avsnittet [Komma igång](../../catalog/api/getting-started.md) i guiden för katalogutvecklare för att samla in de nödvändiga inloggningsuppgifterna för att ringa anrop till [!DNL Experience Platform] API:er.

För att kunna anropa slutpunkterna som beskrivs i det här dokumentet måste du ha det unika `id`-värdet för en specifik datauppsättning. Om du inte har det här värdet läser du i guiden [lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Söka efter etiketter för en datauppsättning {#look-up}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-begäran till [!DNL Dataset Service]-API:t.

**API-format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id`-värdet för datauppsättningen vars etiketter du vill söka efter. |

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

Du kan använda en uppsättning etiketter för en hel datauppsättning genom att tillhandahålla dem i nyttolasten för en POST- eller PUT-begäran till API:t [!DNL Dataset Service]. Begärandetexten är densamma för båda anropen. Du kan inte lägga till etiketter i enskilda datauppsättningsfält.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id`-värdet för datauppsättningen som du skapar etiketter för. |

**Begäran**

POST-begäran nedan i exemplet uppdaterar hela datauppsättningen med en `C1`-etikett. Fälten i nyttolasten är desamma som krävs för en PUT-begäran.

När API-anrop görs som uppdaterar de befintliga etiketterna för en datauppsättning (PUT), måste ett `If-Match`-huvud som anger den aktuella versionen av datauppsättningsetiketten i datauppsättningstjänsten inkluderas. För att förhindra datakonflikter uppdaterar tjänsten bara datauppsättningsentiteten om den inkluderade `If-Match`-strängen matchar den senaste versionstaggen som genererats av systemet för den datauppsättningen.

>[!NOTE]
>
>Om det finns etiketter för den aktuella datauppsättningen kan nya etiketter bara läggas till via en PUT-begäran, vilket kräver en `If-Match`-rubrik. När etiketter har lagts till i en datauppsättning måste det senaste `etag`-värdet uppdateras eller tas bort vid ett senare tillfälle<br>Innan du kör PUT-metoden måste du utföra en GET-begäran på datauppsättningsetiketterna. Se till att du bara uppdaterar de specifika fält som är avsedda att ändras i begäran, så att resten förblir oförändrad. Se även till att PUT-anropet behåller samma överordnade enheter som GET-anropet. Alla avvikelser resulterar i fel för kunden.

Om du vill hämta den senaste versionen av datauppsättningsetiketten skapar du en [GET-begäran](#look-up) till `/datasets/{DATASET_ID}/labels`-slutpunkten. Det aktuella värdet returneras i svaret under en `etag`-rubrik. När du uppdaterar befintliga datauppsättningsrubriker är det bästa sättet att först utföra en sökbegäran för datauppsättningen för att hämta det senaste `etag`-värdet innan du använder det värdet i `If-Match`-huvudet för din efterföljande PUT-begäran.

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
| `entityId.namespace` | Detta används för att undvika ID-kollisioner. `namespace` är `AEP`. |
| `entityId.id` | ID:t för resursen som uppdateras. Det här refererar till `datasetId`. |
| `entityId.type` | Typen för resursen som uppdateras. Det här kommer alltid att vara `dataset`. |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i hela datauppsättningen. |
| `parents` | Arrayen `parents` innehåller en lista med `entityId` som den här datauppsättningen kommer att ärva etiketter från. Datauppsättningar kan ärva etiketter från scheman och/eller datauppsättningar. |

**Svar**

Ett lyckat svar returnerar den uppdaterade uppsättningen etiketter för datauppsättningen.

>[!IMPORTANT]
>
>Egenskapen `optionalLabels` har tagits bort för användning med POST-begäranden. Det går inte längre att lägga till dataetiketter i datauppsättningsfält. En POST-åtgärd genererar ett fel om det finns ett `optionalLabel`-värde. Du kan emellertid ta bort etiketter från enskilda fält med hjälp av en PUT-begäran och egenskapen `optionalLabels`. Mer information finns i avsnittet [Ta bort etiketter från en datamängd](#remove).

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

Du kan ta bort tidigare använda fältetiketter genom att antingen uppdatera de befintliga `optionalLabels` värdena med en delmängd av de befintliga fältetiketterna eller genom att ta bort en tom lista helt. Gör en PUT-begäran till [!DNL Dataset Service]-API:t om att uppdatera eller ta bort etiketter som redan används.

>[!NOTE]
>
>Du kan helt ta bort en datamängds etiketter genom att ange en tom lista för parametern `labels`. Det är inte obligatoriskt för en datauppsättning att behålla etiketter.

**API-format**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id`-värdet för datauppsättningen som du skapar etiketter för. |

**Begäran**

The below dataset on which PUT operation is applied was C1 optionalLabel on properties/person/properties/address field and C1, C2 optionalLabels on /properties/person/properties/name/properties/fullName field. Efter placeringsåtgärden har det första fältet ingen etikett (C1-etiketten har tagits bort) och det andra fältet har bara C1-etikett (C2-etiketten har tagits bort)

I exemplet nedan används en PUT-begäran för att ta bort etiketter som lagts till i enskilda fält. Innan begäran gjordes användes etiketterna `C1` och `C2` för fältet `fullName`, och etiketten `address` användes redan för fältet `C1`. PUT-begäran åsidosätter de befintliga etiketterna `C1, C2` från fältet `fullName` med en `C1`-etikett som använder parametern `optionalLabels.labels`. Begäran åsidosätter även etiketten `C1` från fältet `address` med en tom uppsättning fältetiketter.

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
| `entityId` | Detta identifierar den specifika datauppsättningsentiteten som ska uppdateras. `entityId` måste innehålla följande tre värden:<br/><br/>`namespace`: Detta används för att undvika ID-kollisioner. `namespace` är `AEP`.<br/>`id`: ID:t för resursen som uppdateras. Det här refererar till `datasetId`.<br/>`type`: Typen för resursen som uppdateras. Det här kommer alltid att vara `dataset`. |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i hela datauppsättningen. |
| `parents` | Arrayen `parents` innehåller en lista med `entityId` som den här datauppsättningen kommer att ärva etiketter från. Datauppsättningar kan ärva etiketter från scheman och/eller datauppsättningar. |
| `optionalLabels` | Den här parametern används för att ta bort etiketter som tidigare använts i ett datauppsättningsfält. En lista över enskilda fält i datauppsättningen som du vill ta bort etiketterna från. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller [!DNL Experience Data Model] (XDM)-attributen för fältet. Följande tre egenskaper krävs:<ul><li><code>id</code>: URI <code>$id</code> värdet för schemat som är associerat med fältet.</li><li><code>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör ha formen av en av de giltiga <a href="../../xdm/api/getting-started.md#accept">Acceptera rubrikerna</a> för en XDM-sökningsbegäran.</li><li><code>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: Det här värdet måste innehålla en delmängd av de befintliga fältetiketterna eller vara tomt om du vill ta bort alla befintliga fältetiketter. PUT- eller POST-metoderna returnerar nu ett fel om fältet `optionalLabels` innehåller nya eller ändrade etiketter. |

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

Genom att läsa det här dokumentet har du lärt dig att hantera dataanvändningsetiketter för datauppsättningar och fält med API:t [!DNL Dataset Service]. Du kan nu definiera [dataanvändningsprinciper](../policies/overview.md) och [åtkomstkontrollprinciper](../../access-control/abac/ui/policies.md) baserat på de etiketter du har använt.

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform] finns i [översikten över datauppsättningar](../../catalog/datasets/overview.md).
