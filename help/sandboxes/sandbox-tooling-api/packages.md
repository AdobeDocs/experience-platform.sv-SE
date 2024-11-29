---
title: API-slutpunkt för sandlådeverktygspaket
description: Med slutpunkten /packages i sandlådeverktygets API kan du programmässigt hantera paket i Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 47e4616e5465ec97512647b9280f461c6971aa42
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 1%

---

# Slutpunkt för paket

Med sandlådeverktygen kan du markera olika artefakter (kallas även objekt) och exportera dem till ett paket. Ett paket kan bestå av en enda artefakt eller flera artefakter (till exempel datauppsättningar eller scheman). Artefakter som ingår i ett paket måste komma från samma sandlåda.

Med slutpunkten `/packages` i sandlådeverktygets API kan du programmässigt hantera paket i organisationen, inklusive publicera ett paket och importera ett paket till en sandlåda.

## Skapa ett paket {#create}

Du kan skapa ett paket med flera artefakter genom att göra en POST-förfrågan till slutpunkten `/packages` och samtidigt ange värden för paketets namn och pakettyp.

**API-format**

```http
POST /packages/
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `name` | Paketets namn. | Sträng | Ja |
| `description` | En beskrivning som ger mer information om ditt paket. | Sträng | Nej |
| `packageType` | Pakettypen är **PARTIAL** för att ange att du inkluderar specifika artefakter i ett paket. | Sträng | JA |
| `sourceSandbox` | Paketets källsandlåda. | Objekt | Nej |
| `expiry` | Tidsstämpeln som definierar paketets förfallodatum. Standardvärdet är 90 dagar från skapandedatumet. Svarets förfallofält är epoch UTC-tid. | Sträng (UTC-tidsstämpelformat) | Nej |
| `artifacts` | En lista med artefakter som ska exporteras till paketet. Värdet `artifacts` ska vara **null** eller **empty** när `packageType` är `FULL`. | Array | Nej |

**Svar**

Ett lyckat svar returnerar det nya paketet. Svaret innehåller motsvarande paket-ID samt information om status, utgångsdatum och lista över artefakter.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Uppdatera ett paket {#update}

Du kan uppdatera ett paket genom att göra en PUT-begäran till slutpunkten `/packages`.

### Lägga till artefakter i ett paket {#add-artifacts}

Om du vill lägga till artefakter i ett paket måste du ange `id` och inkludera **ADD** för `action`.

**API-format**

```http
PUT /packages/
```

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `id` | ID:t för paketet som ska uppdateras. | Sträng | Ja |
| `action` | Om du vill lägga till artefakter i paketet måste åtgärdsvärdet vara **ADD**. Den här åtgärden stöds bara för pakettyperna **PARTIAL**. | Sträng | Ja |
| `artifacts` | En lista med artefakter som ska läggas till i paketet. Paketet ändras inte om listan är **null** eller **tom**. Artefakter tas bort innan de läggs till i paketet. Se tabellen nedan för en fullständig lista över de artefakter som stöds. | Array | Nej |
| `expiry` | Tidsstämpeln som definierar paketets förfallodatum. Standardvärdet är 90 dagar från den tidpunkt då PUT API anropas om inget förfallodatum anges i nyttolasten. Svarets förfallofält är epoch UTC-tid. | Sträng (UTC-tidsstämpelformat) | Nej |

Följande artefakttyper stöds för närvarande.

| Artefakt | Plattform | Objekt | Delflöde | Fullständig sandlåda |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Resor | Ja | Nej |
| `ID_NAMESPACE` | Kunddataplattform | Identiteter | Ja | Ja |
| `REGISTRY_DATATYPE` | Kunddataplattform | Datatyp | Ja | Ja |
| `REGISTRY_CLASS` | Kunddataplattform | Klass | Ja | Ja |
| `REGISTRY_MIXIN` | Kunddataplattform | Fältgrupp | Ja | Ja |
| `REGISTRY_SCHEMA` | Kunddataplattform | Scheman | Ja | Ja |
| `CATALOG_DATASET` | Kunddataplattform | Datauppsättningar | Ja | Ja |
| `DULE_CONSENT_POLICY` | Kunddataplattform | Samtycke- och styrningsprinciper | Ja | Ja |
| `PROFILE_SEGMENT` | Kunddataplattform | Målgrupper | Ja | Ja |
| `FLOW` | Kunddataplattform | Källdataflöde | Ja | Ja |

**Svar**

Ett lyckat svar returnerar det uppdaterade paketet. Svaret innehåller motsvarande paket-ID samt information om status, utgångsdatum och lista över artefakter.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Ta bort felaktigheter från ett paket {#delete-artifacts}

Om du vill ta bort artefakter från ett paket måste du ange `id` och inkludera **DELETE** för `action`.

**API-format**

```http
PUT /packages/
```

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `id` | ID:t för paketet som ska uppdateras. | Sträng | Ja |
| `action` | Om du vill ta bort artefakter från ett paket bör åtgärdsvärdet vara **DELETE**. Den här åtgärden stöds bara för pakettyperna **PARTIAL**. | Sträng | Ja |
| `artifacts` | En lista med artefakter som ska tas bort från paketet. Paketet ändras inte om listan är **null** eller **tom**. | Array | Nej |

**Svar**

Ett lyckat svar returnerar det uppdaterade paketet. Svaret innehåller motsvarande paket-ID samt information om status, utgångsdatum och lista över artefakter.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Uppdatera metadatafält i ett paket {#update-metadata}

>[!NOTE]
>
>Åtgärden **UPDATE** används för att uppdatera paketets metadatafält och **kan inte** användas för att lägga till/ta bort artefakter i ett paket.

Om du vill uppdatera metadatafälten i ett paket måste du ange `id` och inkludera **UPDATE** för `action`.

**API-format**

```http
PUT /packages/
```

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `id` | ID:t för paketet som ska uppdateras. | Sträng | Ja |
| `action` | Om du vill uppdatera metadatafälten i ett paket ska åtgärdsvärdet vara **UPDATE**. Den här åtgärden stöds bara för pakettyperna **PARTIAL**. | Sträng | Ja |
| `name` | Paketets uppdaterade namn. Dubblettpaketnamn tillåts inte. | Array | Ja |
| `sourceSandbox` | Source sandlåda ska tillhöra samma organisation som anges i begärans huvud. | Objekt | Ja |

**Svar**

Ett lyckat svar returnerar det uppdaterade paketet. Svaret innehåller motsvarande paket-ID samt information om dess beskrivning, status, förfallodatum och lista över artefakter.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Ta bort ett paket {#delete}

Om du vill ta bort ett paket skickar du en DELETE-begäran till slutpunkten `/packages` och anger ID:t för det paket som du vill ta bort.

**API-format**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill ta bort. |

**Begäran**

Följande begäran tar bort paketet med ID:t {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar en orsak som visar det paket-ID som tagits bort.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish ett paket {#publish}

Om du vill kunna importera ett paket till en sandlåda måste du publicera det. Gör en GET-förfrågan till `/packages`-slutpunkten och ange ID:t för det paket som du vill publicera.

**API-format**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill publicera. |

**Begäran**

Följande begäran publicerar paketet med ID:t {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `expiryPeriod` | Den här användarspecificerade tidsperioden definierar paketets förfallodatum (i dagar) från den tidpunkt då paketet publicerades. Värdet får inte vara negativt.<br> Om inget värde anges beräknas standardvärdet till 90 (dagar) från publiceringsdatumet. | Heltal | Nej |

**Svar**

Ett lyckat svar returnerar det publicerade paketet.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Söka efter ett paket {#look-up-package}

Du kan söka efter ett enskilt paket genom att göra en GET-begäran till slutpunkten `/packages` som innehåller motsvarande ID för paketet i sökvägen för begäran.

**API-format**

```http
GET /packages/{PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill söka efter. |

**Begäran**

Följande begäran hämtar information för {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett slutfört svar returnerar information för det efterfrågade paket-ID:t. Svaret innehåller namn, beskrivning, publiceringsdatum och förfallodatum, paketets källsandlåda samt en lista med artefakter.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Listpaket {#list-packages}

Du kan visa alla paket i din organisation genom att göra en GET-förfrågan till slutpunkten `/packages`.

**API-format**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Mer information finns i avsnittet om [frågeparametrar](./appendix.md). |

**Begäran**

Följande begäran hämtar information om paketen baserat på {QUERY_PARAMS}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett godkänt svar returnerar en lista med paket som tillhör din organisation, inklusive information om namn, status, förfallodatum och artefakt.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Importera ett paket {#import}

Den här slutpunkten används för att hämta objekt i konflikt i den angivna mållandlådan. Objekt i konflikt representerar liknande objekt som redan finns i målsandlådan.

**API-format**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill söka efter. |

**Begäran**

Följande begäran importerar {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Konflikter returneras i svaret. Svaret visar det ursprungliga paketet plus `alternatives`-fragmentet som en array som sorterats efter rangordning.

+++Visa svar

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Skicka en import {#submit-import}

>[!NOTE]
>
>Med konfliktlösning är det naturligt att den alternativa artefakten redan finns i målsandlådan.

Du kan skicka en import för ett paket när du har granskat konflikter och tillhandahållit ersättningar genom att göra en POST-förfrågan till slutpunkten `/packages`. Resultatet anges som en nyttolast, som startar importjobbet för målsandlådan enligt vad som anges i nyttolasten.

Nyttolasten accepterar även användarspecificerat jobbnamn och beskrivning för importjobb. Om användarspecificerat namn och beskrivning inte är tillgängliga används paketnamn och beskrivning för jobbnamn och beskrivning.

**API-format**

```http
POST /packages/import
```

**Begäran**

Följande begäran hämtar paket som ska importeras. Nyttolasten är en karta över ersättningar där, om det finns en post, nyckeln är den `artifactId` som anges av paketet, och alternativet är värdet. Om kartan eller nyttolasten är **tom** utförs inga ersättningar.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` representerar mappningen av källsandlådeartefakter till befintliga målarsandlådeartefakter. Eftersom de redan finns där undviker importjobbet att skapa dessa artefakter i målsandlådan. | Sträng | Nej |

**Svar**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Lista alla beroende objekt {#dependent-objects}

Visa alla beroende objekt för de exporterade objekten i ett paket genom att göra en POST-förfrågan till slutpunkten `/packages` samtidigt som du anger paketets ID.

**API-format**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | Paketets ID. |

**Begäran**

I följande begäran visas alla beroende objekt för {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Svar**

Ett godkänt svar returnerar en lista med underordnade objekt för objekten.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Kontrollera rollbaserade behörigheter för att importera alla paketartefakter {#role-based-permissions}

Du kan kontrollera om du har behörighet att importera paketartefakter genom att göra en GET-begäran till slutpunkten `/packages` och samtidigt ange ID:t för paketet och målsandlådans namn.

**API-format**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill importera. |

**Begäran**

Följande begäran kontrollerar dina behörigheter för {PACKAGE_ID} och sandlådan.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar resursbehörigheter för målsandlådan, inklusive en lista över nödvändiga behörigheter, saknade behörigheter, typ av artefakt och ett beslut om huruvida skapandet är tillåtet.

+++Visa svar

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Visa export-/importjobb {#list-jobs}

Du kan visa aktuella export-/importjobb genom att göra en GET-förfrågan till slutpunkten `/packages`.

**API-format**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Mer information finns i avsnittet om [frågeparametrar](./appendix.md). |

**Begäran**

I följande begäran visas alla slutförda importjobb.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar alla slutförda importjobb.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```

## Dela paket mellan olika organisationer {#org-linking}

Med slutpunkten `/handshake` i sandlådeverktygs-API kan du samarbeta med andra organisationer för att dela paket.

### Skicka en delningsbegäran {#send-request}

Skicka en begäran till en målpartnerorganisation för att dela godkännande genom att göra en POST-förfrågan till slutpunkten `/handshake/bulkCreate`. Detta krävs innan du kan dela privata paket.

**API-format**

```http
POST /handshake/bulkCreate
```

**Begäran**

Följande begäran initierar delningsgodkännande mellan en målpartnerorganisation och källorganisationen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | En lista över målorganisationer att skicka delningsbegäran till. | Array | Ja |
| `sourceIMSDetails` | Information om källorganisationen. | Objekt | Ja |

**Svar**

Ett godkänt svar returnerar information om din delningsförfrågan.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKIND_ID}"
        }
    },
    "failedRequests": {}
}
```

### Godkänna mottagna delningsbegäranden {#approve-requests}

Godkänn delningsbegäranden från målpartnerorganisationer genom att göra en POST-förfrågan till slutpunkten `/handshake/action`. Efter godkännande kan källpartnerorganisationer dela privata paket.

**API-format**

```http
POST /handshake/action
```

**Begäranden**

Följande begäran godkänner en delningsbegäran från en målpartnerorganisation.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `linkingID` | ID:t för delningsbegäran som du svarar på. | Sträng | Ja |
| `status` | Åtgärden som utförs på delningsbegäran. Godtagbara värden är `APPROVED` eller `REJECTED`. | Sträng | Ja |
| `reason` | Orsaken till att åtgärden vidtas. | Sträng | Ja |
| `targetIMSOrgDetails` | Information om målorganisationen där ID-värdet ska vara målorganisationens **ID**, namnvärdet ska vara målorganisationens **NAME** och regionsvärdet ska vara målorganisationens **REGION**. | Objekt | Ja |

**Svar**

Ett godkänt svar returnerar information om den godkända delningsbegäran.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Visa utgående/inkommande delningsbegäranden {#outgoing-and-incoming-requests}

Visa utgående och inkommande delningsbegäranden genom att göra en GET-förfrågan till slutpunkten `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`.

**API-format**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Parameter | Godkända/standardvärden |
| --- | --- |
| `property` | Anger den egenskap som ska filtreras efter, till exempel status. Godtagbara värden för status är: `APPROVED`, `REJECTED` och `IN_PROGRESS`. |
| `start` | Standardvärdet för start är `0`. |
| `limit` | Standardvärdet för gräns är `20`. |
| `orderBy` | Sorterar posterna i stigande eller fallande ordning. |
| `requestType` | Accepterar antingen `INCOMING` eller `OUTGOING`. |

**Begäran**

Följande begäran returnerar en lista över alla utgående och inkommande delningsbegäranden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Ett godkänt svar returnerar en lista över utgående och inkommande delningsbegäranden och deras information.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Överför paket

Använd slutpunkten `/transfer` i sandlådans verktyg-API för att hämta och skapa nya paketdelningsbegäranden.

### Ny delningsbegäran {#share-request}

Hämta en publicerad källorganisations paket och dela det med en målorganisation genom att göra en POST-förfrågan till slutpunkten `/transfer` samtidigt som paket-ID och målorganisations-ID tillhandahålls.

**API-format**

```http
POST /transfer
```

**Begäran**

Följande begäran hämtar ett paket med källorganisationer och delar det med en målorganisation.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `packageId` | ID:t för det paket som du vill dela. | Sträng | Ja |
| `targets` | En lista över organisationer att dela till paketera med. | Array | Ja |

**Svar**

Ett lyckat svar returnerar information om det begärda paketet och dess delningsstatus.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### Hämta en delningsbegäran via ID {#fetch-transfer-by-id}

Hämta information om en delningsbegäran genom att göra en GET-begäran till `/transfer/{TRANSFER_ID}`-slutpunkten och ange överförings-ID.

**API-format**

```http
GET /transfer/{TRANSFER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{TRANSFER_ID}` | ID:t för överföringen som du vill hämta. |

**Begäran**

Följande begäran hämtar en överföring med ID:t {TRANSFER_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Svar**

Ett svar om att åtgärden lyckades returnerar information om en delningsbegäran.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### Hämta resurslista {#transfers-list}

Hämta en lista över överföringsbegäranden genom att göra en GET-begäran till `/transfer/list?{QUERY_PARAMETERS}`-slutpunkten och ändra frågeparametrarna efter behov.

**API-format**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Parameter | Godkända/standardvärden |
| --- | --- |
| `property` | Anger den egenskap som ska filtreras efter, till exempel status. Godtagbara värden för status är: `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`. |
| `start` | Standardvärdet för start är `0`. |
| `limit` | Standardvärdet för gräns är `20`. |
| `orderBy` | Beställningen accepterar endast fältet `createdDate`. |

**Begäran**

Följande begäran hämtar en lista med överföringsbegäranden från de angivna sökparametrarna.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Svar**

Ett godkänt svar returnerar en lista med alla överföringsbegäranden från de angivna sökparametrarna.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Uppdatera paketets tillgänglighet från privat till offentlig {#update-availability}

Ändra ett paket från privat till offentlig genom att göra en GET-begäran till slutpunkten `/packages/update`. Som standard skapas ett paket med privat tillgänglighet.

**API-format**

```http
PUT `/packages/update`
```

**Begäran**

Följande begäran ändrar ett pakets tillgänglighet från privat till offentlig.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `id` | ID:t för paketet som ska uppdateras. | Sträng | Ja |
| `action` | Om du vill uppdatera synligheten till publik ska åtgärdsvärdet vara **UPDATE**. | Sträng | Ja |
| `packageVisbility` | PaketVisibility-värdet bör vara **PUBLIC** för att uppdatera synligheten. | Sträng | Ja |

**Svar**

Ett godkänt svar returnerar information om ett paket och dess synlighet.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Begäran om att importera ett publikt paket {#pull-public-package}

Importera ett paket från en källorganisation med publik tillgänglighet genom att göra en POST-förfrågan till slutpunkten `/transfer/pullRequest`.

**API-format**

```http
POST /transfer/pullRequest
```

**Begäran**

Följande begäran importerar ett paket och anger dess tillgänglighet som publik.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `imsOrgId` | ID:t från paketets källorganisation. | Sträng | Ja |
| `packageId` | ID:t från paketet som ska importeras. | Sträng | Ja |

**Svar**

Ett lyckat svar returnerar information om det importerade publika paketet.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Visa offentliga paket {#list-public-packages}

Hämta en lista över paket med offentlig synlighet genom att göra en GET-begäran till slutpunkten `/transfer/list?{QUERY_PARAMS}`.

**API-format**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Parameter | Godkända/standardvärden |
| --- | --- |
| `property` | Anger den egenskap som ska filtreras efter, till exempel status. Godtagbara värden för status är: `COMPLETED` och `FAILED`. |
| `start` | Standardvärdet för start är `0`. |
| `limit` | Standardvärdet för gräns är `20`. |
| `orderBy` | Beställningen accepterar endast fältet `createdDate`. |
| `requestType` | Accepterar antingen `PUBLIC` eller `PRIVATE`. |

**Begäran**

Följande begäran hämtar en lista över paket med allmän tillgänglighet.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Ett lyckat svar returnerar en lista med publika paket och deras information.

+++Visa svar

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Kopiera paketnyttolast (#package-payload)

Du kan kopiera ett publikt pakets nyttolast genom att göra en GET-begäran till slutpunkten `/packages/payload` som innehåller motsvarande ID för paketet i sökvägen för begäran.

**API-format**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{PACKAGE_ID}` | ID:t för det paket som du vill kopiera. |

**Begäran**

Följande begäran hämtar ett pakets nyttolast med ID:t {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| Egenskap | Beskrivning | Typ | Obligatoriskt |
| --- | --- | --- | --- |
| `imsOrdId` | ID:t för organisationen som paketet tillhör. | Sträng | Ja |
| `packageId` | ID:t för det paket som du begär nyttolast. | Sträng | Ja |

**Svar**

Ett lyckat svar returnerar paketets nyttolast.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```
