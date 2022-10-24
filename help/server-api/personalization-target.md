---
title: Personalisering via Adobe Target
description: Lär dig hur du använder Server-API:t för att leverera och återge personaliserade upplevelser som skapats i Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: d6573f8f4d779fb7ed11b44561a0ad9667748b27
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# Personalisering via Adobe Target

## Översikt {#overview}

API:t för Edge Network Server kan leverera och återge personaliserade upplevelser som skapats i Adobe Target med hjälp av [Formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>Personaliseringsupplevelser som skapats med [Target Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) stöds inte fullt ut av Server-API:t. Server-API:t kan **hämta** aktiviteter skapade av VEC, men Server API kan inte **återge** aktiviteter skapade av VEC. Om du vill återge aktiviteter skapade av VEC använder du [Web SDK](../edge/home.md).

## Konfigurera ditt datastream {#configure-your-datastream}

Innan du kan använda Server-API:t i kombination med Adobe Target måste du aktivera Adobe Target-anpassning för din datastream-konfiguration.

Se [guide om hur du lägger till tjänster i ett datastream](../edge/datastreams/overview.md#adobe-target-settings), för detaljerad information om hur du aktiverar Adobe Target.

När du konfigurerar dataströmmen kan du (valfritt) ange värden för [!DNL Property Token], [!DNL Target Environment ID]och [!DNL Target Third Party ID Namespace].

![Användargränssnittsbild som visar konfigurationsskärmen för datastream-tjänsten, med Adobe Target markerat](assets/target-datastream.png)

Du kan välja mellan följande [!DNL Analytics Logging] alternativ:

* **[!DNL Server Side]**: Det här är standardalternativet för [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). När det här alternativet är markerat returneras det relevanta innehållet för varje gång personaliseringsinnehållet returneras av Target [!DNL A4T] data skickas automatiskt till Analytics utifrån svaret från Target-personaliseringsmotorn.
* **[!DNL Client Side]**: När det här alternativet är markerat returneras det relevanta innehållet för varje gång personaliseringsinnehållet returneras av Target [!DNL A4T] data returneras till det anropande programmet. Om ni avser att registrera dessa data i Analytics måste ni se till att de rapporteras vid en efterföljande anrop till [!DNL Analytics].

   >[!IMPORTANT]
   >
   >Förutom att markera **[!UICONTROL Client Side]** i målkonfigurationen måste du även inaktivera Analytics (Analyser) för att Edge Network ska kunna returnera [!DNL A4T] information tillbaka till svaret.


## Egna parametrar {#custom-parameters}

De flesta fälten i [!DNL XDM] del av varje begäran serialiseras till punktnotation och skickas sedan till Target som anpassad eller [!DNL mbox] parametrar.


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

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Uppdateringar av målprofiler {#profile-update}

The [!DNL Server API] tillåter uppdateringar av Target-profilen. Om du vill uppdatera en målprofil kontrollerar du att profildata skickas i `data` del av begäran i följande format:

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

Frågedelen av begäran avgör vilket innehåll som returneras av Target. Under `personalization` objekt, `schemas` Anger vilken typ av innehåll som ska returneras av Target.

I situationer där du är osäker på vilka erbjudanden du kommer att hämta bör du inkludera alla fyra scheman i din personaliseringsfråga till Edge Network:

* **HTML-baserade erbjudanden:**
https://ns.adobe.com/personalization/html-content-item
* **JSON-baserade erbjudanden:**
https://ns.adobe.com/personalization/json-content-item
* **Omdirigeringserbjudanden**
https://ns.adobe.com/personalization/redirect-item
* **Target DOM Manipulation offers**
https://ns.adobe.com/personalization/dom-action

### Beslutsomfattningar {#decision-scopes}

Adobe Target [!DNL mbox] namn ska tas med i `decisionScopes` -array för att returnera rätt innehåll.

#### Exempel {#decision-scopes-example}

I exemplet nedan efterfrågas alla fyra erbjudandetyperna tillsammans med en Target-aktivitet som kallas `serverapimbox`.

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

Edge Network returnerar ett svar som liknar det nedan.

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

Om besökaren kvalificerar sig för en personaliseringsaktivitet baserat på data som skickas till Adobe Target, hittar du det relevanta aktivitetsinnehållet under `handle` objekt, där typen är `personalization:decisions`.

Annat innehåll returneras ibland under `handle` också. Andra innehållstyper är inte relevanta för målpersonaliseringen. Om besökaren kvalificerar sig för flera aktiviteter blir varje aktivitet en separat `personalization` -objektet i arrayen.

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
