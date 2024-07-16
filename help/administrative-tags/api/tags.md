---
title: Slutpunkt för enhetliga taggar
description: Lär dig hur du skapar, uppdaterar, hanterar och tar bort taggkategorier och taggar med Adobe Experience Platform API:er.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 1%

---

# Slutpunkt för enhetliga taggar

>[!IMPORTANT]
>
>Slutpunkts-URL för den här uppsättningen slutpunkter är `https://experience.adobe.io`.

Taggar är en funktion som gör att du kan hantera taxonomier för att klassificera affärsobjekt så att de blir enklare att identifiera och kategorisera. Du kan sedan ordna dessa taggar i ytterligare grupper genom att lägga till dem i taggkategorier.

Den här handboken innehåller information som hjälper dig att förstå taggar och taggkategorier bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här handboken är en del av Adobe Experience Platform API:er. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop

### Ordlista

I följande ordlista markeras skillnaden mellan en **tagg** och en **taggkategori**.

- **Tagg**: Med en tagg kan du hantera metadatataxonomin för affärsobjekt, vilket gör att du kan klassificera dessa objekt för enklare identifiering och kategorisering.
   - **Okategoriserad tagg**: En okategoriserad tagg är en tagg som inte tillhör en taggkategori. Som standard delas skapade taggar upp.
- **Taggkategori**: Med en taggkategori kan du gruppera dina taggar i meningsfulla uppsättningar, så att du kan skapa mer kontext för taggens syfte.

## Hämta en lista med taggkategorier {#get-tag-categories}

Du kan hämta en lista med taggkategorier som tillhör din organisation genom att göra en GET-förfrågan till slutpunkten `/tagCategory`.

