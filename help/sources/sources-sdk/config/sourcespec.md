---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera autentiseringsspecifikationer för Sources SDK
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda Sources SDK.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `sourceSpec.attributes` | Innehåller information om källan som är specifik för gränssnittet eller API:t. |
| `sourceSpec.attributes.uiAttributes` | Visar information om källan som är specifik för användargränssnittet. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ett booleskt attribut som anger om källan kräver mer feedback från kunderna för att lägga till dess funktioner. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definierar källans kategori. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definierar ikonen som används för återgivning av källan i plattformsgränssnittet. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Visar en kort beskrivning av källan. |
| `sourceSpec.attributes.uiAttributes.label` | Visar den etikett som ska användas för återgivning av källan i plattformsgränssnittet. |
| `sourceSpec.attributes.urlParams` | Innehåller information om URL-resursens sökväg, metod och vilka frågeparametrar som stöds. |
| `sourceSpec.attributes.urlParams.path` | Definierar resurssökvägen varifrån data ska hämtas. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Definierar den HTTP-metod som ska användas för att begära att resursen hämtar data. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Definierar de frågeparametrar som stöds och som kan användas för att lägga till käll-URL:en när data hämtas. Frågeparametrar måste vara kommatecken (`,`) avgränsade nyckelvärdepar. **Anteckning**: Alla användartillhandahållna parametervärden måste formateras som platshållare. Exempel: `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Definierar kommat (`,`) avgränsade rubriker som måste anges i HTTP-begäran till käll-URL när data hämtas. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Definierar de obligatoriska innehållsparametrarna. Den här egenskapen används bara om `urlParams.method` är inställd på `POST`. |
| `sourceSpec.attributes.contentPath` | Definierar noden som innehåller listan med objekt som krävs för att kopplas till plattformen. Attributet ska följa giltig JSON-sökvägssyntax och peka på en viss array. | Se [appendix](#content-path) för ett exempel på resursen som finns i en innehållssökväg. |
| `sourceSpec.attributes.contentPath.path` | Sökvägen som pekar på samlingsposterna som ska importeras till Platform. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Med den här egenskapen kan du identifiera specifika objekt från den resurs som identifieras i innehållssökvägen som ska uteslutas från kapsling. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Med den här egenskapen kan du åsidosätta värdet för attributnamnet som du angav i `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Med den här egenskapen kan du uttryckligen ange de enskilda attribut som du vill mappa. |
| `sourceSpec.attributes.explodeEntityPath` | Med den här egenskapen kan du förenkla två arrayer och omvandla resursdata till en plattformsresurs. |
| `sourceSpec.attributes.explodeEntityPath.path` | Sökvägen som pekar på samlingsposterna som du vill förenkla. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Med den här egenskapen kan du identifiera specifika objekt från den resurs som identifieras i entitetssökvägen som ska uteslutas från inkapsling. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Med den här egenskapen kan du åsidosätta värdet för attributnamnet som du angav i `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Med den här egenskapen kan du uttryckligen ange de enskilda attribut som du vill mappa. |
| `sourceSpec.attributes.paginationParams` | Definierar de parametrar eller fält som måste anges för att få en länk till nästa sida från användarens aktuella sidsvar, eller när en URL för nästa sida skapas. |
| `sourceSpec.attributes.paginationParams.type` | Visar vilken typ av sidnumrering som stöds för källan. | <ul><li>`offset`: Med den här sidnumreringstypen kan du tolka resultaten genom att ange ett index från vilken den resulterande arrayen ska startas och en gräns för hur många resultat som returneras.</li><li>`pointer`: Med den här sidnumreringstypen kan du använda en `pointer` variabel för att peka på ett visst objekt som behöver skickas med en begäran. Sidnumreringen av pekartypen kräver en sökväg i nyttolasten som pekar på nästa sida</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | Namnet på gränsen genom vilken API:t kan ange antalet poster som ska hämtas på en sida. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | Antalet poster som ska hämtas på en sida. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | Förskjutningsattributets namn. Detta krävs om sidnumreringstypen är inställd på `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | Pekarens attributnamn. Detta kräver JSON-sökväg till attributet som pekar på nästa sida. Detta krävs om sidnumreringstypen är inställd på `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Innehåller parametrar som definierar schemaläggningsformat som stöds för källan. Schemaparametrarna innehåller `startTime` och `endTime`, som båda gör att du kan ange specifika tidsintervall för batchkörningar, vilket sedan säkerställer att poster som hämtats i en tidigare batchkörning inte hämtas igen. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Definierar namnet på starttidsparametern | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Definierar sluttidsparameterns namn | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Definierar det format som stöds för `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Definierar det format som stöds för `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
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