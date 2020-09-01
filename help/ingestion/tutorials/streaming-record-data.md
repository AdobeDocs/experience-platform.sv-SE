---
keywords: Experience Platform;home;popular topics;streaming ingestion;ingestion;record data;stream record data;
solution: Experience Platform
title: Direktuppspelande postdata
topic: tutorial
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# Strömma postdata till Adobe Experience Platform

Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning, som ingår i Adobe Experience Platform API: [!DNL Data Ingestion Service] er.

## Komma igång

Den här självstudiekursen kräver kunskaper om olika Adobe Experience Platform-tjänster. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar upplevelsedata.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Utvecklarhandbok](../../xdm/api/getting-started.md)för schemaregister: En omfattande guide som täcker alla tillgängliga slutpunkter i [!DNL Schema Registry] API:t och hur du anropar dem. Det handlar om att känna till din `{TENANT_ID}`information, som visas i samtal under kursen, och att veta hur man skapar scheman, som används för att skapa en datauppsättning för förtäring.

Den här självstudien kräver dessutom att du redan har skapat en direktuppspelningsanslutning. Mer information om hur du skapar en direktuppspelningsanslutning finns i självstudiekursen [Skapa en direktuppspelningsanslutning](./create-streaming-connection.md).

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:er för direktuppspelning.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Skapa ett schema baserat på [!DNL XDM Individual Profile] klassen

Om du vill skapa en datauppsättning måste du först skapa ett nytt schema som implementerar [!DNL XDM Individual Profile] klassen. Mer information om hur du skapar scheman finns i utvecklarhandboken [för](../../xdm/api/getting-started.md)schemaregistrets API.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `meta:immutableTags` | I det här exemplet används `union` -taggen för att lagra dina data i [[!DNL Real-time Customer Profile]](../../profile/home.md). |

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
    "imsOrg": "{IMS_ORG}",
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
| `{TENANT_ID}` | Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i IMS-organisationen. Mer information om klientorganisations-ID finns i [schemaregisterguiden](../../xdm/api/getting-started.md#know-your-tenant-id). |

Observera attributen `$id` och `version` attributen, eftersom båda används när du skapar datauppsättningen.

## Ange en primär identitetsbeskrivning för schemat

Lägg sedan till en [identitetsbeskrivare](../../xdm/api/descriptors.md) i schemat som skapas ovan, med e-postadressattributet work som primär identifierare. Om du gör detta kommer två ändringar att göras:

1. E-postadressen till arbetet blir ett obligatoriskt fält. Det innebär att meddelanden som skickas utan det här fältet inte kan valideras och inte kan importeras.

2. [!DNL Real-time Customer Profile] kommer att använda e-postadressen till arbetet som en identifierare för att sammanfoga mer information om den personen.

### Begäran

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{SCHEMA_REF_ID}` | Den `$id` som du tidigare fick när du komponerade schemat. Det borde se ut ungefär så här: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**ID-namnområdeskoder**
>
> Kontrollera att koderna är giltiga - i exemplet ovan används&quot;email&quot; som är ett vanligt identitetsnamnutrymme. Andra vanliga standardnamnutrymmen för identiteter finns i Vanliga frågor om [identitetstjänsten](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Om du vill skapa ett anpassat namnutrymme följer du de steg som beskrivs i [översikten](../../identity-service/home.md)över identitetsnamnutrymmet.

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
    "imsOrg": "{IMS_ORG}"
}
```

## Skapa en datauppsättning för postdata

När du har skapat schemat måste du skapa en datauppsättning för att kunna importera postdata.

>[!NOTE]
>
>Den här datauppsättningen kommer att aktiveras för **[!DNL Real-time Customer Profile]** och **[!DNL Identity Service]**.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 och en matris som innehåller ID:t för den nya datauppsättningen i formatet `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Infoga postdata till direktuppspelningsanslutningen

När datauppsättningen och direktuppspelningsanslutningen är på plats kan du importera XDM-formaterade JSON-poster att importera postdata till [!DNL Platform].

**API-format**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Värdet `id` för den direktuppspelningsanslutning som skapades tidigare. |
| `synchronousValidation` | En valfri frågeparameter som är avsedd för utvecklingsändamål. Om det anges till `true`kan det användas för att omedelbart avgöra om begäran har skickats. Som standard är det här värdet inställt på `false`. |

**Begäran**

>[!NOTE]
>
>Följande API-anrop kräver **inga** autentiseringshuvuden.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen strömmade filen [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID:t för den tidigare skapade direktuppspelningsanslutningen. |
| `xactionId` | En unik identifierare som genererats på serversidan för den post du just skickade. Detta ID hjälper Adobe att spåra postens livscykel via olika system och med felsökning. |
| `receivedTimeMs` | En tidsstämpel (epok i millisekunder) som visar vilken tid begäran togs emot. |
| `synchronousValidation.status` | Eftersom frågeparametern `synchronousValidation=true` lades till visas det här värdet. Om valideringen har slutförts blir statusen `pass`. |

## Hämta nyligen inmatade postdata

Om du vill validera de poster som har importerats tidigare kan du använda API:t för [[!DNL-profilåtkomst]](../../profile/api/entities.md) för att hämta postdata.

>[!NOTE]
>
>Om ID:t för sammanfogningsprincipen inte har definierats och `schema.name` eller `relatedSchema.name` är `_xdm.context.profile`, [!DNL Profile Access] hämtas **alla** relaterade identiteter.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Genom att läsa det här dokumentet kan du nu förstå hur du importerar postdata till [!DNL Platform] med direktuppspelningsanslutningar. Du kan försöka göra fler anrop med olika värden och hämta de uppdaterade värdena. Dessutom kan du börja övervaka dina inkapslade data via [!DNL Platform] användargränssnittet. Mer information finns i guiden [för dataöverföring](../quality/monitor-data-flows.md) .

Mer information om direktuppspelningsuppläsning i allmänhet finns i översikten över [direktuppspelningsuppläsning](../streaming-ingestion/overview.md).


