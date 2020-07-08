---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Hämta klusterhistorik för en identitet
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Hämta klusterhistoriken för en identitet

Identiteter kan flytta kluster under olika enhetsgrafkörningar. [!DNL Identity Service] ger synlighet i klusterassociationerna för en viss identitet över tid.

Använd den valfria `graph-type` parametern för att ange vilken utdatatyp som klustret ska hämtas från. Alternativen är:

- `None` - Utför ingen identitetssammanfogning.
- `Private Graph` - Utför identitetssammanfogning baserat på ditt privata identitetsdiagram. Om inget `graph-type` anges är detta standardvärde.

## Hämta klusterhistoriken för en enskild identitet

**API-format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Begäran**

Alternativ 1: Ange identiteten som namnutrymme (`nsId`, efter ID) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 2: Ange identiteten som namnutrymme (`ns`, efter namn) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 3: Ange identiteten som XID (`xid`). Mer information om hur du hämtar en identitets XID finns i avsnittet om att [hämta en identitets](./list-native-id.md)XID.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Hämta klusterhistoriken för flera identiteter

Använd `POST` metoden som en batchmotsvarighet till den `GET` metod som beskrivs ovan för att returnera klusterhistoriken för flera identiteter.

>[!NOTE]
>
>Begäran får inte innehålla fler än 1 000 identiteter. Begäranden som överskrider 1 000 identiteter resulterar i 400-statuskod.

**API-format**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Begärandetext**

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

Användning av sidhuvudet kommer att returnera ett statiskt svar `x-uis-cst-ctx: stub` . Detta är en tillfällig lösning som underlättar utvecklingen av tidig integration medan tjänsterna är färdiga. Detta kommer att bli inaktuellt när det inte längre behövs.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Använda UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Ändra**

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