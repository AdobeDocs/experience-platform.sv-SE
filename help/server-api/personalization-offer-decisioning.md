---
title: Personalisering via Offer decisioning
description: Lär dig hur du använder Server-API:t för att leverera och återge personaliserade upplevelser via Offer decisioning.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Personalisering via Offer decisioning

## Översikt {#overview}

API:t för Edge Network Server kan leverera personaliserade upplevelser som hanteras i [offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) till webbkanalen.

[!DNL Offer Decisioning] har stöd för ett icke-visuellt gränssnitt för att skapa, aktivera och leverera aktiviteter och personaliseringsupplevelser.

## Förutsättningar {#prerequisites}

Personalisering via [!DNL Offer Decisioning] kräver att du har åtkomst till [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en) innan du konfigurerar integreringen.

## Konfigurera ditt datastream {#configure-your-datastream}

Innan du kan använda server-API:t tillsammans med Offer decisioning måste du aktivera Adobe Experience Platform-anpassning för din datastream-konfiguration och aktivera **[!UICONTROL Offer Decisioning]** alternativ.

Se [guide om hur du lägger till tjänster i ett datastream](../datastreams/overview.md#adobe-experience-platform-settings), för detaljerad information om hur du aktiverar Offer decisioning.

![Användargränssnittsbild som visar konfigurationsskärmen för datastream-tjänsten, med Offer decisioning markerad](assets/aep-od-datastream.png)

## Skapa målgrupper {#audience-creation}

[!DNL Offer Decisioning] använder Adobe Experience Platform Segmentation Service för att skapa målgrupper. Dokumentationen till [!DNL Segmentation Service] [här](../segmentation/home.md).

## Definiera beslutsomfattningar {#creating-decision-scopes}

The [!DNL Offer Decision Engine] använder Adobe Experience Platform data och [Kundprofiler i realtid](../profile/home.md), tillsammans med [!DNL Offer Library], för att leverera erbjudanden till rätt kunder och kanaler vid rätt tidpunkt.

Läs mer om [!DNL Offer Decisioning Engine], se den dedikerade [dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html).

Efter [konfigurera ditt datastream](#configure-your-datastream)måste ni definiera de beslutsomfattningar som ska användas i er personaliseringskampanj.

[Beslutsomfattningar](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) är de Base64-kodade JSON-strängarna som innehåller aktivitets- och placerings-ID:n som du vill använda [!DNL Offer Decisioning Service] att använda vid offerter.

**Beslutsomfattelse JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**Beslutsomfattare Base64-kodad sträng**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

När du har skapat dina erbjudanden och samlingar måste du definiera en [beslutsområde](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes).

Kopiera Base64-kodad beslutsomfattning. Du kommer att använda den i `query` objekt för Server API-begäran.

![Användargränssnittsbild som visar användargränssnittet för Offera decisioningen och som framhäver beslutsomfånget.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## Exempel på API-anrop {#api-example}

**API-format**

```http
POST /ee/v2/interact
```

### Begäran {#request}

En fullständig begäran som innehåller ett fullständigt XDM-objekt, dataobjekt och en Offer decisioning-fråga beskrivs nedan.

>[!NOTE]
>
>The `xdm` och `data` -objekt är valfria och behövs bara för Offer decisioning om du har skapat segment med villkor som använder fält i något av dessa objekt.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            }
        },
        "data": {
            "page": {
                "pageInfo": {
                    "pageName": "Promotions",
                    "siteSection": "Home"
                },
                "promos": {
                    "heroPromos": "purse,shoes,sunglasses"
                },
                "customVariables": {
                    "testGroup": "orange/black theme"
                },
                "events": {
                    "homePage": true
                },
                "products": [
                    {
                        "productSKU": "abc123",
                        "productName": "shirt"
                    }
                ]
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Svar {#response}

Edge Network returnerar ett svar som liknar det nedan.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Om besökaren kvalificerar sig för en personaliseringsaktivitet baserat på data som skickas till [!DNL Offer Decisioning], kommer det relevanta aktivitetsinnehållet att finnas under `handle` objekt, där typen är `personalization:decisions`.

Annat innehåll returneras under `handle` -objekt också. Andra innehållstyper är inte relevanta för [!DNL Offer Decisioning] personalisering. Om besökaren kvalificerar sig för flera aktiviteter finns de i en array.

Tabellen nedan förklarar de viktigaste elementen i den delen av svaret.

| Egenskap | Beskrivning | Exempel |
|---|---|---|
| `scope` | Beslutsomfattandet som hör till de föreslagna erbjudanden som returnerades. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Unikt ID för erbjudandeaktiviteten. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Unikt ID för erbjudandeplaceringen. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | Unikt ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schemat för innehållet som är associerat med det föreslagna erbjudandet. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | Unikt ID för det föreslagna erbjudandet. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Formatet på innehållet som är associerat med det föreslagna erbjudandet. | `"format": "text/html"` |
| `language` | En array med språk som är associerade med innehållet i det föreslagna erbjudandet. | `"language": [ "en-US" ]` |
| `content` | Innehåll som är associerat med det föreslagna erbjudandet i form av en sträng. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinnehåll som är associerat med det föreslagna erbjudandet i formatet för en URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON-objekt som innehåller de egenskaper som är associerade med det föreslagna erbjudandet. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
