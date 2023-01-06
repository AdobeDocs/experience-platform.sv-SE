---
keywords: Experience Platform;hem;populära ämnen;namnutrymme;namnutrymme;namnutrymmen;namnutrymmen;namnutrymmen;namnområde;namnområde för identitet;identitet;identitet
solution: Experience Platform
title: Skapa ett anpassat namnutrymme i Identity Service API
description: Med API:t för identitetsnamnområde kan du skapa ett anpassat identitetsnamnutrymme som bara är tillgängligt för din organisation.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---

# Skapa ett anpassat namnutrymme i Identity Service API

Använda [!DNL Identity Namespace] API: du kan skapa ett anpassat ID-namnutrymme som bara är tillgängligt för din organisation.

Rekommendationer om hur du skapar anpassade namnutrymmen finns i [dokumentation om vanliga frågor om identitetstjänster](../troubleshooting-guide.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Gå till nästa självstudiekurs för att [lista ID:t för en identitet](./list-native-id.md)
