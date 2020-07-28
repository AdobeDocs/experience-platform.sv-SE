---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ersätta en resurs
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Ersätta en resurs

Med [!DNL Schema Registry] den kan du ersätta en hel resurs med en PUT-åtgärd. Den här åtgärden skriver i princip om resursen, och därför måste begärandetexten innehålla alla fält som krävs när en ny resurs skapas med en begäran om POST.

Den här metoden är särskilt användbar om du vill uppdatera mycket information i resursen samtidigt.

>[!NOTE]
>
>Om du bara vill uppdatera en del av en resurs i stället för att ersätta den helt, ska du läsa dokumentet om hur du [uppdaterar en resurs med en PATCH-åtgärd](update-resource.md).

**API-format**

En PUT-begäran kan bara utföras mot resurser som du definierar i innehavarbehållaren.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska uppdateras från [!DNL Schema Library]. Giltiga typer är `datatypes`, `mixins`, `schemas`och `classes`. |
| `{RESOURCE_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` resursen. |

**Begäran**

Denna exempelbegäran ersätter datatypen Property Construction som skapades i ett tidigare exempel. Begärandetexten ser ut ungefär som den POST som användes för att skapa datatypen, förutom att den nu innehåller en uppdaterad uppsättning fält med nya värden som ersätter det som tidigare definierats.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Svar**

Ett lyckat svar returnerar informationen om datatypen och visar de uppdaterade fälten och värdena som anges i begäran.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
