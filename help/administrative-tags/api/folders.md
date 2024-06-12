---
title: Slutpunkt för mappar
description: Lär dig hur du skapar, uppdaterar, hanterar och tar bort mappar med Adobe Experience Platform API:er.
role: Developer
source-git-commit: 8f9a2b5a2063b76518302eb9de38b628c87416e1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---


# Mappslutpunkt

>[!IMPORTANT]
>
>Slutpunkts-URL för den här uppsättningen slutpunkter är `https://experience.adobe.io`.

Mappar är en funktion som gör att du kan ordna dina affärsobjekt bättre för enklare navigering och kategorisering.

Den här handboken innehåller information som hjälper dig att förstå mappar bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med mappar {#list}

Du kan hämta en lista över mappar som tillhör din organisation genom att göra en GET-förfrågan till `/folder` slutpunkt och ange mapptyp och ID för överordnad mapp.

**API-format**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |
| `{PARENT_FOLDER_ID}` | ID för den överordnade mapp som du hämtar listan med mappar från. Om du vill visa en lista över alla överordnade mappar använder du mapp-ID:t `root`. |

**Begäran**

+++En exempelbegäran om att lista alla datamappar på den översta nivån

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över alla mappar på den översta nivån för datauppsättningen i organisationen.

+++Ett exempelsvar som innehåller en lista över alla mappar på den översta nivån för datauppsättningen i organisationen.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Skapa en ny mapp {#create}

Du kan skapa en ny mapp genom att göra en POST-förfrågan till `/folder` slutpunkt och ange mapptyp.

**API-format**

```http
POST /folder/{FOLDER_TYPE}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |

**Begäran**

+++En exempelbegäran om att skapa en ny mapp.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på mappen som du vill skapa. |
| `parentId` | ID för den överordnade mappen. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nya mapp.

+++Ett exempelsvar som innehåller information om den nyligen skapade mappen.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | ID för den nyligen skapade mappen. |
| `createdBy` | ID för den användare som skapade mappen. |
| `createdAt` | Tidsstämpeln för när mappen skapades. |
| `modifiedBy` | ID för den användare som senast ändrade mappen. |
| `modifiedAt` | Tidsstämpeln för när mappen senast uppdaterades. |

+++

## Hämta en specifik mapp {#get}

Du kan hämta en specifik mapp som tillhör din organisation genom att göra en GET-förfrågan till `/folder` slutpunkt och ange mapptyp och mappens ID.

**API-format**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |
| `{FOLDER_ID}` | ID:t för mappen som du hämtar. |

**Begäran**

+++En exempelbegäran för att hämta en specifik mapp

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den begärda mappen.

+++Ett exempelsvar som innehåller information om den begärda mappen.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | ID för den begärda mappen. |
| `name` | Namnet på den begärda mappen. |
| `parentId` | ID för den överordnade mappen. |
| `createdBy` | ID för den användare som skapade mappen. |
| `createdAt` | Tidsstämpeln för när mappen skapades. |
| `modifiedBy` | ID för den användare som senast uppdaterade mappen. |
| `modifiedAt` | Tidsstämpeln för när mappen senast uppdaterades. |
| `status` | Status för den begärda mappen. Värden som stöds är `IN_USE` och `ARCHIVED`. |

+++

## Validera en angiven mapp {#validate}

Du kan validera om en mapp är berättigad att ha objekt genom att göra en GET-förfrågan till `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` och ange både mapptyp och ID.

**API-format**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |
| `{FOLDER_ID}` | ID för mappen som du validerar. |

**Begäran**

+++En exempelbegäran om att validera en specifik mapp

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

En lyckad status returnerar HTTP-status 200 med information om mappen som du validerar.

+++Ett exempelsvar innehåller information om den validerade mappen

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Uppdatera en specifik mapp {#update}

Du kan uppdatera informationen om en viss mapp som tillhör din organisation genom att göra en PATCH-förfrågan till `/folder` slutpunkt och ange mapptyp och mappens ID.

**API-format**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |
| `{FOLDER_ID}` | ID:t för mappen som du uppdaterar. |

**Begäran**

+++En exempelbegäran om att uppdatera en specifik mapp

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade mappen.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Ta bort en specifik mapp {#delete}

Du kan ta bort en viss mapp som tillhör din organisation genom att göra en DELETE-förfrågan till `/folder` och ange mapptyp och mappens ID.

***API-format**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Den typ av objekt som finns i mappen. Värdena som stöds är `segment` och `dataset`. |
| `{FOLDER_ID}` | ID för mappen som du tar bort. |

**Begäran**

+++En exempelbegäran om att ta bort en viss mapp

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett godkänt svar returnerar HTTP-status 200 med ett meddelande som informerar dig om att mappen har tagits bort.

```json
{
    "message": "delete request accepted successfully"
}
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur du skapar, hanterar och tar bort mappar med Adobe Experience Platform API.