**API-format**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Följande valfria frågeparametrar kan användas när taggkategorier hämtas.

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `start` | Platsen där resultatlistan börjar. Du kan använda detta för att ange startindex för numrering av resultat. | `start=a` |
| `limit` | Det maximala antalet taggkategorier som du vill hämta per sida. | `limit=20` |
| `property` | Det attribut som du vill filtrera efter när du hämtar taggkategorier. Värden som stöds är: &lt;ul≥<li>`name`: Namnet på taggkategorin.</li></ul> | `property=name==category` |
| `sortBy` | Den ordning i vilken taggkategorierna sorteras. Värden som stöds är `name`, `createdAt` och `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Den riktning som taggkategorierna sorteras efter. Värden som stöds är `asc` och `desc`. | `sortOrder=asc` |

**Begäran**

+++En exempelbegäran om att lista alla taggkategorier i organisationen

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över alla taggkategorier för din organisation.

+++Ett exempelsvar som innehåller en lista över alla taggkategorier i organisationen.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Skapa en ny taggkategori {#create-tag-category}

>[!IMPORTANT]
>
>Endast systemadministratören och produktadministratören kan använda detta API-anrop.

Du kan skapa en ny taggkategori genom att göra en POST-förfrågan till slutpunkten `/tagCategory`.

**API-format**

```http
POST /tagCategory
```

**Begäran**

+++En exempelbegäran om att skapa en ny taggkategori.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på den taggkategori som du vill skapa. |
| `description` | En beskrivning av den taggkategori som du vill skapa. |

+++

**Svar**

Ett exempelsvar returnerar HTTP-status 200 med information om din nyligen skapade taggkategori.

+++Ett exempelsvar som innehåller information om den nyligen skapade taggkategorin.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Hämta en specifik taggkategori {#get-tag-category}

Du kan hämta en specifik taggkategori som tillhör din organisation genom att göra en GET-förfrågan till `/tagCategory`-slutpunkten och ange taggkategorins ID.

**API-format**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID:t för den taggkategori som du hämtar. |

**Begäran**

+++En exempelbegäran om att hämta en specifik taggkategori

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna taggkategorin.

+++Ett exempelsvar som innehåller information om den angivna taggkategorin.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | ID för den begärda taggkategorin. |
| `name` | Namnet på den begärda taggkategorin. |
| `description` | Beskrivningen av den begärda taggkategorin. |
| `createdBy` | ID för den användare som skapade taggkategorin. |
| `createdAt` | Tidsstämpeln som användes när taggkategorin skapades. |
| `modifiedBy` | ID för den användare som senast uppdaterade taggkategorin. |
| `modifiedAt` | Tidsstämpeln för när taggkategorin senast uppdaterades. |
| `tagCount` | Antalet taggar som tillhör taggkategorin. |

+++

## Uppdatera en specifik taggkategori {#update-tag-category}

>[!IMPORTANT]
>
>Endast systemadministratören och produktadministratören kan använda detta API-anrop.

Du kan uppdatera information om en specifik taggkategori som tillhör din organisation genom att göra en PATCH-begäran till `/tagCategory`-slutpunkten och ange taggkategorins ID.

**API-format**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID:t för den taggkategori som du hämtar. |

**Begäran**

+++En exempelbegäran om att uppdatera en specifik taggkategori

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `op` | Den slutförda åtgärden. Om du vill uppdatera en specifik taggkategori anger du värdet `replace`. |
| `path` | Sökvägen till det fält som ska uppdateras. Värden som stöds är `name` och `description`. |
| `value` | Det uppdaterade värdet för fältet som du vill uppdatera. |
| `from` | Det ursprungliga värdet för det fält som du vill uppdatera. |

+++

**Svar**

HTTP-status 200 med information om den nyligen uppdaterade taggkategorin har slutförts.

+++Ett exempelsvar som innehåller information om den nyligen uppdaterade taggkategorin.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Ta bort en specifik taggkategori {#delete-tag-category}

>[!IMPORTANT]
>
>Endast systemadministratören och produktadministratören kan använda detta API-anrop.

Du kan ta bort en specifik taggkategori som tillhör din organisation genom att göra en DELETE-begäran till `/tagCategory`-slutpunkten och ange taggkategorins ID.

**API-format**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | ID:t för den taggkategori som du hämtar. |

**Begäran**

+++En exempelbegäran om att ta bort en specifik taggkategori

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt svar.

## Hämta en lista med taggar {#get-tags}

Du kan hämta en lista med taggar som tillhör din organisation genom att göra en GET-förfrågan till slutpunkten `/tags` och ID:t för taggkategorin.

**API-format**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Följande valfria frågeparametrar kan användas vid hämtning av taggar.

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `start` | Platsen där resultatlistan börjar. Du kan använda detta för att ange startindex för numrering av resultat. | `start=a` |
| `limit` | Det maximala antalet taggar som du vill hämta per sida. | `limit=20` |
| `property` | Det attribut som du vill filtrera efter när du hämtar taggar. Följande värden stöds:<ul><li>`name`: Namnet på taggen.</li><li>`archived`: Om taggarna har arkiverats eller inte har arkiverats. Du kan ange det här värdet till antingen `true` eller `false`.</li><li>`tagCategoryId`: ID:t för den taggkategori som taggen tillhör.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | Den ordning i vilken taggarna sorteras. Värden som stöds är `name`, `createdAt` och `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Den riktning som taggkategorierna sorteras efter. Värden som stöds är `asc` och `desc`. | `sortOrder=asc` |


**Begäran**

+++En exempelbegäran om att hämta alla taggar som tillhör en viss taggkategori

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om taggarna som tillhör den taggkategorin.

