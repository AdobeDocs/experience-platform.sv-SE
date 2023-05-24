---
title: Slutpunkt för regelkomponenter
description: Lär dig hur du anropar /rule_components-slutpunkten i Reactor API.
exl-id: 8a878a89-7f41-45fc-88f3-17f0f743e29c
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 1%

---

# Slutpunkt för regelkomponenter

I datainsamlingstaggar [regler](./rules.md) styra beteendet för resurserna i en distribuerad [bibliotek](./libraries.md). **Regelkomponenter** är de enskilda delar som utgör en regel. Om en regel är ett recept är en regelkomponent en av ingredienserna. The `/rule_components` -slutpunkten i Reaktors API gör att du kan hantera regelkomponenter programmatiskt.

>[!NOTE]
>
>Det här dokumentet beskriver hur du hanterar regelkomponenter i Reaktors-API:t. Mer information om hur du interagerar med regler och regelkomponenter i användargränssnittet finns i [Användargränssnittsguide](../../ui/managing-resources/rules.md).

Regelkomponenter har tre grundläggande typer:

| Regelkomponenttyp | Beskrivning |
| --- | --- |
| Händelser | En händelse är utlösaren för en regel. Regeln startar när händelsen inträffar vid körning på klientenheten. &quot;[!UICONTROL Library Load]&quot;, &quot;[!UICONTROL Page Top]&quot;, och &quot;[!UICONTROL Click]&quot; är exempel på händelser. |
| Villkor | Ett villkor är en utvärdering av om vissa kriterier uppfylls innan några åtgärder utförs. När en händelse inträffar utvärderas villkoren. Regelns åtgärder körs bara om alla villkor uppfylls. |
| Instruktioner | Detta är de åtgärder som du vill att regeln faktiskt ska utföra, som att skicka en Adobe Analytics-fyr, hämta ett anpassat besökar-ID eller bränna en viss ruta. |

{style="table-layout:auto"}

En regelkomponent tillhör exakt en regel. En regel kan (och bör) ha många regelkomponenter.

En regelkomponent tillhandahålls av exakt en [extension](./extensions.md). Tillägg kan innehålla många regelkomponenttyper.

## Komma igång

