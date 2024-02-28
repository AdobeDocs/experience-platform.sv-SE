---
keywords: Experience Platform;hem;populära ämnen;lissandlådor
solution: Experience Platform
title: API-slutpunkt för sandlådetyper
description: Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till slutpunkten /sandboxTypes.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# Slutpunkt för sandlådetyper

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-förfrågan till `/sandboxTypes` slutpunkt.

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista över sandlådetyper som stöds

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-förfrågan till `/sandboxTypes` slutpunkt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
