---
keywords: Experience Platform;hemmabruk;populära ämnen;direktuppspelning;intag;tidsseriedata;data från strömtidsserier;
solution: Experience Platform
title: Strömma data i tidsserier med API:er för strömmande inmatning
type: Tutorial
description: Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning, som ingår i API:erna för Adobe Experience Platform datainmatningstjänst.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 0%

---

# Strömma tidsseriedata med Streaming Ingmit APIs

Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning som ingår i Adobe Experience Platform [!DNL Data Ingestion Service] API:er.

## Komma igång

Den här självstudiekursen kräver kunskaper om olika Adobe Experience Platform-tjänster. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar upplevelsedata.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md): En omfattande guide som täcker alla tillgängliga slutpunkter i [!DNL Schema Registry] API och hur du anropar dem. Detta innefattar att känna till `{TENANT_ID}`, som visas i anrop genom den här självstudiekursen, samt hur du skapar scheman, som används för att skapa en datauppsättning för inhämtning.

Den här självstudien kräver dessutom att du redan har skapat en direktuppspelningsanslutning. Mer information om hur du skapar en direktuppspelningsanslutning finns i [skapa en självstudiekurs för direktuppspelningsanslutning](./create-streaming-connection.md).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../landing/api-guide.md).

## Skapa ett schema baserat på klassen XDM ExperienceEvent

Om du vill skapa en datauppsättning måste du först skapa ett nytt schema som implementerar [!DNL XDM ExperienceEvent] klassen. Mer information om hur du skapar scheman finns i [Utvecklarhandbok för API för schematabell](../../xdm/api/getting-started.md).

**API-format**

```http
POST /schemaregistry/tenant/schemas
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `title` | Namnet som du vill använda för ditt schema. Namnet måste vara unikt. |
| `description` | En meningsfull beskrivning av schemat som du skapar. |
| `meta:immutableTags` | I det här exemplet `union` -taggen används för att lagra data i [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om ditt nyligen skapade schema.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TENANT_ID}` | Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i din organisation. Mer information om klient-ID finns i [guide för schemaregister](../../xdm/api/getting-started.md#know-your-tenant-id). |

Observera `$id` och `version` -attribut, eftersom båda dessa kommer att användas när du skapar datauppsättningen.

## Ange en primär identitetsbeskrivning för schemat

Lägg sedan till en [identitetsbeskrivare](../../xdm/api/descriptors.md) till schemat som skapas ovan, med arbetsprogrammets e-postadressattribut som primär identifierare. Om du gör detta kommer två ändringar att göras:

1. E-postadressen till arbetet blir ett obligatoriskt fält. Det innebär att meddelanden som skickas utan det här fältet inte kan valideras och inte kan importeras.

2. [!DNL Real-Time Customer Profile] kommer att använda e-postadressen till arbetet som en identifierare för att sammanfoga mer information om den personen.

### Begäran

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | The `$id` som du tidigare fått när du komponerade schemat. Det borde se ut ungefär så här: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Identitetsnamnområdeskoder**
>
> Kontrollera att koderna är giltiga - i exemplet ovan används&quot;email&quot; som är ett vanligt identitetsnamnutrymme. Andra vanliga standardnamnutrymmen för identiteter finns i [Vanliga frågor om identitetstjänsten](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Om du vill skapa ett anpassat namnutrymme följer du de steg som beskrivs i [Översikt över namnutrymmet identity](../../identity-service/home.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om schemats nya primära identitetsnamnrymd.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## Skapa en datauppsättning för tidsseriedata

När du har skapat schemat måste du skapa en datauppsättning för att kunna importera postdata.

>[!NOTE]
>
>Den här datauppsättningen kommer att aktiveras för **[!DNL Real-Time Customer Profile]** och **[!DNL Identity]** genom att ange lämpliga taggar.

**API-format**

```http
POST /catalog/dataSets
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 och en matris som innehåller ID:t för den nyskapade datauppsättningen i formatet `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## Skapa en direktuppspelningsanslutning

När du har skapat ditt schema och din datauppsättning måste du skapa en direktuppspelningsanslutning för att kunna importera dina data.

Mer information om hur du skapar en direktuppspelningsanslutning finns i [skapa en självstudiekurs för direktuppspelningsanslutning](./create-streaming-connection.md).

## Infoga tidsseriedata i direktuppspelningsanslutningen

När datauppsättningen, direktuppspelningsanslutningen och dataflödet har skapats kan du importera XDM-formaterade JSON-poster för att importera tidsseriedata i [!DNL Platform].

**API-format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | The `id` värdet för den nyligen skapade direktuppspelningsanslutningen. |
| `syncValidation` | En valfri frågeparameter som är avsedd för utvecklingsändamål. Om inställt på `true`kan den användas för att omedelbart avgöra om begäran har skickats. Som standard är det här värdet inställt på `false`. Observera att om du ställer in den här frågeparametern på `true` att antalet förfrågningar begränsas till 60 gånger per minut `CONNECTION_ID`. |

**Begäran**

Inmatning av tidsseriedata till en direktuppspelningsanslutning kan göras antingen med eller utan källnamnet.

Exemplet nedan anger att tidsseriedata med ett saknat källnamn ska importeras till plattformen. Om källnamnet saknas i data läggs käll-ID:t till från anslutningsdefinitionen för direktuppspelning.

Båda `xdmEntity._id` och `xdmEntity.timestamp` är obligatoriska fält för tidsseriedata. The `xdmEntity._id` attribut representerar en unik identifierare för själva posten, **not** ett unikt ID för den person eller enhet vars register det är.

Du måste skapa en egen `xdmEntity._id` och `xdmEntity.timestamp` för posten på ett sätt som är konsekvent om posten någonsin behöver hämtas på nytt. I idealfallet innehåller källsystemet dessa värden. Om ett ID inte är tillgängligt bör du överväga att sammanfoga värden för andra fält i posten för att skapa ett unikt värde som konsekvent kan återskapas från posten vid återinläsning.

>[!NOTE]
>
>Följande API-anrop fungerar **not** kräver några autentiseringsrubriker.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
            }
        }
    }
}'
```

Om du vill ta med ett källnamn visar följande exempel hur du skulle ta med det.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen strömmade [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{CONNECTION_ID}` | The `inletId` av den tidigare skapade direktuppspelningsanslutningen. |
| `xactionId` | En unik identifierare som genererats på serversidan för den post du just skickade. Detta ID hjälper Adobe att spåra postens livscykel via olika system och med felsökning. |
| `receivedTimeMs`: En tidsstämpel (epok i millisekunder) som visar vilken tid begäran togs emot. |
| `syncValidation.status` | Sedan frågeparametern `syncValidation=true` läggs till, det här värdet visas. Om valideringen har slutförts kommer statusen att `pass`. |

