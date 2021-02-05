---
keywords: Experience Platform;hem;populära ämnen;identitet;Identitet
solution: Experience Platform
title: Lista identitetsmappningar
topic: API guide
description: En mappning är en samling med alla identiteter i ett kluster för ett angivet namnområde.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Visa identitetsmappningar

En mappning är en samling med alla identiteter i ett kluster för ett angivet namnområde.

## Hämta en identitetsmappning för en enskild identitet

Om en identitet anges hämtar du alla relaterade identiteter från samma namnområde som representeras av identiteten i begäran.

**API-format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Begäran**

Alternativ 1: Ange identiteten som namnutrymme (`nsId`, efter ID) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 2: Ange identiteten som namnutrymme (`ns`, efter namn) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 3: Ange identiteten som XID (`xid`). Mer information om hur du hämtar en identitets XID finns i avsnittet i det här dokumentet som handlar om [att hämta XID för en identitet](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Hämta identitetsmappningar för flera identiteter

Använd metoden `POST` som en batchmotsvarighet till metoden `GET` som beskrivs ovan för att hämta mappningar för flera identiteter.

>[!NOTE]
>
>Begäran får inte innehålla fler än 1 000 identiteter. Begäranden som överskrider 1 000 identiteter resulterar i 400-statuskod.

**API-format**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Begärandetext**

Alternativ 1: Ange en lista med XID:n som mappningar ska hämtas för.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Alternativ 2: Ange en lista över identiteter som sammansatta ID:n, där varje namn anger ID-värdet och namnutrymmet per namnområdes-ID. I det här exemplet visas hur du använder den här metoden när du skriver över standardvärdet `graph-type` för &quot;Privat diagram&quot;.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Begäran**

**Använda XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Använda UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Om inga relaterade identiteter hittades med angivna indata returneras en `HTTP 204`-svarskod utan innehåll.

**Svar**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: Tidsstämpeln när indataidentiteten senast associerades med den här identiteten.
- `regions`: Anger  `regionId` och  `lastAssociationTime` för var identiteten sågs.

## Nästa steg

Gå till nästa självstudiekurs för att [visa tillgängliga namnutrymmen](./list-namespaces.md).
