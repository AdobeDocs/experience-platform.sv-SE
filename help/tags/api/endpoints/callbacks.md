---
title: Återanropsslutpunkt
description: Lär dig hur du anropar slutpunkten /callback i Reactor API.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 3%

---

# Återanropsslutpunkt

Ett återanrop är ett meddelande som Reactor API skickar till en specifik URL (vanligtvis en som din organisation är värd för).

Återanrop är avsedda att användas tillsammans med [granskningshändelser](./audit-events.md) för att spåra aktiviteter i Reaktors API. Varje gång en granskningshändelse av en viss typ genereras kan ett återanrop skicka ett matchande meddelande till den angivna URL:en.

Tjänsten bakom URL:en som anges i återanropet måste svara med HTTP-statuskoden 200 (OK) eller 201 (Skapad). Om tjänsten inte svarar med någon av dessa statuskoder provas meddelandeleveransen igen med följande intervall:

* 1 minut
* 5 minuter
* 30 minuter
* 1 timme
* 12 timmar
* 1 dag
* 3 dagar

>[!NOTE]
>
>Återförsöksintervall är relativa till föregående intervall. Om till exempel ett försök misslyckas på en minut schemaläggs nästa försök i fem minuter efter att ett försök på en minut misslyckades (sex minuter efter att meddelandet genererades).

Om alla leveransförsök misslyckas ignoreras meddelandet.

Ett återanrop tillhör exakt en [egenskap](./properties.md). En egenskap kan ha många återanrop.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Visa återanrop {#list}

Du kan visa alla återanrop under en egenskap genom att göra en GET-förfrågan.

**API-format**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beskrivning |
| --- | --- |
| `{PROPERTY_ID}` | `id` för egenskapen vars återanrop du vill visa. |

{style="table-layout:auto"}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade återanrop filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Mer information finns i guiden om [filtrering av svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med återanrop för den angivna egenskapen.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Söka efter ett återanrop {#lookup}

Du kan slå upp ett återanrop genom att ange dess ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `CALLBACK_ID` | `id` för det återanrop som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar detaljerna för återanropet.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Skapa ett återanrop {#create}

Du kan skapa ett nytt återanrop genom att göra en POST.

**API-format**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | `id` för [egenskapen](./properties.md) som du definierar återanropet under. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `url` | URL-målet för återanropsmeddelandet. URL:en måste använda HTTPS-protokolltillägget. |
| `subscriptions` | En array med strängar som anger de granskningshändelsetyper som kommer att utlösa återanropet. En lista med möjliga händelsetyper finns i [slutpunktshandboken för granskningshändelser](./audit-events.md). |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om det nya återanropet.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Uppdatera ett återanrop

Du kan uppdatera ett återanrop genom att ta med dess ID i sökvägen för en PATCH-begäran.

**API-format**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `CALLBACK_ID` | `id` för det återanrop som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Följande begäran uppdaterar `subscriptions`-arrayen för ett befintligt återanrop.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | Ett objekt vars egenskaper representerar de attribut som ska uppdateras för återanropet. Varje nyckel representerar det callback-attribut som ska uppdateras, tillsammans med motsvarande värde som det ska uppdateras till.<br><br>Följande attribut kan uppdateras för återanrop:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | `id` för det återanrop som du vill uppdatera. Det här bör matcha det `{CALLBACK_ID}`-värde som anges i sökvägen till begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `callbacks`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om det uppdaterade återanropet.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Ta bort ett återanrop

Du kan ta bort ett återanrop genom att ta med dess ID i sökvägen för en DELETE-begäran.

**API-format**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `CALLBACK_ID` | `id` för det återanrop som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext, vilket anger att återanropet har tagits bort.
