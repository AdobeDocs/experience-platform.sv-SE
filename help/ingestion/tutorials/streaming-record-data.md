---
keywords: Experience Platform;hemmabruk;populära ämnen;direktuppspelning;intag;postdata;dataströmspostdata;
solution: Experience Platform
title: Direktuppspela postdata med API:er för direktuppspelning
topic-legacy: tutorial
type: Tutorial
description: Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning, som ingår i API:erna för Adobe Experience Platform datainmatningstjänst.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---


# Strömma postdata med Streaming Ingput API:er

Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning som ingår i Adobe Experience Platform [!DNL Data Ingestion Service] API:er.

## Komma igång

Den här självstudiekursen kräver kunskaper om olika Adobe Experience Platform-tjänster. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar upplevelsedata.
   - [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md): En omfattande guide som täcker alla tillgängliga slutpunkter i [!DNL Schema Registry] API och hur du anropar dem. Detta innefattar att känna till `{TENANT_ID}`, som visas i anrop genom den här självstudiekursen, samt hur du skapar scheman, som används för att skapa en datauppsättning för inhämtning.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../landing/api-guide.md).

## Skapa ett schema baserat på [!DNL XDM Individual Profile] class

Om du vill skapa en datauppsättning måste du först skapa ett nytt schema som implementerar [!DNL XDM Individual Profile] klassen. Mer information om hur du skapar scheman finns i [Utvecklarhandbok för API för schematabell](../../xdm/api/getting-started.md).

**API-format**

```http
POST /schemaregistry/tenant/schemas
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
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
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TENANT_ID}` | Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i IMS-organisationen. Mer information om klient-ID finns i [guide för schemaregister](../../xdm/api/getting-started.md#know-your-tenant-id). |

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
    "xdm:sourceProperty":"/workEmail/address",
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
>&#x200B; &#x200B;**Identitetsnamnområdeskoder**
>
> Kontrollera att koderna är giltiga - i exemplet ovan används&quot;email&quot; som är ett vanligt identitetsnamnutrymme. Andra vanliga standardnamnutrymmen för identiteter finns i [Vanliga frågor om identitetstjänsten](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Om du vill skapa ett anpassat namnutrymme följer du de steg som beskrivs i [Översikt över namnutrymmet identity](../../identity-service/home.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om schemats nya primära identitetsbeskrivning.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## Skapa en datauppsättning för postdata

När du har skapat schemat måste du skapa en datauppsättning för att kunna importera postdata.

>[!NOTE]
>
>Den här datauppsättningen kommer att aktiveras för **[!DNL Real-Time Customer Profile]** och **[!DNL Identity Service]**.

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
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
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
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Skapa en direktuppspelningsanslutning

När du har skapat ditt schema och din datauppsättning kan du skapa en direktuppspelningsanslutning

Mer information om hur du skapar en direktuppspelningsanslutning finns i [skapa en självstudiekurs för direktuppspelningsanslutning](./create-streaming-connection.md).

## Infoga postdata till direktuppspelningsanslutningen {#ingest-data}

När datauppsättningen och direktuppspelningsanslutningen är på plats kan du importera XDM-formaterade JSON-poster för att importera postdata till [!DNL Platform].

**API-format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | The `inletId` värdet för den direktuppspelningsanslutning som skapades tidigare. |
| `syncValidation` | En valfri frågeparameter som är avsedd för utvecklingsändamål. Om inställt på `true`kan den användas för att omedelbart avgöra om begäran har skickats. Som standard är det här värdet inställt på `false`. Observera att om du ställer in den här frågeparametern på `true` att antalet förfrågningar begränsas till 60 gånger per minut `CONNECTION_ID`. |

**Begäran**

Inmatning av postdata till en direktuppspelningsanslutning kan göras antingen med eller utan källnamnet.

Exempelbegäran nedan importerar en post med ett saknat källnamn till plattformen. Om en post saknar källnamnet läggs käll-ID:t till från anslutningsdefinitionen för direktuppspelning.

>[!NOTE]
>
>Följande API-anrop fungerar **not** kräver några autentiseringsrubriker.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
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
| `{CONNECTION_ID}` | ID:t för den tidigare skapade direktuppspelningsanslutningen. |
| `xactionId` | En unik identifierare som genererats på serversidan för den post du just skickade. Detta ID hjälper Adobe att spåra postens livscykel via olika system och med felsökning. |
| `receivedTimeMs` | En tidsstämpel (epok i millisekunder) som visar vilken tid begäran togs emot. |
| `syncValidation.status` | Sedan frågeparametern `syncValidation=true` läggs till, det här värdet visas. Om valideringen har slutförts kommer statusen att `pass`. |

## Hämta nyligen inmatade postdata

Om du vill validera tidigare importerade poster kan du använda [[!DNL Profile Access API]](../../profile/api/entities.md) för att hämta postdata.

>[!NOTE]
>
>Om ID för sammanfogningsprincip inte har definierats och `schema.name` eller `relatedSchema.name` är `_xdm.context.profile`, [!DNL Profile Access] hämtar **alla** relaterade identiteter.

**API-format**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `schema.name` | **Obligatoriskt.** Namnet på schemat som du försöker komma åt. |
| `entityId` | ID för entiteten. Om det anges måste du även ange entitetens namnutrymme. |
| `entityIdNS` | Namnområdet för det ID som du försöker hämta. |

**Begäran**

Du kan granska tidigare inmatade postdata med följande GET-förfrågan.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om de begärda entiteterna. Som du ser är detta samma post som importerades tidigare.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Nästa steg

Genom att läsa det här dokumentet kan du nu förstå hur du importerar postdata till [!DNL Platform] med direktuppspelningsanslutningar. Du kan försöka göra fler anrop med olika värden och hämta de uppdaterade värdena. Dessutom kan du börja övervaka dina inkapslade data via [!DNL Platform] Gränssnitt. Mer information finns i [övervaka datainmatning](../quality/monitor-data-ingestion.md) guide.

Mer information om direktuppspelning i allmänhet finns i [översikt över direktuppspelning](../streaming-ingestion/overview.md).
