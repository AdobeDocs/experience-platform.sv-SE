---
title: Exportera API-slutpunkt
description: Med slutpunkten /export i API:t för schemaregister kan du dela XDM-resurser mellan sandlådor.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Exportera slutpunkt

Alla resurser i [!DNL Schema Library] finns i en specifik sandlåda i Adobe Experience Platform. I vissa fall kanske du vill dela XDM-resurser (Experience Data Model) mellan sandlådor och organisationer. Med slutpunkten `/rpc/export` i API:t [!DNL Schema Registry] kan du generera en exportnyttolast för alla scheman, schemafältgrupper och datatyper i [!DNL Schema Library] och sedan använda den nyttolasten för att importera resursen (och alla beroende resurser) till en mållandlåda och organisation via [`/rpc/import` endpoint ](./import.md).

## Komma igång

Slutpunkten `/rpc/export` är en del av [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

Slutpunkten `/rpc/export` är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i API:t [!DNL Schema Registry] kräver RPC-slutpunkter inga ytterligare rubriker som `Accept` eller `Content-Type`, och använder inte `CONTAINER_ID`. I stället måste de använda namnutrymmet `/rpc`, vilket visas i API-anropen nedan.

## Generera en exportnyttolast för en resurs {#export}

För alla befintliga scheman, fältgrupper eller datatyper i [!DNL Schema Library] kan du generera en exportnyttolast genom att göra en GET-begäran till `/export`-slutpunkten, som anger ID:t för resursen i sökvägen.

**API-format**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` eller URL-kodad `$id` för XDM-resursen som du vill exportera. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en exportnyttolast för en `Restaurant`-fältgrupp.

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

Ett lyckat svar returnerar en array med objekt, som representerar mål-XDM-resursen och alla dess beroende resurser. I det här exemplet är det första objektet i arrayen en datatyp som skapats av en innehavare, `Property`, som används av fältgruppen `Restaurant`, medan det andra objektet är själva fältgruppen `Restaurant`. Den här nyttolasten kan sedan användas för att [importera resursen](#import) till en annan sandlåda eller organisation.

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

När du har genererat exportnyttolasten från CSV-filen kan du skicka den nyttolasten till `/rpc/import`-slutpunkten för att generera schemat.

Mer information om hur du genererar scheman från exportnyttolaster finns i [importguiden](./import.md).
