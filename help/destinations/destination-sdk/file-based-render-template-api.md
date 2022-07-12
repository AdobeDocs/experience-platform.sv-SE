---
description: Den här sidan förklarar hur du använder slutpunkten /authoring/testing/template/render för att visualisera hur de mallsidiga kunddatafälten som definieras i målkonfigurationen skulle se ut.
title: Validera mallsidiga kundfält
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# Validera mallsidiga kundfält

## Översikt {#overview}

The `/authoring/testing/template/render` kan du visualisera hur mallarna [kunddatafält](file-based-destination-configuration.md#customer-data-fields) som definierats i målkonfigurationen skulle se ut så här.

Slutpunkten genererar slumpmässiga värden för kunddatafälten och returnerar dem i svaret. Detta hjälper dig att validera den semantiska strukturen i kunddatafält, till exempel bucketnamn eller mappsökvägar.

## Komma igång {#getting-started}

Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Förutsättningar {#prerequisites}

Innan du kan använda `/template/render` måste du se till att följande villkor uppfylls:

* Du har ett befintligt filbaserat mål som skapas via Destinationen SDK och du kan se det i [målkatalog](../ui/destinations-workspace.md).
* För att kunna utföra API-begäran behöver du det målinstans-ID som motsvarar den målinstans som du ska testa. Hämta det målinstans-ID som du bör använda i API-anropet från webbadressen när du bläddrar i en anslutning till målet i plattformsgränssnittet.

   ![Användargränssnittsbild som visar hur du hämtar målinstans-ID från URL:en.](assets/get-destination-instance-id.png)

## Återge mallsidiga kundfält {#render-customer-fields}

**API-format**

```http
POST /authoring/testing/template/render/destination
```

Om du vill visa beteendet för den här API-slutpunkten ska du överväga ett filbaserat mål med följande konfiguration för kunddatafält:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Begäran**

Begäran nedan anropar `/authoring/testing/template/render` slutpunkt, som returnerar ett svar med slumpmässigt genererade värden för de två kunddatafälten som nämns ovan.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parametrar | Beskrivning |
| -------- | ----------- |
| `destinationId` | ID för [målkonfiguration](file-based-destination-configuration.md) som du testar. |
| `templates` | De mallsidiga fältnamnen som definieras i [målserverkonfiguration](server-and-file-configuration.md). |

**Svar**

Ett godkänt svar returnerar ett `HTTP 200 OK` och brödtexten innehåller slumpmässigt genererade värden för de mallsidiga fälten.

Detta svar kan hjälpa er att validera den korrekta strukturen i kunddatafälten, till exempel bucketnamn eller mappsökvägar.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API-felhantering {#api-error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du validerar konfigurationen av kunddatafältet som definieras i [målserver](server-and-file-configuration.md).
