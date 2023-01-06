---
keywords: Experience Platform;hem;populära ämnen;datauppsättning api;hantera dataanvändning;dataanvändning api
solution: Experience Platform
title: Hantera dataanvändningsetiketter för datauppsättningar med API:er
description: Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Hantera dataanvändningsetiketter för datauppsättningar med API:er

The [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) gör att du kan använda och redigera användningsetiketter för datauppsättningar. Den är en del av Adobe Experience Platform funktioner för datakatalog, men skiljer sig från [!DNL Catalog Service] API som hanterar datauppsättningsmetadata.

>[!IMPORTANT]
>
>Användning av etiketter på datauppsättningsnivå stöds bara för datastyrningsanvändning. Om du försöker skapa åtkomstprofiler för data måste du [lägg till etiketter i schemat](../../xdm/tutorials/labels.md) som datauppsättningen baseras på. Se översikten på [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för mer information.

Det här dokumentet beskriver hur du hanterar etiketter för datauppsättningar och fält med hjälp av [!DNL Dataset Service API]. Anvisningar om hur du hanterar etiketter för dataanvändning i sig med API-anrop finns i [slutpunktshandbok för etiketter](../api/labels.md) för [!DNL Policy Service API].

## Komma igång

Innan du läser den här handboken följer du de steg som beskrivs i [komma igång, avsnitt](../../catalog/api/getting-started.md) i guiden för katalogutvecklare om du vill samla in de inloggningsuppgifter som krävs för att ringa till [!DNL Platform] API:er.

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

Du kan skapa en uppsättning etiketter för en datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran till [!DNL Dataset Service] API. Om du använder någon av dessa metoder skrivs befintliga etiketter över och ersätts med de som finns i nyttolasten.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning som du skapar etiketter för. |

**Begäran**

Exemplet på PUT-begäran nedan uppdaterar de befintliga etiketterna för en datauppsättning samt ett specifikt fält i den datauppsättningen. Fälten i nyttolasten är desamma som skulle behövas för en begäran om POST.

När API-anrop görs som uppdaterar befintliga etiketter för en datauppsättning (PUT), kan `If-Match` rubrik som anger den aktuella versionen av datauppsättningsetiketten i datauppsättningstjänsten måste inkluderas. För att förhindra datakonflikter uppdaterar tjänsten bara datauppsättningsentiteten om den inkluderade `If-Match` strängen matchar den senaste versionstaggen som genererats av systemet för den datauppsättningen.

>[!NOTE]
>
>Om det inte finns några etiketter för den aktuella datauppsättningen kan nya etiketter bara läggas till via en POST som inte kräver en `If-Match` header. När etiketterna har lagts till i en datauppsättning kan du `etag` tilldelas ett värde som kan användas för att uppdatera eller ta bort etiketterna vid ett senare tillfälle.

Om du vill hämta den senaste versionen av datauppsättningens etikett skapar du en [Begäran om GET](#look-up) till `/datasets/{DATASET_ID}/labels` slutpunkt. Det aktuella värdet returneras i svaret under ett `etag` header. När du uppdaterar befintliga datauppsättningsrubriker är det bästa sättet att först utföra en sökbegäran för datauppsättningen för att hämta den senaste `etag` värdet innan du använder värdet i `If-Match` huvud för din efterföljande begäran från PUT.

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
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i datauppsättningen. |
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som du vill lägga till etiketter i. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller [!DNL Experience Data Model] (XDM)-attribut för fältet. Följande tre egenskaper krävs:<ul><li>id</code>: URI $id</code> värdet för schemat som är associerat med fältet.</li><li>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör ha formatet en av de giltiga <a href="../../xdm/api/getting-started.md#accept">Acceptera sidhuvuden</a> för en XDM-sökningsbegäran.</li><li>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

**Svar**

Ett lyckat svar returnerar den uppdaterade uppsättningen etiketter för datauppsättningen.

```json
{
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
```

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att hantera dataanvändningsetiketter för datauppsättningar och fält med [!DNL Dataset Service] API. Nu kan du definiera [dataanvändningsprinciper](../policies/overview.md) och [åtkomstkontrollprinciper](../../access-control/abac/ui/policies.md) baserat på de etiketter du har använt.

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform], se [datauppsättningar, översikt](../../catalog/datasets/overview.md).
