---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera autentiseringsspecifikationer för Sources SDK
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda Sources SDK.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4c4c89ab7db7d3546163d707ac80210561c2fa02
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Konfigurera källspecifikation för Sources SDK

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
| `sourceSpec.attributes.spec.properties.contentPath` | Definierar noden som innehåller listan med objekt som krävs för att kopplas till plattformen. Attributet ska följa giltig JSON-sökvägssyntax och peka på en viss array. | Se [appendix](#content-path) för ett exempel på resursen som finns i en innehållssökväg. |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Visar vilken typ av sidnumrering som stöds för källan. | <ul><li>`offset`: Med den här sidnumreringstypen kan du tolka resultaten genom att ange ett index från vilken den resulterande arrayen ska startas och en gräns för hur många resultat som returneras.</li><li>`pointer`: Med den här sidnumreringstypen kan du använda en `pointer` variabel för att peka på ett visst objekt som behöver skickas med en begäran. Sidnumreringen av pekartypen kräver en sökväg i nyttolasten som pekar på nästa sida</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Namnet på gränsen genom vilken API:t kan ange antalet poster som ska hämtas på en sida. | `limit` eller `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Antalet poster som ska hämtas på en sida. | `limit=10` eller `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Förskjutningsattributets namn. Detta krävs om sidnumreringstypen är inställd på `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Pekarens attributnamn. Detta kräver JSON-sökväg till attributet som pekar på nästa sida. Detta krävs om sidnumreringstypen är inställd på `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Innehåller parametrar som definierar schemaläggningsformat som stöds för källan. Schemaparametrarna innehåller `startTime` och `endTime`, som båda gör att du kan ange specifika tidsintervall för batchkörningar, vilket sedan säkerställer att poster som hämtats i en tidigare batchkörning inte hämtas igen. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definierar namnet på starttidsparametern | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definierar sluttidsparameterns namn | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definierar det format som stöds för `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definierar det format som stöds för `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definierar de parametrar som användaren anger för att hämta resursvärden. | Se [appendix](#user-input) för ett exempel på användarangivna parametrar för `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Bilaga {#appendix}

### Exempel på innehållssökväg {#content-path}

Här följer ett exempel på innehållet i `contentPath` egenskap i en [!DNL MailChimp Campaigns] anslutningsspecifikation.

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

## Nästa steg

När källspecifikationerna är ifyllda kan du fortsätta att konfigurera utforska specifikationerna för den källa som du vill integrera med plattformen. Se dokumentet på [konfigurera specifikationer för utforska](./explorespec.md) för mer information.
