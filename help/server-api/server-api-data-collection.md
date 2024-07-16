---
title: Datainsamling
description: Läs om hur Adobe Experience Platform Edge Network Server-API strukturerar insamlade data.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 2%

---


# Datainsamling

[!DNL Server API] erbjuder två typer av datainsamlingsslutpunkter:

* [Interaktiva datainsamlingsslutpunkter](interactive-data-collection.md) som används när klienten förväntar sig att ett svar returneras av servern. Dessa slutpunkter kan också returnera innehåll från andra Edge Network-tjänster när datainsamling utförs.
* [Icke-interaktiv händelsedatainsamling](non-interactive-data-collection.md) som används när inget svar förväntas från servern. De här slutpunkterna används bara för datainsamling.

## `Event` objekt {#event-object}

Data som samlas in av [!DNL Server API] är strukturerade i objektet `Event`. Objektets struktur beskrivs nedan.

```json
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
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Attribut | Typ | Beskrivning |
| --- | --- | --- |
| `xdm` | Objekt | *Krävs*. JSON-objekt som innehåller data i XDM-format, som motsvarar dataset-schemat. |
| `data` | Objekt | *Valfritt*. JSON-objekt som innehåller frihandsdata, som kan mappas till XDM av Edge Network. |

