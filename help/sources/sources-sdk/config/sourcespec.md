---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera källspecifikationer för självbetjäningskällor (batch-SDK)
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# Konfigurera källspecifikation för självbetjäningskällor (batch-SDK)

Källspecifikationerna innehåller information som är specifik för en källa, inklusive attribut som gäller en källas kategori, betastatus och katalogikon. De innehåller även användbar information som URL-parametrar, innehåll, rubrik och schema. Källspecifikationerna beskriver också schemat för de parametrar som krävs för att skapa en källanslutning från en basanslutning. Schemat är nödvändigt för att skapa en källanslutning.

Se [appendix](#source-spec) för ett exempel på en fullt ifylld källspecifikation.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path."
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `sourceSpec.attributes` | Innehåller information om källan som är specifik för gränssnittet eller API:t. |
| `sourceSpec.attributes.uiAttributes` | Visar information om källan som är specifik för användargränssnittet. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ett booleskt attribut som anger om källan kräver mer feedback från kunderna för att lägga till dess funktioner. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definierar källans kategori. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definierar ikonen som används för återgivning av källan i plattformsgränssnittet. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visar en kort beskrivning av källan. |
| `sourceSpec.attributes.uiAttributes.label` | Visar den etikett som ska användas för återgivning av källan i plattformsgränssnittet. |
| `sourceSpec.attributes.spec.properties.urlParams` | Innehåller information om URL-resursens sökväg, metod och vilka frågeparametrar som stöds. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definierar resurssökvägen varifrån data ska hämtas. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definierar den HTTP-metod som ska användas för att begära att resursen hämtar data. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definierar de frågeparametrar som stöds och som kan användas för att lägga till käll-URL:en när data hämtas. **Anteckning**: Alla användartillhandahållna parametervärden måste formateras som platshållare. Exempel: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` läggs till i käll-URL:en som: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definierar rubriker som måste anges i HTTP-begäran till käll-URL:en när data hämtas. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Det här attributet kan konfigureras för att skicka HTTP-brödtext via en POST-begäran. |
| `sourceSpec.attributes.spec.properties.contentPath` | Definierar noden som innehåller listan med objekt som krävs för att kopplas till plattformen. Attributet ska följa giltig JSON-sökvägssyntax och peka på en viss array. | Visa [sektion med ytterligare resurser](#content-path) för ett exempel på resursen som finns i en innehållssökväg. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Sökvägen som pekar på samlingsposterna som ska importeras till Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Med den här egenskapen kan du identifiera specifika objekt från den resurs som identifieras i innehållssökvägen som ska uteslutas från kapsling. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Med den här egenskapen kan du uttryckligen ange de enskilda attribut som du vill behålla. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Med den här egenskapen kan du åsidosätta värdet för attributnamnet som du angav i `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Med den här egenskapen kan du förenkla två arrayer och omvandla resursdata till en plattformsresurs. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Sökvägen som pekar på samlingsposterna som du vill förenkla. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Med den här egenskapen kan du identifiera specifika objekt från den resurs som identifieras i entitetssökvägen som ska uteslutas från inkapsling. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Med den här egenskapen kan du uttryckligen ange de enskilda attribut som du vill behålla. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Med den här egenskapen kan du åsidosätta värdet för attributnamnet som du angav i `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definierar de parametrar eller fält som måste anges för att få en länk till nästa sida från användarens aktuella sidsvar, eller när en URL för nästa sida skapas. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visar vilken typ av sidnumrering som stöds för källan. | <ul><li>`OFFSET`: Med den här sidnumreringstypen kan du tolka resultaten genom att ange ett index från vilken den resulterande arrayen ska startas och en gräns för hur många resultat som returneras.</li><li>`POINTER`: Med den här sidnumreringstypen kan du använda en `pointer` variabel för att peka på ett visst objekt som behöver skickas med en begäran. Sidnumreringen av pekartypen kräver en sökväg i nyttolasten som pekar på nästa sida.</li><li>`CONTINUATION_TOKEN`: Med den här sidnumreringstypen kan du lägga till en token för fråga- eller rubrikparametrar för att hämta återstående returdata från källan, som inte returnerades från början på grund av ett fördefinierat maxvärde.</li><li>`PAGE`: Med den här sidnumreringstypen kan du lägga till frågeparametern med en sidindelningsparameter för att gå igenom returdata för sidor, med början från sidan noll.</li><li>`NONE`: Den här sidnumreringstypen kan användas för källor som inte stöder någon av de tillgängliga sidnumreringstyperna. Sidnumreringstyp `NONE` returnerar hela svarsdata efter en begäran.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Namnet på gränsen genom vilken API:t kan ange antalet poster som ska hämtas på en sida. | `limit` eller `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Antalet poster som ska hämtas på en sida. | `limit=10` eller `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Förskjutningsattributets namn. Detta krävs om sidnumreringstypen är inställd på `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Pekarens attributnamn. Detta kräver JSON-sökväg till attributet som pekar på nästa sida. Detta krävs om sidnumreringstypen är inställd på `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Innehåller parametrar som definierar schemaläggningsformat som stöds för källan. Schemaparametrarna innehåller `startTime` och `endTime`, som båda gör att du kan ange specifika tidsintervall för batchkörningar, vilket sedan säkerställer att poster som hämtats i en tidigare batchkörning inte hämtas igen. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definierar namnet på starttidsparametern | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definierar sluttidsparameterns namn | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definierar det format som stöds för `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definierar det format som stöds för `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definierar de parametrar som användaren anger för att hämta resursvärden. | Se [ytterligare resurser](#user-input) för ett exempel på användarangivna parametrar för `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Ytterligare resurser {#appendix}

I följande avsnitt finns information om ytterligare konfigurationer som du kan göra för dina `sourceSpec`, inklusive avancerad schemaläggning och anpassade scheman.

### Exempel på innehållssökväg {#content-path}

Här följer ett exempel på innehållet i `contentPath` egenskap i en [!DNL MailChimp Members] anslutningsspecifikation.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` användarinmatningsexempel {#user-input}

Följande är ett exempel på en användare `spec.properties` med [!DNL MailChimp Members] anslutningsspecifikation.

I det här exemplet `listId` tillhandahålls som en del av `urlParams.path`. Om du behöver hämta `listId` från en kund måste ni också definiera den som en del av `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Exempel på källspecifikation {#source-spec}

Följande är en färdig källspecifikation som använder [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Konfigurera olika sidnumreringstyper för källan {#pagination}

Nedan följer exempel på andra sidnumreringstyper som stöds av självbetjäningskällor (Batch SDK):

#### `CONTINUATION_TOKEN`

En fortsättningssymbol för numrering returnerar en strängtoken som anger att det finns fler objekt som inte kan returneras på grund av ett fördefinierat maximalt antal objekt som kan returneras i ett enda svar.

En källa som stöder typen fortsättning av token för sidnumrering kan ha en sidnumreringsparameter som liknar:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `type` | Den typ av sidnumrering som används för att returnera data. |
| `continuationTokenPath` | Värdet som måste läggas till i frågeparametrarna för att kunna gå till nästa sida i de returnerade resultaten. |
| `parameterType` | The `parameterType` egenskapen definierar var `parameterName` måste läggas till. The `QUERYPARAM` kan du lägga till din fråga med `parameterName`. The `HEADERPARAM` kan du lägga till `parameterName` till rubrikbegäran. |
| `parameterName` | Namnet på den parameter som används för att inkludera en fortsättningssymbol. Formatet är följande: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | The `delayRequestMillis` sidnumreringsegenskapen gör att du kan styra hur många begäranden som görs till källan. Vissa källor kan ha en gräns för hur många begäranden du kan göra per minut. Till exempel: [!DNL Zendesk] har en gräns på 100 begäranden per minut och definierar  `delayRequestMillis` till `850` Med kan du konfigurera källan så att den kan ringa samtal med ungefär 80 förfrågningar per minut, vilket är mycket mindre än tröskelvärdet på 100 förfrågningar per minut. |

Följande är ett exempel på ett svar som returneras med en fortsättningstokentyp för sidnumrering:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

The `PAGE` sidnumreringstypen gör att du kan gå igenom returdata efter antal sidor med början från noll. När du använder `PAGE` sidnumrering måste du ange hur många poster som ska anges på en sida.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `type` | Den typ av sidnumrering som används för att returnera data. |
| `limitName` | Namnet på gränsen genom vilken API:t kan ange antalet poster som ska hämtas på en sida. |
| `limitValue` | Antalet poster som ska hämtas på en sida. |
| `pageParamName` | Namnet på den parameter som du måste lägga till i frågeparametrar för att kunna gå igenom olika sidor i returdata. Till exempel: `https://abc.com?pageIndex=1` skulle returnera den andra sidan av en API:s returnyttolast. |
| `maximumRequest` | Det maximala antalet begäranden som en källa kan göra för en given inkrementell körning. Den aktuella standardgränsen är 10000. |

#### `NONE`

The `NONE` Sidnumreringstyp kan användas för källor som inte stöder någon av de tillgängliga sidnumreringstyperna. Källor som använder sidnumreringstypen för `NONE` returnera helt enkelt alla poster som går att hämta när en GET begärs.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Avancerad schemaläggning för självbetjäningskällor (batch-SDK)

Konfigurera källans inkrementella schema och schema för efterfyllnad med avancerad schemaläggning. The `incremental` -egenskapen gör att du kan konfigurera ett schema där källan bara får in nya eller ändrade poster, medan `backfill` kan du skapa ett schema för att importera historiska data.

Med avancerad schemaläggning kan du använda uttryck och funktioner som är specifika för källan för att konfigurera inkrementella scheman och bakgrundsfyllningsscheman. I exemplet nedan är [!DNL Zendesk] source kräver att det inkrementella schemat formateras som `type:user updated > {START_TIME} updated < {END_TIME}` och fylla bakåt som `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Egenskap | Beskrivning |
| --- | --- |
| `scheduleParams.type` | Typen av schemaläggning som källan kommer att använda. Ange det här värdet till `ADVANCE` om du vill använda den avancerade schemaläggningstypen. |
| `scheduleParams.paramFormat` | Det definierade formatet för din schemaläggningsparameter. Detta värde kan vara samma som källans `scheduleStartParamFormat` och `scheduleEndParamFormat` värden. |
| `scheduleParams.incremental` | Den inkrementella frågan för källan. Stegvis innebär en metod för intag där endast nya eller ändrade data har importerats. |
| `scheduleParams.backfill` | Källans bakgrundsfyllningsfråga. Backfill avser en ingestionsmetod där historiska data är inmatade. |

När du har konfigurerat din avancerade schemaläggning måste du se `scheduleParams` i avsnittet för URL-, body- eller rubrikparametrar, beroende på vad din källa stöder. I exemplet nedan `{SCHEDULE_QUERY}` är en platshållare som används för att ange var inkrementella schemaläggningsuttryck och schemaläggningsuttryck för bakåtfyllnad ska användas. Om [!DNL Zendesk] källa, `query` används i `queryParams` för att ange avancerad schemaläggning.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Lägg till ett anpassat schema för att definiera källans dynamiska attribut

Du kan inkludera ett anpassat schema i din `sourceSpec` för att definiera alla attribut som krävs för källan, inklusive alla dynamiska attribut som du kan behöva. Du kan uppdatera källans motsvarande anslutningsspecifikation genom att göra en PUT-förfrågan till `/connectionSpecs` slutpunkt för [!DNL Flow Service] API, samtidigt som du tillhandahåller ditt anpassade schema i `sourceSpec` i anslutningsspecifikationen.

Följande är ett exempel på ett anpassat schema som du kan lägga till i källans anslutningsspecifikation:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Nästa steg

När källspecifikationerna är ifyllda kan du fortsätta att konfigurera utforska specifikationerna för den källa som du vill integrera med plattformen. Se dokumentet på [konfigurera specifikationer för utforska](./explorespec.md) för mer information.
