---
title: Regelslutpunkt
description: Lär dig hur du anropar /rules-slutpunkten i Reactor API.
exl-id: 79ef4389-e4b7-461e-8579-16a1a78cdd43
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# Regelslutpunkt

När det gäller datainsamlingstaggar styr reglerna beteendet för resurserna i ett distribuerat bibliotek. En regel består av en eller flera [regelkomponenter](./rule-components.md) som finns för att knyta ihop regelkomponenterna på ett logiskt sätt. Med slutpunkten `/rules` i Reaktors API kan du hantera taggregler programmatiskt.

>[!NOTE]
>
>I det här dokumentet beskrivs hur du hanterar regler i Reactor API. Mer information om hur du interagerar med regler i användargränssnittet finns i [användargränssnittshandboken](../../ui/managing-resources/rules.md).

En regel tillhör exakt en [egenskap](./properties.md). En egenskap kan ha många regler.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta en lista med regler {#list}

Du kan hämta en lista över regler som tillhör en egenskap genom att göra en GET-begäran.

**API-format**

```http
GET /properties/{PROPERTY_ID}/rules
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | `id` för egenskapen vars komponenter du vill visa. |

{style="table-layout:auto"}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade regler filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Mer information finns i guiden om [filtrering av svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med regler för den angivna egenskapen.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
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

## Söka efter en regel {#lookup}

Du kan söka efter en regel genom att ange dess ID i sökvägen för en GET-begäran.

>[!NOTE]
>
>När regler tas bort markeras de som borttagna men tas inte bort från systemet. Det är därför möjligt att hämta en borttagen regel. Borttagna regler kan identifieras med en `meta.deleted_at`-egenskap.

**API-format**

```http
GET /rules/{RULE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_ID` | `id` för regeln som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar information om regeln.

```json
{
  "data": {
    "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:33.188Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:33.188Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/property"
        },
        "data": {
          "id": "PRfa164e39b0d74eb5b093ab963b1f1200",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/origin"
        },
        "data": {
          "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRfa164e39b0d74eb5b093ab963b1f1200",
      "origin": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "self": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "rule_components": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Skapa en regel {#create}

Du kan skapa en ny regel genom att göra en POST-förfrågan.

**API-format**

```http
POST /properties/{PROPERTY_ID}/rules
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | `id` för egenskapen som du definierar en regel under. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Rule",
            "enabled": true,
          },
          "type": "rules"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.name` | **(Obligatoriskt)** Ett läsbart namn för regeln. |
| `attributes.enabled` | Ett booleskt värde som anger om regeln är aktiverad. |
| `type` | Den typ av resurs som skapas. För den här slutpunkten måste värdet vara `rules`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade regeln.

```json
{
  "data": {
    "id": "RL52d156a9074844b89ca20c987dbafd3b",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:31:46.883Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:31:46.883Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin"
        },
        "data": {
          "id": "RL52d156a9074844b89ca20c987dbafd3b",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "origin": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "self": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "rule_components": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Lägga till händelser, villkor och åtgärder i en regel {#components}

När du har [skapat en regel](#create) kan du börja bygga ut dess logik genom att lägga till händelser, villkor och åtgärder (kallas gemensamt för regelkomponenter). Läs avsnittet [Skapa en regelkomponent](./rule-components.md#create) i `/rule_components`-slutpunktshandboken om du vill veta hur du gör det i Reaktors-API:t.

## Uppdatera en regel {#update}

Du kan uppdatera attributen för en regel genom att ta med dess ID i sökvägen för en PATCH-begäran.

**API-format**

```http
PATCH /rules/{RULE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_ID` | `id` för regeln som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Följande begäran uppdaterar `name` för en befintlig regel.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
  "data": {
    "attributes": {
      "name": "Test Rule"
    },
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules"
  }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | Ett objekt vars regler representerar attributen som ska uppdateras för regeln. Följande attribut kan uppdateras för en regel: <ul><li>`name`</li><li>`enabled`</li></ul> |
| `id` | `id` för regeln som du vill uppdatera. Det här bör matcha det `{RULE_ID}`-värde som anges i sökvägen till begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `rules`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om den uppdaterade regeln.

```json
{
  "data": {
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:55.026Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Test Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:55.717Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/property"
        },
        "data": {
          "id": "PR7e37a33354cc4aa7880f2a550c4f844f",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/origin"
        },
        "data": {
          "id": "RLd2528a53c21a468f93cfd85244f16fdd",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7e37a33354cc4aa7880f2a550c4f844f",
      "origin": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "self": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "rule_components": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Ta bort en regel

Du kan ta bort en regel genom att ta med dess ID i sökvägen för en DELETE-begäran.

**API-format**

```http
DELETE /rules/{RULE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_ID` | `id` för regeln som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext, vilket anger att regeln har tagits bort.

## Hantera anteckningar för en regel {#notes}

Regler är&quot;anmärkningsvärda&quot; resurser, vilket innebär att du kan skapa och hämta textbaserade anteckningar för varje enskild resurs. Mer information om hur du hanterar anteckningar för regler och andra kompatibla resurser finns i [anteckningsguiden](./notes.md).

## Hämta relaterade resurser för en regel {#related}

Följande anrop visar hur du hämtar relaterade resurser för en regel. När [söker efter en regel &#x200B;](#lookup) visas de här relationerna under regeln `relationships`.

Se [relationshandboken](../guides/relationships.md) för mer information om relationer i Reactor API.

### Lista relaterade bibliotek för en regel {#libraries}

Du kan lista bibliotek som använder en viss regel genom att lägga till `/libraries` i sökvägen för en sökningsbegäran.

**API-format**

```http
GET  /rules/{RULE_ID}/libraries
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_ID}` | `id` för regeln vars bibliotek du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med bibliotek som använder den angivna regeln.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
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

### Lista relaterade revisioner för en regel {#revisions}

Du kan lista revideringarna för en regel genom att lägga till `/revisions` i sökvägen för en uppslagsbegäran.

**API-format**

```http
GET  /rules/{RULE_ID}/revisions
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_ID}` | `id` för regeln vars revisioner du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med revisioner som använder den angivna regeln.

```json
{
  "data": [
    {
      "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:29.835Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:57:29.835Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "rule_components": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:30.528Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:57:30.528Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
        "rule_components": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
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
      "total_count": 2
    }
  }
}
```

### Söka efter relaterat ursprung för en regel {#origin}

Du kan slå upp regelns ursprung (tidigare version) genom att lägga till `/origin` i sökvägen för en sökningsbegäran.

**API-format**

```http
GET /rules/{RULE_ID}/origin
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_ID}` | `id` för regeln vars ursprung du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar information om den angivna regelns tillägg.

```json
{
  "data": {
    "id": "RLb83ed2278dc045628c069ab7eb9bb866",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:57:41.517Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:57:41.517Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/property"
        },
        "data": {
          "id": "PR169d832d20ea4243b5a5db0ccc5aae9c",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin"
        },
        "data": {
          "id": "RLb83ed2278dc045628c069ab7eb9bb866",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR169d832d20ea4243b5a5db0ccc5aae9c",
      "origin": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "self": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "rule_components": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Söka efter den relaterade egenskapen för en regel {#property}

Du kan söka efter egenskapen som äger en regel genom att lägga till `/property` i sökvägen för en sökbegäran.

**API-format**

```http
GET /rules/{RULE_ID}/property
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_ID}` | `id` för regeln vars egenskap du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RC3d0805fde85d42db8988090bc074bb44/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om den angivna regelns egenskap.

```json
{
  "data": {
    "id": "PR8ac25b57d5c24ebab68ffe5c630fc690",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:19.088Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:19.088Z",
      "platform": "web",
      "development": false,
      "token": "97b2cb1177df",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments",
      "extensions": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions",
      "rules": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules",
      "self": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690"
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
