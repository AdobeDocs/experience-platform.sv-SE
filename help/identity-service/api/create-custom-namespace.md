---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Skapa ett anpassat namnutrymme
topic: API guide
description: Med API:t för identitetsnamnområde kan du skapa ett anpassat identitetsnamnutrymme som bara är tillgängligt för din organisation.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 2%

---


# Skapa ett anpassat namnutrymme

Med API:t kan du skapa ett anpassat ID-namnutrymme som bara är tillgängligt för din organisation. [!DNL Identity Namespace]

Rekommendationer om hur du skapar anpassade namnutrymmen finns [i dokumentationen](../troubleshooting-guide.md)om vanliga frågor om identitetstjänsten.

>[!NOTE]
>
>Namnutrymmen är en kvalificerare för identiteter. När ett namnutrymme har skapats kan det därför inte tas bort.

**API-format**

```http
POST /idnamespace/identities
```

**Begäran**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Svar**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Nästa steg

Gå vidare till nästa självstudiekurs för att [visa en identitets egna ID](./list-native-id.md)