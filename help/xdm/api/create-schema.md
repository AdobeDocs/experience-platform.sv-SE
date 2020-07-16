---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa ett schema
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Skapa ett schema

Ett schema kan ses som en plan för de data som du vill importera till [!DNL Experience Platform]. Varje schema består av en klass och noll eller flera mixiner. Du behöver alltså inte lägga till en blandning för att definiera ett schema, men i de flesta fall används minst en blandning.

Schemadispositionsprocessen börjar med att tilldela en klass. Klassen definierar viktiga beteendeaspekter för data (post- eller tidsserier) samt de minimifält som krävs för att beskriva de data som ska importeras.

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Begäran måste innehålla ett `allOf` attribut som refererar till `$id` en klass. Det här attributet definierar den &quot;basklass&quot; som schemat ska implementera. I det här exemplet är basklassen en&quot;Egenskapsinformation&quot;-klass som skapades tidigare.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `allOf > $ref` | Värdet `$id` för den klass som det nya schemat ska implementera. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om det nyligen skapade schemat, inklusive `$id`, `meta:altId`och `version`. Dessa värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Om du utför en GET-begäran om att lista alla scheman i innehavarbehållaren skulle det nu inkludera egenskapsinformationsschemat, eller så kan du utföra en GET-begäran med den URL-kodade `$id` URI:n för att visa det nya schemat direkt. Kom ihåg att inkludera `version` i huvudet Godkänn för alla uppslagsbegäranden.
