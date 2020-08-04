---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Hantera dataanvändningsetiketter för datauppsättningar med API:er '
topic: developer guide
translation-type: tm+mt
source-git-commit: 2f35765c0dfadbfb4782b6c3904e33ae7a330b2f
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---


# Hantera dataanvändningsetiketter för datauppsättningar med API:er

Med [!DNL Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) den kan du använda och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från det API som hanterar [!DNL Catalog Service] datauppsättningsmetadata.

Det här dokumentet beskriver hur du hanterar etiketter för datauppsättningar och fält med hjälp av [!DNL Dataset Service API]. Anvisningar om hur du hanterar etiketter för dataanvändning i sig med API-anrop finns i [etikettens slutpunktshandbok](../api/labels.md) för [!DNL Policy Service API].

## Komma igång

Innan du läser den här handboken följer du de steg som beskrivs i avsnittet [](../../catalog/api/getting-started.md) Komma igång i guiden för katalogutvecklare för att samla in de nödvändiga inloggningsuppgifterna för att ringa anrop till [!DNL Platform] API:er.

För att kunna anropa slutpunkterna som beskrivs i det här dokumentet måste du ha det unika `id` värdet för en viss datauppsättning. Om du inte har det här värdet läser du i guiden om att [lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Söka efter etiketter för en datauppsättning {#look-up}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-begäran till [!DNL Dataset Service] API:t.

**API-format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för datauppsättningen vars etiketter du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar dataanvändningsetiketterna som har tillämpats på datauppsättningen.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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

Du kan skapa en uppsättning etiketter för en datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran till [!DNL Dataset Service] API:t. Om du använder någon av dessa metoder skrivs befintliga etiketter över och ersätts med de som finns i nyttolasten.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för datauppsättningen som du skapar etiketter för. |

**Begäran**

Följande begäran om POST lägger till en serie etiketter i datauppsättningen samt ett specifikt fält i datauppsättningen. Fälten i nyttolasten är desamma som skulle behövas för en PUT-begäran.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som du vill lägga till etiketter i. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller fältets [!DNL Experience Data Model] (XDM) attribut. Följande tre egenskaper krävs:<ul><li>id</code>: URI $id</code> -värdet för schemat som är associerat med fältet.</li><li>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör göras i form av en av de giltiga <a href="../../xdm/api/look-up-resource.md">Acceptera rubrikerna</a> för en XDM-sökningsbegäran.</li><li>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

**Svar**

Ett lyckat svar returnerar etiketterna som har lagts till i datauppsättningen.

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

## Ta bort etiketter från en datauppsättning {#remove}

Du kan ta bort etiketterna som används i en datauppsättning genom att göra en DELETE-begäran till [!DNL Dataset Service] API:t.

**API-format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för den datauppsättning vars etiketter du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar på HTTP-status 200 (OK), som anger att etiketterna har tagits bort. Du kan [slå upp befintliga etiketter](#look-up) för datauppsättningen i ett separat anrop för att bekräfta detta.

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att hantera dataanvändningsetiketter för datauppsättningar och fält med hjälp av [!DNL Dataset Service] API.

När du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till [!DNL Experience Platform]. Om du vill veta mer kan du börja med att läsa [dokumentationen](../../ingestion/home.md)för dataöverföring.

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i översikten över [dataanvändningsprinciper](../policies/overview.md).

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform]finns i [översikten över](../../catalog/datasets/overview.md)datauppsättningar.