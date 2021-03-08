---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;Experience data model;data model;data model;data model;sampledata;sample data;rpc;
solution: Experience Platform
title: Exempel på API-slutpunkt för data
description: Med slutpunkten /sampledata i API:t för schemaregister kan du generera exempeldata mappade till strukturen för ett befintligt XDM-schema.
topic: utvecklarhandbok
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Exempeldataslut

För att kunna importera data till Adobe Experience Platform måste dataformatet och datastrukturen överensstämma med ett befintligt XDM-schema (Experience Data Model). Beroende på hur komplicerat schemat är för en viss datauppsättning kan det vara svårt att fastställa den exakta formen för de data som datauppsättningen förväntar sig vid intag.

Med hjälp av `/sampledata`-slutpunkten i [!DNL Schema Registry]-API:t kan du generera ett exempelobjekt för eventuella tidigare skapade schema.

## Komma igång

Slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anropen i det här dokumentet och viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

Exempeldatans slutpunkt är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i API:t [!DNL Schema Registry], kräver RPC-slutpunkter inga ytterligare rubriker som `Accept` eller `Content-Type`, och använder inte en `CONTAINER_ID`. I stället måste de använda namnutrymmet `/rpc`, vilket visas i API-anropet nedan.

## Hämta exempeldata för ett schema

Du kan hämta exempeldata för alla scheman i schemabiblioteket genom att ange schemats ID i sökvägen till en GET-begäran till slutpunkten.

**API-format**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` eller URL-kodad `$id` för schemat som du vill generera exempeldata för. |

**Begäran**

Följande begäran genererar exempeldata för ett medlemsschema för lojalitet.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar ett exempeldataobjekt för det angivna schemat.

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
