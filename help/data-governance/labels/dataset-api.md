---
keywords: Experience Platform;hem;populära ämnen;datauppsättning api;hantera dataanvändning;dataanvändning api
solution: Experience Platform
title: 'Hantera dataanvändningsetiketter för datauppsättningar med API:er '
topic: developer guide
description: Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# Hantera dataanvändningsetiketter för datauppsättningar med API:er

Med [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) kan du använda och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men skiljer sig från [!DNL Catalog Service]-API:t som hanterar datauppsättningsmetadata.

Det här dokumentet beskriver hur du hanterar etiketter för datauppsättningar och fält med [!DNL Dataset Service API]. Anvisningar om hur du hanterar etiketter för dataanvändning i sig med API-anrop finns i [etikettens slutpunktshandbok](../api/labels.md) för [!DNL Policy Service API].

## Komma igång

Innan du läser den här guiden följer du de steg som beskrivs i [avsnittet ](../../catalog/api/getting-started.md) Komma igång i guiden för katalogutvecklare för att samla in de nödvändiga inloggningsuppgifterna för att anropa [!DNL Platform] API:er.

För att kunna anropa slutpunkterna som beskrivs i det här dokumentet måste du ha det unika `id`-värdet för en specifik datauppsättning. Om du inte har det här värdet kan du läsa guiden på [lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Söka efter etiketter för en datauppsättning {#look-up}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-begäran till API:t [!DNL Dataset Service].

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

Du kan skapa en uppsättning etiketter för en datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran till API:t [!DNL Dataset Service]. Om du använder någon av dessa metoder skrivs befintliga etiketter över och ersätts med de som finns i nyttolasten.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id`-värdet för datauppsättningen som du skapar etiketter för. |

**Begäran**

Följande PUT-begäran uppdaterar de befintliga etiketterna för en datauppsättning samt ett specifikt fält i datauppsättningen. Fälten i nyttolasten är desamma som skulle behövas för en begäran om POST.

>[!IMPORTANT]
>
>Ett giltigt `If-Match`-huvud måste anges när du gör PUT-begäranden till `/datasets/{DATASET_ID}/labels`-slutpunkten. Se avsnittet [appendix](#if-match) för mer information om hur du använder det obligatoriska huvudet.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som du vill lägga till etiketter i. Varje objekt i den här arrayen måste ha följande egenskaper: <br/><br/>`option`: Ett objekt som innehåller fältets [!DNL Experience Data Model]-attribut (XDM). Följande tre egenskaper krävs:<ul><li>id</code>: URI $id</code>-värdet för schemat som är associerat med fältet.</li><li>contentType</code>: Innehållstypen och versionsnumret för schemat. Detta bör göras i form av en av de giltiga <a href="../../xdm/api/getting-started.md#accept">acceptera rubrikerna</a> för en XDM-sökningsbegäran.</li><li>schemaPath</code>: Sökvägen till fältet i datasetens schema.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

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

Du kan ta bort etiketterna som används i en datauppsättning genom att göra en DELETE-begäran till API:t [!DNL Dataset Service].

**API-format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Det unika `id`-värdet för datauppsättningen vars etiketter du vill ta bort. |

**Begäran**

Följande begäran tar bort etiketterna för datauppsättningen som anges i sökvägen.

>[!IMPORTANT]
>
>Ett giltigt `If-Match`-huvud måste anges när du gör DELETE-begäranden till `/datasets/{DATASET_ID}/labels`-slutpunkten. Se avsnittet [appendix](#if-match) för mer information om hur du använder det obligatoriska huvudet.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Svar**

Ett lyckat svar på HTTP-status 200 (OK), som anger att etiketterna har tagits bort. Du kan [leta upp de befintliga etiketterna](#look-up) för datauppsättningen i ett separat anrop för att bekräfta detta.

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig hur du hanterar dataanvändningsetiketter för datauppsättningar och fält med hjälp av API:t [!DNL Dataset Service].

När du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till [!DNL Experience Platform]. Om du vill veta mer börjar du med att läsa [dokumentationen om datafrågor](../../ingestion/home.md).

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i översikten över [dataanvändningsprinciper](../policies/overview.md).

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform] finns i översikten över [datauppsättningar](../../catalog/datasets/overview.md).

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om hur du arbetar med etiketter med hjälp av API:t för datauppsättningstjänsten.

### [!DNL If-Match] header  {#if-match}

När du gör API-anrop som uppdaterar de befintliga etiketterna för en datauppsättning (PUT och DELETE) måste ett `If-Match`-huvud som anger den aktuella versionen av datauppsättningsetiketten i datauppsättningstjänsten inkluderas. För att förhindra datakonflikter uppdaterar tjänsten bara datauppsättningsentiteten om den inkluderade `If-Match`-strängen matchar den senaste versionstaggen som genererats av systemet för den datauppsättningen.

>[!NOTE]
>
>Om det inte finns några etiketter för den aktuella datauppsättningen kan nya etiketter bara läggas till via en POST-förfrågan, som inte kräver en `If-Match`-rubrik. När etiketter har lagts till i en datauppsättning tilldelas ett `etag`-värde som kan användas för att uppdatera eller ta bort etiketterna vid ett senare tillfälle.

Om du vill hämta den senaste versionen av datauppsättningsetiketten skapar du en [GET-begäran](#look-up) till `/datasets/{DATASET_ID}/labels`-slutpunkten. Det aktuella värdet returneras i svaret under en `etag`-rubrik. När du uppdaterar befintliga datauppsättningsrubriker är det bäst att först utföra en sökbegäran för datauppsättningen för att hämta det senaste `etag`-värdet innan du använder det värdet i `If-Match`-huvudet i din efterföljande PUT- eller DELETE-begäran.