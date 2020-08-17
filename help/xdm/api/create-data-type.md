---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;datatype;Datatype
solution: Experience Platform
title: Skapa en datatyp
topic: developer guide
description: 'När det finns gemensamma datastrukturer som din organisation vill använda på flera sätt kanske du vill definiera en datatyp. Datatyper möjliggör konsekvent användning av flerfältsstrukturer, med större flexibilitet än blandningar, eftersom de kan inkluderas var som helst i ett schema genom att lägga till dem som"typ" för ett fält. '
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Skapa en datatyp

När det finns gemensamma datastrukturer som din organisation vill använda på flera sätt kanske du vill definiera en datatyp. Datatyper möjliggör konsekvent användning av flerfältsstrukturer, med större flexibilitet än blandningar, eftersom de kan inkluderas var som helst i ett schema genom att lägga till dem som `type` fältets.

Med andra ord kan du med hjälp av datatyper definiera en objekthierarki en gång och referera till den i ett fält på samma sätt som andra skalära typer.

**API-format**

```http
POST /tenant/datatypes
```

**Begäran**

För att definiera en datatyp krävs inte `meta:extends` eller `meta:intendedToExtend` fält, och inte heller måste fält kapslas för att undvika kollisioner.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om den nya datatypen, inklusive `$id`, `meta:altId`och `version`. Dessa tre värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Om en GET-begäran om att lista alla datatyper i klientbehållaren utförs, kommer datatypen för egenskapskonstruktion att ingå. Du kan också utföra en sökning (GET)-begäran med den URL-kodade `$id` URI:n för att visa den nya datatypen direkt. Se till att du tar med `version` texten i huvudet Godkänn för en uppslagsbegäran.
