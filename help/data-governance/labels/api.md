---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Hantera dataanvändningsetiketter med API:er '
topic: developer guide
translation-type: tm+mt
source-git-commit: d685f1851badf54ce1d1ac3cbacd69d62894c33f

---


# Hantera dataanvändningsetiketter med API:er

Det här dokumentet innehåller steg för hur du hanterar dataanvändningsetiketter på data- och fältnivå med hjälp av katalogtjänstens API.

## Komma igång

Innan du läser den här guiden rekommenderar vi att du läser översikten [över](../../catalog/home.md) katalogtjänsten för att få en mer robust introduktion till tjänsten. Dessutom måste du följa de steg som beskrivs i avsnittet [](../../catalog/api/getting-started.md) Komma igång i guiden för katalogutvecklare för att samla in de inloggningsuppgifter som krävs för att ringa anrop till katalog-API:t.

För att kunna anropa slutpunkterna som beskrivs i avsnitten nedan måste du ha det unika `id` värdet för en viss datauppsättning. Om du inte har det här värdet läser du i utvecklarguiden om [att lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Söka efter etiketter för en datauppsättning {#lookup}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-begäran.

**API-format**

```http
GET /dataSets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för datauppsättningen vars etiketter du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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

## Tillämpa etiketter på en datauppsättning

Du kan skapa en uppsättning etiketter för en datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran. Om du använder någon av dessa metoder skrivs befintliga etiketter över och ersätts med de som finns i nyttolasten.

**API-format**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för datauppsättningen som du skapar etiketter för. |

**Begäran**

Följande POST-begäran lägger till en serie etiketter i datauppsättningen samt ett specifikt fält i den datauppsättningen. Fälten i nyttolasten är desamma som skulle behövas för en PUT-begäran.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som du vill lägga till etiketter i. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller fältets XDM-attribut (Experience Data Model). Följande tre egenskaper krävs:<ul><li>id</code>: URI $id</code> -värdet för schemat som är associerat med fältet.</li><li>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör göras i form av en av de giltiga <a href="../../xdm/api/look-up-resource.md">Acceptera rubrikerna</a> för en XDM-sökningsbegäran.</li><li>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

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

## Ta bort etiketter för en datauppsättning

Du kan ta bort etiketter som används i en datauppsättning genom att göra en DELETE-begäran.

**API-format**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id` värdet för den datauppsättning vars etiketter du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar på HTTP-status 200 (OK), som anger att etiketterna har tagits bort. Du kan [slå upp befintliga etiketter](#lookup) för datauppsättningen i ett separat anrop för att bekräfta detta.

## Nästa steg

Nu när du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till Experience Platform. Om du vill veta mer kan du börja med att läsa [dokumentationen](../../ingestion/home.md)för dataöverföring.

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i översikten över [dataanvändningsprinciper](../policies/overview.md).