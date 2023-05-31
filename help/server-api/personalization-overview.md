---
title: Personalisering - översikt
description: Lär dig hur du använder API:t för Adobe Experience Platform Edge Network Server för att hämta personaliserat innehåll från personaliseringslösningar från Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 7%

---

# Personalisering - översikt

Med [!DNL Server API]kan ni hämta personaliserat innehåll från personaliseringslösningar i Adobe, inklusive [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) och [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

Dessutom finns [!DNL Server API] möjliggör personalisering på samma sida och nästa sida genom Adobe Experience Platform personaliseringsmål, som [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) och [anslutning för anpassad personalisering](../destinations/catalog/personalization/custom-personalization.md). Mer information om hur du konfigurerar Experience Platform för anpassning av samma sida och nästa sida finns i [dedikerad guide](../destinations/ui/activate-edge-personalization-destinations.md).

När du använder Server-API:t måste du integrera det svar som personaliseringsmotorn ger med den logik som används för att återge innehåll på webbplatsen. Till skillnad från [Web SDK](../edge/home.md), [!DNL Server API] har ingen funktion för att automatiskt tillämpa innehåll som returneras av [!DNL Adobe Target] och [!DNL Offer Decisioning].

## Terminologi {#terminology}

Innan du arbetar med personaliseringslösningar från Adobe måste du förstå följande koncept:

* **Erbjudande**: ett erbjudande är ett marknadsföringsmeddelande som kan ha kopplade regler som fastställer vem som kan se erbjudandet.
* **Beslut**: Ett beslut (tidigare kallat erbjudandeaktivitet) informerar om valet av erbjudande.
* **Schema**: Schemat för ett beslut informerar den typ av erbjudande som returneras.
* **Omfång**: Beslutets omfattning.
   * I Adobe Target är detta [!DNL mbox]. The [!DNL global mbox] är `__view__` omfång
   * För [!DNL Offer Decisioning]är de Base64-kodade strängarna för JSON som innehåller de aktivitets- och placerings-ID som du vill att offera decisioningen ska använda för att föreslå erbjudanden.

## The `query` object {#query-object}

För att kunna hämta anpassat innehåll krävs ett explicit frågeobjekt för en begäran. Frågeobjektet har följande format:

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| Attribut | Typ | Obligatoriskt/valfritt | Beskrivning |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Krävs för målanpassning. Valfritt för Offer decisioning. | Lista med scheman som används i beslutet för att välja typ av returnerade erbjudanden. |
| `scopes` | `String[]` | Valfritt | Förteckning över beslutsomfattningar. Högst 30 per begäran. |

## Handtagsobjektet {#handle}

Personaliserat innehåll som hämtats från personaliseringslösningar presenteras i en `personalization:decisions` handle, som har följande format för sin nyttolast:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Attribut | Typ | Beskrivning |
| --- | --- | --- |
| `payload.id` | Sträng | Besluts-ID. |
| `payload.scope` | Sträng | Beslutets omfattning som resulterade i de föreslagna erbjudandena. |
| `payload.scopeDetails.decisionProvider` | Sträng | Ange till `TGT` när du använder Adobe Target. |
| `payload.scopeDetails.activity.id` | Sträng | Unikt ID för erbjudandeaktiviteten. |
| `payload.scopeDetails.experience.id` | Sträng | Unikt ID för erbjudandeplaceringen. |
| `items[].id` | Sträng | Unikt ID för erbjudandeplaceringen. |
| `items[].data.id` | Sträng | ID för det föreslagna erbjudandet. |
| `items[].data.schema` | Sträng | Schemat för innehållet som är associerat med det föreslagna erbjudandet. |
| `items[].data.format` | Sträng | Formatet på innehållet som är associerat med det föreslagna erbjudandet. |
| `items[].data.language` | Sträng | En array med språk som är associerade med innehållet i det föreslagna erbjudandet. |
| `items[].data.content` | Sträng | Innehåll som är associerat med det föreslagna erbjudandet i form av en sträng. |
| `items[].data.selector` | Sträng | HTML-väljare som används för att identifiera mål-DOM-elementet för ett DOM-åtgärdserbjudande. |
| `items[].data.prehidingSelector` | Sträng | HTML-väljaren används för att identifiera DOM-elementet som ska döljas när ett DOM-åtgärdserbjudande hanteras. |
| `items[].data.deliveryUrl` | Sträng | Bildinnehåll som är associerat med det föreslagna erbjudandet i formatet för en URL. |
| `items[].data.characteristics` | Sträng | Egenskaper som är kopplade till det föreslagna erbjudandet i formatet JSON-objekt. |

## Exempel på API-anrop {#sample-call}

**API-format**

```http
POST /ee/v2/interact
```

### Begäran {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `configId` | Sträng | Ja | DataStream ID. |
| `requestId` | Sträng | Nej | Ange ett ID för extern spårning av begäran. Om inget anges genereras ett Edge-nätverk åt dig och returneras i svarstexten/sidhuvudena. |

### Svar {#response}

Returnerar ett `200 OK` status och en eller flera `Handle` objekt, beroende på vilka edge-tjänster som är aktiverade i datastream-konfigurationen.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Meddelanden {#notifications}

Meddelanden ska utlösas när ett förhämtat innehåll eller en förhämtad vy har besöktes eller renderats för slutanvändaren. För att meddelanden ska kunna stängas av för rätt omfång måste du hålla reda på motsvarande `id` för varje omfång.

Meddelanden till höger `id` För att rapporteringen ska kunna speglas på rätt sätt krävs att motsvarande omfång aktiveras.

**API-format**

```http
POST /ee/v2/collect
```

### Begäran {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | ID för datastream som används av datainsamlingsslutpunkten. |
| `requestId` | `String` | Nej | Spårnings-ID för extern begäran. Om inget anges genereras ett Edge-nätverk åt dig och returneras i svarstexten/sidhuvudena. |
| `silent` | `Boolean` | Nej | Valfri boolesk parameter som anger om Edge Network ska returnera en `204 No Content` svar med en tom nyttolast. Kritiska fel rapporteras med motsvarande HTTP-statuskod och nyttolast. |

### Svar {#notifications-response}

Ett godkänt svar returnerar en av följande statusvärden och en `requestID` om ingen har angetts i begäran.

* `202 Accepted` när begäran har behandlats utan fel,
* `204 No Content` när begäran bearbetades och `silent` parametern är inställd på `true`;
* `400 Bad Request` när begäran inte var korrekt formulerad (t.ex. den obligatoriska primära identiteten inte hittades).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
