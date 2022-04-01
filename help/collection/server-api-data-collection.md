---
title: Datainsamling
description: Läs om hur API:t för Adobe Experience Platform Edge Network Server strukturerar insamlade data
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: datainsamling;samling;Adobe Experience Platform Edge Network;api;struktur
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---


# Datainsamling

The [!DNL Server API] har två typer av datainsamlingsslutpunkter:

* [Interaktiva slutpunkter för datainsamling](interactive-data-collection.md), som används när klienten förväntar sig att ett svar returneras av servern. Dessa slutpunkter kan också returnera innehåll från andra Edge Network-tjänster när datainsamling utförs.
* [Icke-interaktiv insamling av händelsedata](non-interactive-data-collection.md)används när inget svar förväntas från servern. De här slutpunkterna används bara för datainsamling.

## `Event` object {#event-object}

Data som samlats in av [!DNL Server API] är strukturerad i `Event` -objekt. Objektets struktur beskrivs nedan.

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
| `xdm` | Objekt | *Obligatoriskt*. JSON-objekt som innehåller data i XDM-format, som motsvarar dataset-schemat. |
| `data` | Objekt | *Valfritt*. JSON-objekt som innehåller frihandsdata, som kan mappas till XDM av Edge Network. |

