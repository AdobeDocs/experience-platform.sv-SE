---
keywords: Experience Platform;hem;populära ämnen;lissandlådor
solution: Experience Platform
title: API-slutpunkt för sandlådetyper
topic-legacy: developer guide
description: Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till slutpunkten /sandboxTypes.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: e644fe9a2faf8692617f6bbee2b91a52c323ff5d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Slutpunkt för sandlådetyper

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till `/sandboxTypes`-slutpunkten.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anropen i det här dokumentet och viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

## Hämta en lista över sandlådetyper som stöds

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till `/sandboxTypes`-slutpunkten.

**API-format**

```http
GET /sandboxTypes
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådetyper som stöds för din organisation.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
