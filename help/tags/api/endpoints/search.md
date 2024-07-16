---
title: Sökslutpunkt
description: Lär dig hur du anropar slutpunkten /search i Reactor API.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Sökslutpunkt

Slutpunkten `/search` i Reaktors API erbjuder ett sätt att hitta resurser som matchar önskade villkor, uttryckta som en fråga.

Följande API-resurstyper är sökbara och använder samma datastruktur som de resursbaserade dokument som returneras via API:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Alla frågor omfattar det aktuella företaget och tillgängliga egenskaper.

>[!IMPORTANT]
>
>Sökfunktionen har följande kavattningar och undantag:
>* Meta är inte sökbart och returneras inte i sökresultaten.
>* Schemafält för delegater för tilläggspaket (åtgärder, villkor osv.) är sökbara som text, inte som en kapslad datastruktur.
>* Intervallfrågor stöder för närvarande bara heltal.

Mer ingående information om hur du använder den här funktionen finns i [sökguiden](../guides/search.md).

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Utför en sökning {#perform}

Du kan göra en sökning genom att göra en POST.

**API-format**

```http
POST /search
```

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `from` | Antalet resultat att förskjuta svaret med. |
| `size` | Den maximala mängden resultat som ska returneras. Resultaten får inte överskrida 100 objekt. |
| `query` | Ett objekt som representerar sökfrågan. För varje egenskap i det här objektet måste nyckeln representera en fältsökväg att fråga efter och värdet måste vara ett objekt vars underegenskaper bestämmer vad som ska sökas efter.<br><br>För varje fältsökväg kan du använda följande underegenskaper:<ul><li>`exists`: Returnerar true om fältet finns i resursen.</li><li>`value`: Returnerar true om fältets värde matchar värdet för den här egenskapen.</li><li>`value_operator`: Boolesk logik som används för att avgöra hur en `value`-fråga ska hanteras. Tillåtna värden är `AND` och `OR`. När det utelämnas antas `AND`-logik. Mer information finns i avsnittet [värdeoperatorlogik](#value-operator).</li><li>`range` Returnerar true om fältets värde ligger inom ett visst numeriskt intervall. Omfånget bestäms av följande underegenskaper:<ul><li>`gt`: Större än det angivna värdet, ej inkluderande.</li><li>`gte`: Större än eller lika med det angivna värdet.</li><li>`lt`: Mindre än det angivna värdet, ej inkluderande.</li><li>`lte`: Mindre än eller lika med det angivna värdet.</li></ul></li></ul> |
| `sort` | En array med objekt, som anger i vilken ordning resultaten ska sorteras. Varje objekt måste innehålla en enda egenskap: nyckeln representerar fältsökvägen som ska sorteras efter och värdet representerar sorteringsordningen (`asc` för stigande, `desc` för fallande). |
| `resource_types` | En array med strängar som anger de specifika resurstyper som ska sökas igenom. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar en lista med matchande resurser för frågan. Mer information om hur API:t avgör matchningar för specifika värden finns i avsnittet om tillägg för [matchande konventioner](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du använder slutpunkten `/search`.

### Värdeoperatorlogik {#value-operator}

Sökfrågevärden är uppdelade i termer som matchar mot indexerade dokument. Mellan varje term antas en `AND`-relation.

När `AND` används som `value_operator` tolkas frågevärdet `My Rule Holiday Sale` som dokument med ett fält som innehåller `My AND Rule AND Holiday AND Sale`.

När `OR` används som `value_operator` tolkas frågevärdet `My Rule Holiday Sale` som dokument med ett fält som innehåller `My OR Rule OR Holiday OR Sale`. Ju fler termer som matchar, desto högre blir `match_score`. På grund av typen av partiell termmatchning kan du, när inget nära matchar det önskade värdet, få en resultatmängd där värdet bara matchas på en mycket grundläggande nivå, t.ex. ett par tecken med text.

### Matchande konventioner {#conventions}

Sökningen handlar om att svara på hur relevant ett dokument är för en given fråga. Hur dokumentdata analyseras och indexeras påverkar detta direkt.

I följande tabell visas matchningskonventionerna för vanliga fälttyper:

| Fälttyp | Matcha konventioner |
| --- | --- |
| Strängar | Text med partiell termanalys, skiftlägeskänslig |
| Uppräkningsvärden | Exakt matchning, skiftlägeskänslig |
| Integers | Exakt matchning |
| Floats | Exakt matchning |
| Tidsstämplar | Exakt matchning (DateTime-format) |
| Visningsnamn | Text med partiell termanalys, skiftlägeskänslig |

Det finns ytterligare konventioner för specifika fält som visas i API:

| Fält | Matcha konventioner |
| --- | --- |
| `id` | Exakt matchning, skiftlägeskänslig |
| `delegate_descriptor_id` | Exakt matchning, skiftlägeskänslig, med termer delade på `::` |
| `name` | Exakt matchning, skiftlägeskänslig |
| `settings` | Text med partiell termanalys, skiftlägeskänslig |
| `type` | Exakt matchning, skiftlägeskänslig |
