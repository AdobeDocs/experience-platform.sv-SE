---
title: Automatiskt insamlad information
description: En översikt över de data som Adobe Experience Platform Web SDK samlar in automatiskt.
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# Automatiskt insamlad information

Adobe Experience Platform Web SDK samlar automatiskt in viss information. Om din organisation inte vill samla in dessa data automatiskt kan du använda `context` i [`configure` kommando](../fundamentals/configuring-the-sdk.md).

Nyckelord som inte ingår i `context` arrayen ingår inte i datainsamlingen. Om `context` arrayen finns inte i `configure` samlas alla data i tabellen nedan in automatiskt.

| Namn | Beskrivning | `context` array, nyckelord | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- | --- |
| Skärmhöjd | Skärmens höjd i pixlar. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Skärmbredd | Skärmens bredd i pixlar. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Skärmorientering | Skärmens orientering. | `device` | `events[].xdm.device.screenOrientation` | `landscape` eller `portrait` |
| Miljötyp | Den typ av miljö som upplevelsen upplevde. Adobe Experience Platform Web SDK anger alltid att fältet ska vara `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Höjd på visningsruta | Höjden på webbläsarens innehållsområde i pixlar. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Bredd på visningsruta | Bredden på webbläsarens innehållsområde i pixlar. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK-namn | SDK-identifieraren. I det här fältet används en URI för att förbättra unika identifierare som tillhandahålls av olika programbibliotek. När det fristående biblioteket används är värdet `https://ns.adobe.com/experience/alloy`. När biblioteket används som en del av taggtillägget är värdet `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK-version | När det fristående biblioteket används är värdet biblioteksversionen. När biblioteket används som en del av taggtillägget är värdet en sammanfogning av biblioteksversionen och taggtilläggsversionen. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Miljö | Den miljö där data samlades in. Adobe Experience Platform Web SDK anger alltid att fältet ska vara `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Lokal tid | Lokal tidsstämpel för slutanvändaren i förenklat utökat ISO-format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokal tidszonsförskjutning | Antal minuter som användaren är förskjuten från GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Tidsstämpel | UTC-tidsstämpeln för slutanvändaren i förenklat utökat ISO-format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Ingår alltid | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| Aktuell sidadress | Den aktuella sidans URL. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referent-URL | URL-adressen till föregående sida som besöktes. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