## Hämta data för den nyligen inmatade tidsserien

Om du vill validera tidigare importerade poster kan du använda [[!DNL Profile Access API]](../../profile/api/entities.md) för att hämta tidsseriedata. Detta kan göras med en GET-begäran till `/access/entities` slutpunkt och valfria frågeparametrar. Flera parametrar kan användas, avgränsade med et-tecken (&amp;).&quot;

>[!NOTE]
>
>Om ID för sammanfogningsprincip inte har definierats och `schema.name` eller `relatedSchema.name` är `_xdm.context.profile`, [!DNL Profile Access] hämtar **alla** relaterade identiteter.

**API-format**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `schema.name` | **Obligatoriskt.** Namnet på schemat som du försöker komma åt. |
| `relatedSchema.name` | **Obligatoriskt.** Eftersom du använder en `_xdm.context.experienceevent`anger det här värdet schemat för den profilentitet som tidsseriehändelser är relaterade till. |
| `relatedEntityId` | ID för den relaterade entiteten. Om det anges måste du även ange entitetens namnutrymme. |
| `relatedEntityIdNS` | Namnområdet för det ID som du försöker hämta. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om de begärda entiteterna. Som du ser är detta samma tidsseriedata som tidigare har importerats.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Nästa steg

Genom att läsa det här dokumentet kan du nu förstå hur du importerar postdata till [!DNL Platform] med direktuppspelningsanslutningar. Du kan försöka göra fler anrop med olika värden och hämta de uppdaterade värdena. Dessutom kan du börja övervaka dina inkapslade data via [!DNL Platform] Gränssnitt. Mer information finns i [övervaka datainmatning](../quality/monitor-data-ingestion.md) guide.

Mer information om direktuppspelning i allmänhet finns i [översikt över direktuppspelning](../streaming-ingestion/overview.md).
