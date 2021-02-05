---
keywords: Experience Platform;hem;populära ämnen;lista identiteter;listkluster
solution: Experience Platform
title: Visa alla identiteter i ett kluster
topic: API guide
description: Identiteter som är relaterade till ett identitetsdiagram, oavsett namnutrymme, anses ingå i samma kluster i det identitetsdiagrammet. Med alternativen nedan får du tillgång till alla klustermedlemmar.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Visa alla identiteter i ett kluster

Identiteter som är relaterade till ett identitetsdiagram, oavsett namnutrymme, anses ingå i samma kluster i det identitetsdiagrammet. Med alternativen nedan får du tillgång till alla klustermedlemmar.

## Hämta associerade identiteter för en enda identitet

Hämta alla klustermedlemmar för en enda identitet.

Du kan använda den valfria parametern `graph-type` för att ange identitetsdiagrammet som klustret ska hämtas från. Alternativen är:

- Ingen - Utför ingen identitetssammanfogning.
- Privat diagram - Utför identitetssammanfogning baserat på ditt privata identitetsdiagram. Om `graph-type` inte anges är detta standardvärde.

**API-format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Begäran**

Alternativ 1: Ange identiteten som namnutrymme (`nsId`, efter ID) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 2: Ange identiteten som namnutrymme (`ns`, efter namn) och ID-värde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Alternativ 3: Ange identiteten som XID (`xid`). Mer information om hur du hämtar en identitets XID finns i avsnittet i det här dokumentet som handlar om [att hämta XID för en identitet](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Hämta associerade identiteter för flera identiteter

Använd `POST` som en gruppmotsvarighet till metoden `GET` som beskrivs ovan för att returnera identiteterna i klustren med flera identiteter.

>[!NOTE]
>
>Begäran får inte innehålla fler än 1 000 identiteter. Begäranden som överskrider 1 000 identiteter resulterar i 400-statuskod.

**API-format**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Begäran**

Följande begäran visar en lista med XID:n som klustermedlemmar ska hämtas för.

**Stub-förfrågan**

Användning av `x-uis-cst-ctx: stub`-huvudet returnerar ett stötningssvar. Detta är en tillfällig lösning som underlättar utvecklingen av tidig integration medan tjänsterna är färdiga. Detta kommer att bli inaktuellt när det inte längre behövs.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Ring med XID:n**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Ring med UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Svar**

**Stubbed-svar**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Fullständigt svar**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>Svaret har alltid en post för varje XID som anges i begäran, oavsett om en begärans XID tillhör samma kluster eller om ett eller flera har ett kluster kopplat över huvud taget.

## Nästa steg

Gå till nästa självstudiekurs för att [visa klusterhistoriken för en identitet](./list-cluster-history.md)