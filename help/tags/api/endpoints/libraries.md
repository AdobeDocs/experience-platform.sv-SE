---
title: Bibliotekets slutpunkt
description: Lär dig hur du anropar slutpunkten /libraries i Reactor API.
exl-id: 0f7bc10f-2e03-43fa-993c-a2635f4d0c64
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 1%

---

# Bibliotekets slutpunkt

Ett bibliotek är en samling taggresurser ([tillägg](./extensions.md), [regler](./rules.md)och [dataelement](./data-elements.md)) som representerar önskat beteende för ett [property](./properties.md). The `/libraries` -slutpunkten i Reaktors-API gör att du kan hantera bibliotek i dina taggegenskaper programmatiskt.

Ett bibliotek tillhör exakt en egenskap. En egenskap kan ha många bibliotek.

## Komma igång

Slutpunkten som används i den här guiden är en del av [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Läs igenom [komma igång-guide](../getting-started.md) om du vill ha viktig information om hur du autentiserar till API:t.

Innan du arbetar med bibliotek i Reaktors-API:t är det viktigt att du förstår vilka roller bibliotekstillstånd och -miljöer spelar när du ska avgöra vilka åtgärder du kan utföra i ett visst bibliotek. Se guiden på [bibliotekets publiceringsflöde](../../ui/publishing/publishing-flow.md) för mer information.

## Hämta en lista med bibliotek {#list}

Du kan hämta en lista med bibliotek för en egenskap genom att ta med egenskapens ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /properties/{PROPERTY_ID}/libraries
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | The `id` av den egendom som äger biblioteken. |

{style="table-layout:auto"}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade bibliotek filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`name`</li><li>`published_at`</li><li>`stale`</li><li>`state`</li><li>`updated_at`</li></ul>Se guiden [filtrera svar](../guides/filtering.md) för mer information.

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med bibliotek för den angivna egenskapen.

```json
{
  "data": [
    {
      "id": "LBb174d60bdbd34f87a2e9466fadaacae0",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:44:10.776Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:44:10.776Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/data_elements",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/extensions",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/rules",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/property"
          },
          "data": {
            "id": "PR4bc17fb09ed845b1acfb0f6600a1f3c0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0",
        "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

## Söka i ett bibliotek {#lookup}

Du kan söka efter ett bibliotek genom att ange dess ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /libraries/{LIBRARY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `LIBRARY_ID` | The `id` för det bibliotek som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om biblioteket.

```json
{
  "data": {
    "id": "LB5862ee2dc21b4646a5536c8d6edb0c84",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:44:00.476Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:44:00.476Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property"
        },
        "data": {
          "id": "PRc90084c615844db58201d4e70d47b8bf",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRc90084c615844db58201d4e70d47b8bf",
      "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Skapa ett bibliotek {#create}

Du kan skapa ett nytt bibliotek genom att göra en POST.

**API-format**

```http
POST /properties/{PROPERTY_ID}/libraries
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | The `id` i [property](./properties.md) som du definierar biblioteket under. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skapar ett nytt bibliotek för den angivna egenskapen. När du först skapar ett bibliotek är det bara dess `name` kan konfigureras. Om du vill lägga till dataelement, tillägg och regler i biblioteket måste du skapa relationer. Se avsnittet om [hantera biblioteksresurser](#resources) för mer information.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Library"
          },
          "type": "libraries"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.name` | **(Obligatoriskt)** Ett läsbart namn för biblioteket. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `libraries`. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar information om det nyligen skapade biblioteket.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My library 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "libraries"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Hantera resurser för ett bibliotek {#resources}

De dataelement, tillägg, regler och miljöer som är kopplade till ett bibliotek etableras via relationer. Avsnitten nedan beskriver hur du hanterar dessa relationer via API-anrop.

### Lägga till resurser i ett bibliotek {#add-resources}

Du kan lägga till resurser i ett bibliotek genom att lägga till `/relationships` till sökvägen för en begäran om POST, följt av resurstypen.

**API-format**

```http
POST /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | ID:t för det bibliotek som du vill lägga till resurser i. |
| `{RESOURCE_TYPE}` | Den typ av resurs som du lägger till i biblioteket. Följande värden accepteras: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**Begäran**

Följande begäran lägger till två dataelement i ett bibliotek.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "DEce7fdee2afe44efeb4d974247d1e8dbe",
            "type": "data_elements"
          },
          {
            "id": "DE8097636264104451ac3a18c95d5ff833",
            "type": "data_elements"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID:t för resursen som du lägger till i biblioteket. |
| `type` | Den typ av resurs som du lägger till i biblioteket. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om de tillagda relationerna. Utföra en [sökförfrågan](#lookup) för biblioteket visar de tillagda relationerna under `relationships` -egenskap.

```json
{
  "data": [
    {
      "type": "data_elements",
      "id": "DEce7fdee2afe44efeb4d974247d1e8dbe"
    },
    {
      "id": "DE8097636264104451ac3a18c95d5ff833",
      "type": "data_elements"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/data_elements",
    "self": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/relationships/data_elements"
  }
}
```

### Ersätta resurserna för ett bibliotek {#replace-resources}

Du kan ersätta alla befintliga resurser av en viss typ för ett bibliotek genom att lägga till `/relationships` till sökvägen för en PATCH-begäran, följt av resurstypen som du ersätter.

**API-format**

```http
PATCH /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | ID:t för det bibliotek vars relationer du vill ersätta. |
| `{RESOURCE_TYPE}` | Den typ av resurs som du ersätter. Följande värden accepteras: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**Begäran**

Följande begäran ersätter tilläggen för ett bibliotek med tilläggen i `data` array.

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "EX58312732fd0f43f98037d765ef96c4cd",
            "type": "extensions"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID:t för resursen som du lägger till i biblioteket. |
| `type` | Den typ av resurs som du lägger till i biblioteket. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar information om de uppdaterade relationerna. Utföra en [sökförfrågan](#lookup) för biblioteket visar relationerna under `relationships` -egenskap.

```json
{
  "data": [
    {
      "type": "extensions",
      "id": "EX58312732fd0f43f98037d765ef96c4cd"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/extensions",
    "self": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/relationships/extensions"
  }
}
```

### Ta bort resurser för ett bibliotek {#remove-resources}

Du kan ta bort befintliga resurser från ett bibliotek genom att lägga till `/relationships` till sökvägen för en DELETE-begäran, följt av resurstypen som du tar bort.

**API-format**

```http
DELETE /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | ID för det bibliotek vars resurser du vill ta bort. |
| `{RESOURCE_TYPE}` | Den typ av resurs som du tar bort. Följande värden accepteras: <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**Begäran**

Följande begäran tar bort en regel från ett bibliotek. Alla befintliga regler som inte ingår i `data` arrayen tas inte bort.

```shell
curl -X DELETE \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "RLa16f7859c7404239940c2cf2ec02b03c",
            "type": "rules"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för resursen som du tar bort från biblioteket. |
| `type` | Den typ av resurs som du tar bort från biblioteket. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar information om de uppdaterade relationerna för resurstypen. Om det inte finns några relationer för den här resurstypen `data` -egenskapen returneras som en tom array. Utföra en [sökförfrågan](#lookup) för biblioteket visar relationerna under `relationships` -egenskap.

```json
{
  "data": [

  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/rules",
    "self": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/relationships/rules"
  }
}
```

## Tilldela ett bibliotek till en miljö {#environment}

Du kan tilldela ett bibliotek till en miljö  `/relationships/environment` till sökvägen för en begäran om POST.

**API-format**

```http
POST /libraries/{LIBRARY_ID}/relationships/environment
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | ID:t för det bibliotek som du vill tilldela. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för miljön som du tilldelar biblioteket till. |
| `type` | Måste anges till `environments`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar detaljerna om relationen. Utföra en [sökförfrågan](#lookup) för biblioteket visar den tillagda relationen under `relationships` -egenskap.

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments"
  },
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/environment",
    "self": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment"
  }
}
```

## Överföra ett bibliotek {#transition}

Du kan överföra ett bibliotek till ett annat publiceringstillstånd genom att ta med dess ID i sökvägen för en PATCH-begäran och ange ett lämpligt `meta.action` värdet i nyttolasten.

**API-format**

```http
PATCH /libraries/{LIBRARY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `LIBRARY_ID` | The `id` för det bibliotek som du vill gå över till. |

{style="table-layout:auto"}

**Begäran**

Följande begäran översätter tillståndet för ett befintligt bibliotek baserat på värdet för `meta.action` anges i nyttolasten. Vilka åtgärder som är tillgängliga för ett bibliotek beror på dess aktuella publiceringstillstånd, enligt beskrivningen i [publiceringsflöde](../../ui/publishing/publishing-flow.md#state).

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "LB80c337c956804738b2db2ea2f69fcdf0",
          "type": "libraries",
          "meta": {
            "action": "submit"
          }
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `meta.action` | Den specifika övergångsåtgärd som du vill utföra i biblioteket. Följande åtgärder är tillgängliga beroende på bibliotekets aktuella publiceringstillstånd: <ul><li>`develop`</li><li>`submit`</li><li>`approve`</li><li>`reject`</li></ul> |
| `id` | The `id` för det bibliotek som du vill uppdatera. Det här bör matcha `{LIBRARY_ID}` värdet som anges i sökvägen för begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `libraries`. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar information om det uppdaterade biblioteket.

```json
{
  "data": {
    "id": "LB80c337c956804738b2db2ea2f69fcdf0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:47:57.783Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:48:06.431Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/rules",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/property"
        },
        "data": {
          "id": "PRbc84c93c1c9f48c9836ade5ea4199006",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/last_build"
        },
        "data": {
          "id": "BL8d6e931f2f6d48ea96d6730122f13bcc",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRbc84c93c1c9f48c9836ade5ea4199006",
      "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Publicera ett bibliotek {#publish}

>[!NOTE]
>
>Endast godkända bibliotek får publiceras i produktionen.

Om du vill publicera ett bibliotek i produktionen ser du till att en produktionsmiljö har lagts till i biblioteket och skapar sedan ett bygge.

**API-format**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| Parameter | Beskrivning |
| --- | --- |
| `LIBRARY_ID` | The `id` för det bibliotek som du vill publicera. |

{style="table-layout:auto"}

**Begäran**

Denna begäran kräver ingen nyttolast.

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Svar**

```json
{
  "data": {
    "id": "BL162b63703eb74c6bb3c12471e0062c05",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:48:18.731Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:48:18.731Z",
      "token": "b223fc55df1c"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/environment"
        },
        "data": {
          "id": "EN5428335fff304c749f06a241db137a60",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/library"
        },
        "data": {
          "id": "LBa937e62887e94d85b77cbe703f5dfc56",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/property"
        },
        "data": {
          "id": "PR7e2b7aaaffcb499398010ba964603415",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN5428335fff304c749f06a241db137a60",
      "library": "https://reactor.adobe.io/libraries/LBa937e62887e94d85b77cbe703f5dfc56",
      "self": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/launch-5986a1b644a4-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/b223fc55df1c/launch-5986a1b644a4-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## Hantera anteckningar för ett bibliotek {#notes}

Bibliotek är&quot;betydande&quot; resurser, vilket innebär att du kan skapa och hämta textbaserade anteckningar för varje enskild resurs. Se [slutpunktshandbok för anteckningar](./notes.md) om du vill ha mer information om hur du hanterar anteckningar för bibliotek och andra kompatibla resurser.

## Hämta relaterade resurser för ett bibliotek {#related}

Följande anrop visar hur du hämtar relaterade resurser för ett bibliotek. När [söka efter ett bibliotek](#lookup), listas dessa relationer under `relationships` -egenskap.

Se [relationshandbok](../guides/relationships.md) för mer information om relationerna i Reactor API.

### Lista relaterade dataelement för ett bibliotek {#data-elements}

Du kan lista dataelement som används i ett bibliotek genom att lägga till `/data_elements` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/data_elements
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` i biblioteket vars dataelement du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med dataelement som använder det angivna biblioteket.

```json
{
  "data": [
    {
      "id": "DE4956628e8baa4b358cc592337049b37b",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:45:11.694Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:45:10 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:11.694Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/property"
          },
          "data": {
            "id": "PR245ca5e560784249b2a88ef82f2851b6",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/origin"
          },
          "data": {
            "id": "DE4c027939f2004fdcb15e3b4099e70974",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/extension"
          },
          "data": {
            "id": "EX5942ffd7fac94428875bd664e397bd47",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension"
          },
          "data": {
            "id": "EXbf411638b90843c486254b5ca0fe47d6",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR245ca5e560784249b2a88ef82f2851b6",
        "origin": "https://reactor.adobe.io/data_elements/DE4c027939f2004fdcb15e3b4099e70974",
        "self": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b",
        "extension": "https://reactor.adobe.io/extensions/EX5942ffd7fac94428875bd664e397bd47"
      },
      "meta": {
        "latest_revision_number": 1
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

### Lista relaterade tillägg för ett bibliotek {#extensions}

Du kan visa de tillägg som används i ett bibliotek genom att lägga till `/extensions` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/extensions
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` för det bibliotek vars tillägg du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med tillägg som använder det angivna biblioteket.

```json
{
  "data": [
    {
      "id": "EXac1e55883e5b47eb9a3589b311960677",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:45:23.759Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:23.759Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/property"
          },
          "data": {
            "id": "PR2d1f3ba867204dc7a4c17614d23bbab0",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/origin"
          },
          "data": {
            "id": "EX63cf3b91ec8146889759bbacb15627c3",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR2d1f3ba867204dc7a4c17614d23bbab0",
        "origin": "https://reactor.adobe.io/extensions/EX63cf3b91ec8146889759bbacb15627c3",
        "self": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
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

### Visa relaterade regler för ett bibliotek {#rules}

Du kan visa reglerna som används i ett bibliotek genom att lägga till `/rules` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/rules
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` för det bibliotek vars regler du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med regler som använder det angivna biblioteket.

```json
{
  "data": [
    {
      "id": "RL460e550125054fffb824cce56c8cb1ac",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:45:36.405Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:36.405Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/property"
          },
          "data": {
            "id": "PRa68d0d2c6e0a4ae380fb30f17f7c435d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/origin"
          },
          "data": {
            "id": "RL04911614524d463a9c115bea442bce72",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRa68d0d2c6e0a4ae380fb30f17f7c435d",
        "origin": "https://reactor.adobe.io/rules/RL04911614524d463a9c115bea442bce72",
        "self": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac",
        "rule_components": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
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

### Söka efter en relaterad miljö för ett bibliotek {#related-environment}

Du kan söka efter miljön som ett bibliotek tilldelas genom att lägga till `/environment` till sökvägen för en GET-begäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/environment
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` för det bibliotek vars miljö du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om miljön som det angivna biblioteket har tilldelats.

```json
{
  "data": {
    "id": "ENe66122e6793641d8a8453f63c42e4270",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:12.484Z",
      "library_path": "f9fd106ab399/2df53b69e8a2",
      "library_name": "launch-1d2ffee7eef5-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-1d2ffee7eef5-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.min.js"
          ],
          "license_path": "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
        },
        {
          "library_name": "launch-1d2ffee7eef5-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:13.988Z",
      "status": "succeeded",
      "token": "1d2ffee7eef5"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/library"
        },
        "data": {
          "id": "LB52ccd7f1e99146999f90cb3bca4940a2",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/host",
          "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/relationships/host"
        },
        "data": {
          "id": "HT53a4ebcb177d431e8fd26929930de0af",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/property"
        },
        "data": {
          "id": "PR79de7e0885a9451786f1bf4b9136a72c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR79de7e0885a9451786f1bf4b9136a72c",
      "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### Söka efter den relaterade egenskapen för ett bibliotek {#property}

Du kan söka efter den egenskap som äger ett bibliotek genom att lägga till `/property` till sökvägen för en GET-begäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/property
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` för det bibliotek vars egenskap du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om egenskapen som äger det angivna biblioteket.

```json
{
  "data": {
    "id": "PRb18ac8f8b69d4f99af43870e91c17543",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:56.180Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:56.180Z",
      "platform": "web",
      "development": false,
      "token": "9d97006b0f9b",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments",
      "extensions": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions",
      "rules": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules",
      "self": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

### Söka efter ett bibliotek i det överordnade flödet {#upstream}

Du kan söka upp nästa bibliotek uppåt från ett bibliotek genom att lägga till `/upstream_library` till sökvägen för en GET-begäran.

**API-format**

```http
GET  /libraries/{LIBRARY_ID}/upstream_library
```

| Parameter | Beskrivning |
| --- | --- |
| `{LIBRARY_ID}` | The `id` för det bibliotek vars överordnade bibliotek du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/upstream_library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om det överordnade biblioteket.

```json
{
  "data": {
    "id": "LB29cc2f86b3684e00a10d196a60f4b0c0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:49:32.459Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:49:41.070Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/rules",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/property"
        },
        "data": {
          "id": "PR7c206ed399644222aef329488cee7fa7",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/last_build"
        },
        "data": {
          "id": "BL87cde018ecd44ac7a20b0271ab06d04b",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7c206ed399644222aef329488cee7fa7",
      "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```
