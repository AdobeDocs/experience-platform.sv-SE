---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ta bort en resurs
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Ta bort en resurs

Ibland kan det vara nödvändigt att ta bort (DELETE) en resurs från [!DNL Schema Registry]. Endast resurser som du skapar i innehavarbehållaren kan tas bort. Detta görs genom att utföra en DELETE-begäran med hjälp `$id` av resursen som du vill ta bort.

**API-format**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska tas bort från [!DNL Schema Library]. Giltiga typer är `datatypes`, `mixins`, `schemas`och `classes`. |
| `{RESOURCE_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` resursen. |

**Begäran**

DELETE kräver inte att du accepterar sidhuvuden.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) till resursen. Du måste inkludera en Accept-rubrik i begäran, men du bör få HTTP-status 404 (Hittades inte) eftersom resursen har tagits bort från [!DNL Schema Registry].