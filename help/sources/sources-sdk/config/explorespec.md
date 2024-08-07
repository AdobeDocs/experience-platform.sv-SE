---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera specifikationer för självbetjäningskällor (Batch SDK)
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Konfigurera specifikationer för självbetjäningskällor (Batch SDK)

Utforska specifikationerna och definiera de parametrar som krävs för att utforska och inspektera objekt som finns i källan. Utforska specifikationerna definierar också det svarsformat som returneras när objekt utforskas och inspekteras.

>[!TIP]
>
>Utforska specifikationerna är hårdkodade och du kan helt enkelt kopiera och klistra in nyttolasten nedan i din anslutningsspecifikation.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Utforska specifikationer | Beskrivning | Exempel |
| --- | --- | --- |
| `name` | Definierar namnet eller identifieraren för specifikationen. | `Resource` |
| `type` | Definierar typen av experimentspecifikation. | `Resource` |
| `requestSpec` | Innehåller de parametrar som krävs för att utforska objekt i anslutningen. |
| `requestSpec.type` | Definierar datatypen för förfrågningsspecifikationen. | `object` |
| `responseSpec` | Innehåller parametrar som definierar formatet för svarsmeddelandet som returneras mot ett utforska anrop. |
| `responseSpec.type` | Definierar datatypen för svarsspecifikationen. | `object` |
| `responseSpec.properties` | Innehåller information om hur svarsmeddelandet formateras. |
| `responseSpec.properties.format` | Definierar svarsschemats formatering. | `object` |
| `responseSpec.properties.format.type` | Definierar egenskapernas datatyp. | `string` |
| `responseSpec.schema` | Innehåller information om hur svarsschemat formateras. |
| `responseSpec.schema.type` | Definierar schemats datatyp. | `object` |
| `responseSpec.schema.properties` | Innehåller information om kolumner, typ och objekt som finns i ett schema. |
| `responseSpec.schema.properties.columns.items.properties.name` | Visar filens namn. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Definierar datatypen för filnamnet. | `string` |

{style="table-layout:auto"}

## Nästa steg

När du har fyllt i utforska specifikationerna kan du fortsätta att skapa en fullständig anslutningsspecifikation med API:t [!DNL Flow Service]. Mer information finns i API-handboken för [Självbetjäningskällor (Batch SDK)](../api/api-overview.md).
