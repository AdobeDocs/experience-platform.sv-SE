---
title: Söka efter resurser i reaktors-API
description: Lär dig hur du söker efter resurser i Reactor API.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Söka efter resurser i Reactor API

Med slutpunkten `/search` i Reaktors-API kan du skapa strukturerade frågor för lagrade resurser. Det här dokumentet innehåller exempel på olika sökfrågor för olika vanliga användningsområden.

>[!NOTE]
>
>Innan du läser den här guiden bör du läsa [sökslutpunktshandboken](../endpoints/search.md) för information om godkänd frågesyntax och andra riktlinjer för användning.

## Grundläggande frågestrategier

I följande exempel visas några grundläggande begrepp för hur du använder API:ts sökfunktion.

### Sök i flera fält

Du kan söka i flera fält med jokertecken i fältnamnet. Om du till exempel vill söka i flera attributfält använder du `attributes.*` som fältnamn.

```json
{
  "data" : {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>Vanligtvis måste sökvärdena matcha den typ av data som söks igenom. Ett frågevärde på `evar7` mot ett heltalsfält skulle till exempel misslyckas. När du söker i flera fält blir frågetypskravet mindre krävande för att undvika fel, men kan ge oönskade resultat.

### Omfattningsfrågor till specifika resurstyper

Du kan göra en sökning till en viss resurstyp genom att ange `resource_types` i begäran. Om du till exempel vill söka i `data_elements` och `rule_components`:

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### Sortera svar

Egenskapen `sort` kan användas för att sortera svar. Om du till exempel vill sortera efter `created_at` med det senaste först:

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## Exempel på vanliga sökningar

I följande exempel visas ytterligare vanliga sökmönster.

### Alla resurser med ett specifikt namn

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### Alla resurser som refererar till &quot;evar7&quot;

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### Dataelement av en delegattyp av typen&quot;anpassad kod&quot;

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### Regelkomponenter som refererar till ett specifikt dataelement

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### Regler i en specifik egenskap

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### Hitta en resurs efter ID

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### Gör en sökning med termisk&quot;OR&quot;

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