Slutpunkten som används i den här guiden är en del av [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Läs igenom [komma igång-guide](../getting-started.md) om du vill ha viktig information om hur du autentiserar till API:t.

## Hämta en lista med regelkomponenter {#list}

Du kan hämta en lista med regelkomponenter som tillhör en regel genom att ta med regelns ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /rules/{RULE_ID}/rule_components
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_ID` | The `id` för den regel vars komponenter du vill visa. |

{style="table-layout:auto"}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade regelkomponenter filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`negate`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Se guiden [filtrera svar](../guides/filtering.md) för mer information.

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f51/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med regelkomponenter för den angivna regeln.

```json
{
  "data": [
    {
      "id": "RC45944086902c4828b6e14ffbb40017f4",
      "type": "rule_components",
      "attributes": {
        "created_at": "2020-12-14T17:54:34.976Z",
        "delegate_descriptor_id": "kessel-test::events::click",
        "deleted_at": null,
        "dirty": true,
        "name": "My Example Click Event",
        "negate": false,
        "order": 0,
        "rule_order": 50.0,
        "timeout": 2000,
        "delay_next": true,
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:54:34.976Z",
        "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
      },
      "relationships": {
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension"
          },
          "data": {
            "id": "EX6312cea676de47ad9f70b42f7c0fbf02",
            "type": "extensions"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/extension"
          },
          "data": {
            "id": "EXbfd099788024423ebdd49cf06b52e50a",
            "type": "extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/notes"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/origin"
          },
          "data": {
            "id": "RC45944086902c4828b6e14ffbb40017f4",
            "type": "rule_components"
          }
        },
        "rule component": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PRb1090b7443e948ac91650964b490e622"
          },
          "data": {
            "id": "PRb1090b7443e948ac91650964b490e622",
            "type": "properties"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules"
          }
        }
      },
      "links": {
        "extension": "https://reactor.adobe.io/extensions/EXbfd099788024423ebdd49cf06b52e50a",
        "origin": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4",
        "rules": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules",
        "self": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4"
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

## Söka efter en regelkomponent {#lookup}

Du kan söka efter en regelkomponent genom att ange dess ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_COMPONENT_ID` | The `id` för regelkomponenten som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar detaljerna om regelkomponenten.

```json
{
  "data": {
    "id": "RC7be169fcfd534ffc82acc7bffdc50128",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:18.551Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:18.551Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension"
        },
        "data": {
          "id": "EXa11e168f2ff2485197a493095269f964",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/extension"
        },
        "data": {
          "id": "EXa76eb16dd86849318b743494e75c33a1",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/origin"
        },
        "data": {
          "id": "RC7be169fcfd534ffc82acc7bffdc50128",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR00a35a74381443dc994e6b30b7152106"
        },
        "data": {
          "id": "PR00a35a74381443dc994e6b30b7152106",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXa76eb16dd86849318b743494e75c33a1",
      "origin": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128",
      "rules": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules",
      "self": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Skapa en regelkomponent {#create}

Du kan skapa en ny regelkomponent genom att göra en POST.

**API-format**

```http
POST /properties/{PROPERTY_ID}/rule_components
```

| Parameter | Beskrivning |
| --- | --- |
| `PROPERTY_ID` | The `id` för egenskapen som du definierar regelkomponenten under. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skapar en ny regelkomponent. I nyttolasten `relationships` -egenskapen associerar komponenten med specifika regler och ett befintligt tillägg. Se guiden [relationer](../guides/relationships.md) för mer information.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "delay_next": true,
            "order": 0,
            "rule_order": 50.0,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}",
            "timeout": 2000
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX31b8c49f134b4307924d71a64204099e",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLf7b4f416b2e04ae1ba857ae681fee5bc",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.delegate_descriptor_id` | **(Obligatoriskt)** De typer av regelkomponenter som du kan definiera tillhandahålls av [tilläggspaket](./extension-packages.md). När du skapar en ny regelkomponent måste du ange ett delegatbeskrivnings-ID som anger vilket tilläggspaket som regelkomponenten baseras på, komponentens typ (händelse, villkor eller åtgärd) och namnet på den specifika komponenten som definieras av tillägget (till exempel händelsen&quot;Click&quot; i tillägget Core).<br><br>Se guiden [delegatbeskrivnings-ID](../guides/delegate-descriptor-ids.md) för mer information. |
| `attributes.name` | **(Obligatoriskt)** Ett namn som kan läsas av människor för regelkomponenten. |
| `attributes.delay_next` | Ett booleskt värde som anger om senare åtgärder ska fördröjas. |
| `attributes.order` | Ett heltal som anger i vilken ordning komponenten ska läsas in efter typ. |
| `attributes.rule_order` | Ett heltal som anger prioriteten för den associerade regeln som ska utlösas. |
| `attributes.settings` | Ett inställnings-JSON-objekt representeras som en sträng. |
| `attributes.timeout` | Ett heltal som anger timeout för åtgärden som körs i sekvens. |
| `relationships` | Ett objekt som upprättar nödvändiga relationer för regelkomponenten. Två relationer måste upprättas: <ol><li>`extension`: Det tillägg som definierar den här regelkomponenten. Detta måste vara samma tillägg vars tilläggspaket anges av `delegate_descriptor_id`.</li><li>`rules`: Regeln som den här komponenten definieras under.</li></ol>Mer allmän information om relationer finns i [relationshandbok](../guides/relationships.md). |
| `type` | Den typ av resurs som skapas. För den här slutpunkten måste värdet vara `rule_components`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om den regelkomponent som nyligen har skapats.

```json
{
  "data": {
    "id": "RC78c44af3cf7644e5927fc0ad61e88940",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:00.232Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:00.232Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension"
        },
        "data": {
          "id": "EX0019a115a74f401fa0b9bb8f57a0196b",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/extension"
        },
        "data": {
          "id": "EX31b8c49f134b4307924d71a64204099e",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/origin"
        },
        "data": {
          "id": "RC78c44af3cf7644e5927fc0ad61e88940",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1"
        },
        "data": {
          "id": "PR97596432a82549ceb8e2a5d9df05c0e1",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EX31b8c49f134b4307924d71a64204099e",
      "origin": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940",
      "rules": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules",
      "self": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Uppdatera en regelkomponent {#update}

Du kan uppdatera en regelkomponent genom att ta med dess ID i sökvägen för en PATCH-begäran.

>[!NOTE]
>
>Uppdatering av en regelkomponent uppdaterar även den överordnade regelns `updated_at` tidsstämpel.

**API-format**

```http
PATCH /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_COMPONENT_ID` | The `id` för regelkomponenten som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Följande begäran uppdaterar `order` och `settings` attribut för en befintlig regelkomponent.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "order": 1,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
          },
          "type": "rule_components",
          "id": "RC9af052ee231346f28d1e44865ab62c04"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | Ett objekt vars regelkomponenter representerar attributen som ska uppdateras för regelkomponenten. Följande attribut kan uppdateras för en regelkomponent: <ul><li>`delay_next`</li><li>`delegate_descriptor_id`</li><li>`name`</li><li>`order`</li><li>`rule_order`</li><li>`settings`</li><li>`timeout`</li></ul> |
| `id` | The `id` för regelkomponenten som du vill uppdatera. Det här bör matcha `{RULE_COMPONENT_ID}` värdet som anges i sökvägen för begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `rule_components`. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar information om den uppdaterade regelkomponenten.

```json
{
  "data": {
    "id": "RC9af052ee231346f28d1e44865ab62c04",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:50.887Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 1,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:52.553Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension"
        },
        "data": {
          "id": "EX468796dd09d743858f17d4c5ca52f3e0",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension"
        },
        "data": {
          "id": "EXcedb08a8265c488e8bb98b46245b2486",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/origin"
        },
        "data": {
          "id": "RC9af052ee231346f28d1e44865ab62c04",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR986402dc07834fbeb4789c56060dbf41"
        },
        "data": {
          "id": "PR986402dc07834fbeb4789c56060dbf41",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXcedb08a8265c488e8bb98b46245b2486",
      "origin": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04",
      "rules": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules",
      "self": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## Ta bort en regelkomponent

Du kan ta bort en regelkomponent genom att ta med dess ID i sökvägen för en DELETE-begäran.

**API-format**

```http
DELETE /rule_components/{RULE_COMPONENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `RULE_COMPONENT_ID` | The `id` för regelkomponenten som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext, vilket anger att regelkomponenten har tagits bort.

## Hantera anteckningar för en regelkomponent {#notes}

Regelkomponenter är&quot;anmärkningsvärda&quot; resurser, vilket innebär att du kan skapa och hämta textbaserade anteckningar för varje enskild resurs. Se [slutpunktshandbok för anteckningar](./notes.md) om du vill ha mer information om hur du hanterar anteckningar för regelkomponenter och andra kompatibla resurser.

## Hämta relaterade resurser för en regelkomponent {#related}

Följande anrop visar hur du hämtar relaterade resurser för en regelkomponent. När [söka efter en regelkomponent](#lookup), listas dessa relationer under `relationships` regelkomponent.

Se [relationshandbok](../guides/relationships.md) för mer information om relationerna i Reactor API.

### Visa relaterade regler för en regelkomponent {#rules}

Du kan lista reglerna som använder en viss regelkomponent genom att lägga till `/rules` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET  /rule_components/{RULE_COMPONENT_ID}/rules
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_COMPONENT_ID}` | The `id` för regelkomponenten vars regler du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med regler som använder den angivna regelkomponenten.

```json
{
  "data": [
    {
      "id": "RLf1baa571748941db88f54de8efd119aa",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:58:36.072Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:58:37.452Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/property"
          },
          "data": {
            "id": "PR966c4a501e1a43a48cb55e104b4de935",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/origin"
          },
          "data": {
            "id": "RLf1baa571748941db88f54de8efd119aa",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR966c4a501e1a43a48cb55e104b4de935",
        "origin": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "self": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "rule_components": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ]
}
```

### Söka efter det relaterade tillägget för en regelkomponent {#extension}

Du kan leta upp tillägget som innehåller en regelkomponent genom att lägga till `/extension` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET /rule_components/{RULE_COMPONENT_ID}/extension
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_COMPONENT_ID}` | The `id` för regelkomponenten vars tillägg du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar information om den angivna regelkomponentens tillägg.

```json
{
  "data": {
    "id": "EX5644c3eed97d46b39cb2279ea11dde29",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:55:22.634Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:22.634Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/property"
        },
        "data": {
          "id": "PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/origin"
        },
        "data": {
          "id": "EX5644c3eed97d46b39cb2279ea11dde29",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
      "origin": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "self": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### Söka efter relaterat ursprung för en regelkomponent {#origin}

Du kan slå upp origo (föregående revision) för en regelkomponent genom att lägga till `/origin` till sökvägen för en sökningsbegäran.

**API-format**

```http
GET /rule_components/{RULE_COMPONENT_ID}/origin
```

| Parameter | Beskrivning |
| --- | --- |
| `{RULE_COMPONENT_ID}` | The `id` för regelkomponenten vars ursprung du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar information om den angivna regelkomponentens ursprung.

```json
{
  "data": {
    "id": "RC3d0805fde85d42db8988090bc074bb44",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:55:40.016Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": false,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:40.016Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension"
        },
        "data": {
          "id": "EXb713fc209ce344c996bdeb377685e2c4",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/extension"
        },
        "data": {
          "id": "EXd6e1dce006b2412f874301e24d58ce24",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin"
        },
        "data": {
          "id": "RC3d0805fde85d42db8988090bc074bb44",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR89c66a560ec44928889b439333255efe"
        },
        "data": {
          "id": "PR89c66a560ec44928889b439333255efe",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXd6e1dce006b2412f874301e24d58ce24",
      "origin": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44",
      "rules": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules",
      "self": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```
