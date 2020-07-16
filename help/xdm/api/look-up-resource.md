---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Söka efter en resurs
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 1%

---


# Söka efter en resurs

Du kan söka efter specifika resurser genom att göra en GET-begäran som innehåller resursens `$id` (URL-kodad URI) i sökvägen till begäran.

**API-format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren där resurserna finns (&quot;global&quot; eller&quot;tenant&quot;). |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska hämtas från [!DNL Schema Library]. Giltiga typer är `datatypes`, `mixins`, `schemas`och `classes`. |
| `{RESOURCE_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` resursen. |

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Begäranden om resurssökning måste `version` inkluderas i huvudet Godkänn. Följande Acceptera rubriker är tillgängliga för sökningar:

| Acceptera | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw med `$ref` och `allOf`har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` och `allOf` är åtgärdade, har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw med `$ref` och `allOf`, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` och `allOf` löste sig - inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` och `allOf` åtgärdade, beskrivningar inkluderades. |

>[!NOTE]
>
>Om du bara anger `major` version (1, 2, 3 osv.) returnerar registret automatiskt den senaste `minor` versionen (.1, .2, .3 osv.).

**Svar**

Ett lyckat svar returnerar information om resursen. Vilka fält som returneras beror på vilket Acceptera-huvud som skickas i begäran. Experimentera med olika Acceptera-huvuden för att jämföra svaren och ta reda på vilken rubrik som är bäst för dig.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
