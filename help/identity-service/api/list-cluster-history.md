---
keywords: Experience Platform;hem;populära ämnen;identiteter;klusterhistorik
solution: Experience Platform
title: Hämta klusterhistorik för en identitet
description: Identiteter kan flytta kluster under olika enhetsgrafkörningar. Identitetstjänsten ger synlighet i klusterassociationerna för en viss identitet över tiden.
role: Developer
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Hämta klusterhistoriken för en identitet

Identiteter kan flytta kluster under olika enhetsgrafkörningar. [!DNL Identity Service] ger synlighet i klusterassociationerna för en viss identitet över tiden.

Använd den valfria parametern `graph-type` för att ange vilken utdatatyp som klustret ska hämtas från. Alternativ:

- `None` - Utför ingen identitetssammanslagning.
- `Private Graph` - Utför identitetssammanfogning baserat på ditt privata identitetsdiagram. Om `graph-type` inte anges är detta standardvärde.

## Hämta klusterhistoriken för en enskild identitet

**API-format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Begäran**

Alternativ 1: Ange identiteten som namnområde (`nsId`, efter ID) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 2: Ange identiteten som namnutrymme (`ns`, efter namn) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 3: Ange identiteten som XID (`xid`). Mer information om hur du hämtar en identitets XID finns i det här dokumentets avsnitt som handlar om [hämtning av ett XID för en identitet](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Hämta klusterhistoriken för flera identiteter

Använd metoden `POST` som en gruppmotsvarighet till metoden `GET` som beskrivs ovan för att returnera klusterhistoriken för flera identiteter.

>[!NOTE]
>
>Begäran får inte innehålla fler än 1 000 identiteter. Begäranden som överskrider 1 000 identiteter resulterar i 400-statuskod.

**API-format**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Begär brödtext**

Alternativ 1: Ange en lista med XID:n som klustermedlemmar ska hämtas för.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Alternativ 2: Ange en lista över identiteter som sammansatta ID:n, där varje namn anger ID-värdet och namnutrymmet efter namnutrymmeskod.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Begäran**

**Stub-förfrågan**

Användning av rubriken `x-uis-cst-ctx: stub` returnerar ett stötningssvar. Detta är en tillfällig lösning som underlättar utvecklingen av tidig integration medan tjänsterna är färdiga. Detta kommer att bli inaktuellt när det inte längre behövs.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Använda XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Använder UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
        "graph-type": "Private Graph"
      }' | json_pp
```

**Omdömen**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>Svaret har alltid en post för varje XID som anges i begäran, oavsett om en begärans XID tillhör samma kluster eller om ett eller flera har ett kluster kopplat över huvud taget.

## Nästa steg

Gå till nästa självstudiekurs för att [lista identitetsmappningar](./list-identity-mappings.md)
