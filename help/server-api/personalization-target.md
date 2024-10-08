---
title: Personalization via Adobe Target
description: Lär dig hur du använder Server-API:t för att leverera och återge personaliserade upplevelser som skapats i Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Personalization via Adobe Target

## Översikt {#overview}

Edge Network Server-API:t kan leverera och återge personaliserade upplevelser som skapats i Adobe Target med hjälp av [formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

>[!IMPORTANT]
>
>Personalization-upplevelser som skapats med [VEC (Target Visual Experience Composer)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) stöds inte helt av Server-API:t. Server-API:t kan **hämta** aktiviteter som skapats av VEC, men Server-API kan inte **återge** aktiviteter som skapats av VEC. Om du vill återge aktiviteter som har skapats av VEC implementerar du [hybridanpassning](../web-sdk/personalization/hybrid-personalization.md) med Web SDK och Edge Network Server-API:t.

## Konfigurera ditt datastream {#configure-your-datastream}

Innan du kan använda Server-API:t i kombination med Adobe Target måste du aktivera Adobe Target-anpassning för din datastream-konfiguration.

Mer information om hur du aktiverar Adobe Target finns i [guiden om hur du lägger till tjänster i ett dataflöde](../datastreams/overview.md#adobe-target-settings).

När du konfigurerar din datastream kan du (valfritt) ange värden för [!DNL Property Token], [!DNL Target Environment ID] och [!DNL Target Third Party ID Namespace].

![Användargränssnittsbild som visar konfigurationsskärmen för datastream-tjänsten, med Adobe Target markerat](assets/target-datastream.png)

## Egna parametrar {#custom-parameters}

De flesta fält i delen [!DNL XDM] i varje begäran serialiseras till punktnotation och skickas sedan till Target som anpassade parametrar eller [!DNL mbox] -parametrar.


### Exempel {#custom-parameters-example}

I följande XDM-exempel:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

När du skapar målgrupper i Target är följande värden tillgängliga som anpassade parametrar:

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Uppdateringar av målprofiler {#profile-update}

[!DNL Server API] tillåter uppdateringar av målprofilen. Om du vill uppdatera en målprofil kontrollerar du att profildata skickas i `data`-delen av begäran i följande format:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Fråga om målaktiviteter {#querying-target-activities}

### Scheman {#schemas}

Frågedelen av begäran avgör vilket innehåll som returneras av Target. Under objektet `personalization` bestämmer `schemas` vilken typ av innehåll som ska returneras av Target.

I situationer där du är osäker på vilka erbjudanden du kommer att hämta bör du inkludera alla fyra scheman i din personaliseringsfråga till Edge Network:

* **HTML-baserade erbjudanden:**
https://ns.adobe.com/personalization/html-content-item
* **JSON-baserade erbjudanden:**
https://ns.adobe.com/personalization/json-content-item
* **Omdirigeringserbjudanden för mål**
https://ns.adobe.com/personalization/redirect-item
* **Target DOM Manipulation offers**
https://ns.adobe.com/personalization/dom-action

### Beslutsomfattningar {#decision-scopes}

Adobe Target [!DNL mbox]-namn bör inkluderas i `decisionScopes`-arrayen för att returnera rätt innehåll.

#### Exempel {#decision-scopes-example}

I exemplet nedan efterfrågas alla fyra erbjudandetyperna tillsammans med en Target-aktivitet med namnet `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
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

En fullständig begäran som innehåller ett fullständigt XDM-objekt, profilparametrar samt lämplig Target-fråga beskrivs nedan.

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
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Svar {#response}

Edge Network kommer att returnera ett svar som liknar det nedan.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Om besökaren kvalificerar sig för en personaliseringsaktivitet baserat på data som skickas till Adobe Target, kommer det relevanta aktivitetsinnehållet att hittas under objektet `handle`, där typen är `personalization:decisions`.

Annat innehåll returneras ibland även under `handle`. Andra innehållstyper är inte relevanta för målpersonaliseringen. Om besökaren kvalificerar sig för flera aktiviteter blir varje aktivitet ett separat `personalization`-objekt i arrayen.

Tabellen nedan förklarar de viktigaste elementen i den delen av svaret.

| Egenskap | Beskrivning | Exempel |
|---|---|---|
| `scope` | Namnet på målmbox som resulterade i de föreslagna erbjudandena. | `"scope": "serverapimbox"` |
| `items[].schema` | Schemat för innehållet som är associerat med det föreslagna erbjudandet. Detta relateras till den aktivitetstyp som du valde när du skapade personaliseringsaktiviteten. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | Unikt ID för erbjudandeaktiviteten. Vanligtvis ett 6-siffrigt tal. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Namnet på den användarspecificerade erbjudandeaktiviteten. Detta anges när aktiviteten skapas. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | Det unika ID:t för personaliseringsupplevelsen. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Det unika namnet på personaliseringsupplevelsen. | `"experience.name": "Experience A"` |
| `items[].data.id` | ID för det föreslagna erbjudandet. | `"id": "282484"` |
| `items[].data.format` | Formatet på innehållet som är associerat med det föreslagna erbjudandet. | `"format: "application/json` |
| `items[].data.content` | Innehåll som är associerat med det föreslagna erbjudandet. Detta kommer att användas för personalisering av innehåll i det anropande programmet. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Exempelprogram för personalisering på serversidan {#sample}

Exempelprogrammet som finns på [den här URL:en](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) visar hur du använder Adobe Experience Platform för att hämta personaliseringsinnehåll från Adobe Target. Webbsidan ändras baserat på det personaliseringsinnehåll som returneras.

Det här exemplet förlitar sig _inte_ på klientbibliotek som [!DNL Web SDK] för att få personaliserat innehåll. Istället används Adobe Experience Platform API:er för att hämta personaliseringsinnehåll. Sedan genererar implementeringen serversidan på HTML baserat på det personaliseringsinnehåll som returneras.
