---
title: Exportera API-slutpunkt
description: Med slutpunkten /export i API:t för schemaregister kan du dela XDM-resurser mellan sandlådor.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Exportera slutpunkt

Alla resurser i [!DNL Schema Library] finns i en viss sandlåda i Adobe Experience Platform. I vissa fall kanske du vill dela XDM-resurser (Experience Data Model) mellan sandlådor och organisationer. The `/rpc/export` slutpunkt i [!DNL Schema Registry] Med API kan du generera en exportnyttolast för alla scheman, schemafältgrupper och datatyper i [!DNL Schema Library]och sedan använda den nyttolasten för att importera resursen (och alla beroende resurser) till en målsandlåda och organisation via [`/rpc/import` slutpunkt](./import.md).

## Komma igång

The `/rpc/export` slutpunkten är en del av [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

The `/rpc/export` slutpunkten är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i [!DNL Schema Registry] API, RPC-slutpunkter kräver inga ytterligare rubriker som `Accept` eller `Content-Type`, och använd inte `CONTAINER_ID`. Istället måste de använda `/rpc` namespace, vilket visas i API-anropen nedan.

## Generera en exportnyttolast för en resurs {#export}

För alla befintliga scheman, fältgrupper eller datatyper i [!DNL Schema Library]kan du generera en exportnyttolast genom att göra en GET-förfrågan till `/export` slutpunkt som anger ID för resursen i sökvägen.

**API-format**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_ID}` | The `meta:altId` eller URL-kodad `$id` för den XDM-resurs som du vill exportera. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en exportnyttolast för en `Restaurant` fältgrupp.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Svar**

Ett lyckat svar returnerar en array med objekt, som representerar mål-XDM-resursen och alla dess beroende resurser. I det här exemplet är det första objektet i arrayen ett objekt som skapats av en innehavare `Property` datatypen som `Restaurant` fältgruppen används, medan det andra objektet är `Restaurant` själva fältgruppen. Nyttolasten kan sedan användas för [importera resursen](#import) till en annan sandlåda eller organisation.

Observera att alla instanser av resursens klient-ID ersätts med `<XDM_TENANTID_PLACEHOLDER>`. Detta gör att schemaregistret automatiskt kan använda rätt klient-ID för resurserna beroende på var de skickas i det efterföljande importanropet.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Importera resursen {#import}

När du har genererat exportnyttolasten från CSV-filen kan du skicka den nyttolasten till `/rpc/import` slutpunkt för att generera schemat.

Se [importera slutpunktsguide](./import.md) om du vill ha mer information om hur du genererar scheman från exportnyttolaster.