+++ Ett exempelsvar som innehåller information om de begärda taggarna.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Skapa en ny tagg {#create-tag}

>[!IMPORTANT]
>
>Det är bara systemadministratören och produktadministratören som kan använda det här API-anropet för att skapa en ny tagg i en angiven taggkategori.
>
>Om du skapar en tagg som inte är kategoriserad behöver du **inte** administratörsbehörighet.

Du kan skapa en ny tagg genom att göra en POST-förfrågan till slutpunkten `/tags`.

**API-format**

```http
POST /tags
```

**Begäran**

+++En exempelbegäran om att skapa en ny tagg.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | **Krävs**. Namnet på taggen som du vill skapa. |
| `tagCategoryId` | *Valfritt*. ID:t för den taggkategori som du vill att taggen ska tillhöra. Om den inte anges skapas taggen som en del av kategorin Ej kategoriserad. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om taggen som du nyss skapade.

+++Ett exempelsvar som innehåller information om den nyligen skapade taggen.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `name` | Namnet på den nyligen skapade taggen. |
| `id` | ID för den nyligen skapade taggen. |
| `org` | ID:t för organisationen som taggen tillhör. |
| `createdAt` | Tidsstämpeln som användes när taggen skapades. |
| `createdBy` | ID för den användare som skapade taggen. |
| `modifiedAt` | Tidsstämpeln för när taggen senast uppdaterades. |
| `modifiedBy` | ID för den användare som senast uppdaterade taggen. |
| `tagCategoryId` | ID:t för den taggkategori som taggen tillhör. |
| `tagCategoryName` | Namnet på den taggkategori som taggen tillhör. |

+++

## Hämta en specifik tagg {#get-tag}

Du kan hämta en specifik tagg som tillhör din organisation genom att göra en GET-förfrågan till slutpunkten `/tags` och ange ID:t för taggen som du vill hämta.

**API-format**

```http
GET /tags/{TAG_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_ID}` | ID:t för taggen som du hämtar. |

**Begäran**

+++En exempelbegäran om att hämta en specifik tagg

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna taggen.

+++Ett exempelsvar som innehåller information om den angivna taggen.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `name` | Namnet på taggen som du hämtade. |
| `id` | ID:t för taggen som du hämtade. |
| `org` | ID:t för organisationen som taggen tillhör. |
| `createdAt` | Tidsstämpeln som användes när taggen skapades. |
| `createdBy` | ID för den användare som skapade taggen. |
| `modifiedAt` | Tidsstämpeln för när taggen senast uppdaterades. |
| `modifiedBy` | ID för den användare som senast uppdaterade taggen. |
| `tagCategoryId` | ID:t för den taggkategori som taggen tillhör. |
| `tagCategoryName` | Namnet på den taggkategori som taggen tillhör. |
| `archived` | Taggens arkiveringsstatus. Om värdet är `true` betyder det att taggen arkiveras. |

+++

## Validera taggar {#validate-tags}

Du kan validera om det finns taggar genom att göra en POST-förfrågan till slutpunkten `/tags/validate`.

**API-format**

```http
POST /tags/validate
```

**Begäran**

+++Ett exempel på en begäran om validering av de angivna tagg-ID:n.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `ids` | En array som innehåller en lista med tagg-ID:n som du vill validera. |
| `entity` | Den entitet som begär valideringen. Du kan använda värdet `{API_KEY}` för den här parametern. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om vilka taggar som är giltiga och ogiltiga.

+++Ett exempelsvar som visar vilka taggar som är giltiga och ogiltiga.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `invalidTags` | En array som innehåller en lista med ogiltiga tagg-ID:n. |
| `validTags` | En array som innehåller en lista med giltiga tagg-ID:n. |

+++

## Uppdatera en specifik tagg {#update-tag}

Du kan uppdatera en angiven tagg genom att göra en PATCH-förfrågan till slutpunkten `/tags` och ange ID:t för taggen som du vill uppdatera.

**API-format**

```http
PATCH /tags/{TAG_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_ID}` | ID:t för taggen som du uppdaterar. |

**Begäran**

+++En exempelbegäran om att uppdatera en specifik tagg

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `op` | Den åtgärd som måste utföras. I det här fallet ställs den alltid in på `replace`. |
| `path` | Sökvägen till det fält som ska uppdateras. Värden som stöds är `name`, `archived` och `tagCategoryId`. |
| `value` | Det uppdaterade värdet för fältet som du vill uppdatera. |
| `from` | Det ursprungliga värdet för det fält som du vill uppdatera. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade taggen.

+++Ett exempelsvar som innehåller information om den uppdaterade taggen.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Ta bort en specifik tagg {#delete-tag}

>[!IMPORTANT]
>
>Endast systemadministratören och produktadministratören kan använda detta API-anrop.
>
>Dessutom kan taggen **inte** kopplas till några affärsobjekt och **måste** arkiveras innan du kan ta bort taggen. Du kan arkivera taggen med [slutpunkten för uppdateringstaggen](#update-tag).

Du kan ta bort en viss tagg genom att lägga till taggen DELETE i `/tags`-slutpunkten och ange ID:t för taggen som du vill ta bort.

**API-format**

```http
DELETE /tags/{TAG_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TAG_ID}` | ID:t för taggen som du tar bort. |

**Begäran**

+++En exempelbegäran om att ta bort en specifik tagg

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt svar.

## Nästa steg

När du har läst den här guiden får du en bättre förståelse för hur du skapar, hanterar och tar bort taggar och taggkategorier med Adobe Experience Platform API:er. Mer information om hur du hanterar taggar med användargränssnittet finns i [handboken om hantering av taggar](../ui/managing-tags.md). Mer information om hur du hanterar taggkategorier med hjälp av användargränssnittet finns i [guiden för taggkategorier](../ui/tags-categories.md).
