---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;behavior;behavior;behaviors;behaviors;behaviors;behaviors;
solution: Experience Platform
title: API-slutpunkt för beteenden
description: Med slutpunkten /behaviors i API:t för schemaregister kan du hämta alla tillgängliga beteenden i den globala behållaren.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Beteendeslutpunkt

I Experience Data Model (XDM) definierar beteenden vilken typ av data som ett schema beskriver. Varje XDM-klass måste referera till ett specifikt beteende, som alla scheman som använder den klassen ärver. För nästan alla användningsområden i Platform finns det två tillgängliga beteenden:

* **[!UICONTROL Record]**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **[!UICONTROL Time-series]**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

>[!NOTE]
>
>Det finns vissa användningsfall i Platform som kräver användning av schema som inte har något av ovanstående beteenden. I dessa fall finns ett tredje &quot;ad hoc&quot;-beteende att tillgå. Se självstudiekursen om [skapa ett ad hoc-schema](../tutorials/ad-hoc.md) för mer information.
>
>Mer allmän information om databeteenden i termer av hur de påverkar schemakomposition finns i handboken på [grunderna för schemakomposition](../schema/composition.md).

The `/behaviors` slutpunkt i [!DNL Schema Registry] Med API kan du visa tillgängliga beteenden i `global` behållare.

## Komma igång

Slutpunkten som används i den här guiden är en del av [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med beteenden {#list}

Du kan hämta en lista över alla tillgängliga beteenden genom att göra en GET-förfrågan till `/behaviors` slutpunkt.

**API-format**

```http
GET /global/behaviors
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Svar**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Söka efter ett beteende {#lookup}

Du kan söka efter ett visst beteende genom att ange dess ID i sökvägen till en GET-begäran till `/behaviors` slutpunkt.

**API-format**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BEHAVIOR_ID}` | The `meta:altId` eller URL-kodad `$id` av beteendet du vill hitta. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar information om postbeteendet genom att ange dess `meta:altId` i sökvägen till begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Svar**

Ett godkänt svar returnerar detaljerna om beteendet, inklusive version, beskrivning och de attribut som beteendet ger till de klasser som använder det.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Nästa steg

Den här guiden beskriver användningen av `/behaviors` slutpunkt i [!DNL Schema Registry] API. Om du vill lära dig hur du tilldelar ett beteende till en klass med API:t kan du läsa [klassers slutpunktshandbok](./classes.md).
