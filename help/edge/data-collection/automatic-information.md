---
title: Automatiskt insamlad information i Adobe Experience Platform Web SDK
description: En översikt över all information som Adobe Experience Platform SDK samlar in automatiskt.
keywords: samla in information;kontext;konfigurera;enhet;screenHeight;screen Height;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewport Height;viewportWidth;viewport Width;populserDetails;browser details;implementationDetails;implementation Details;name;version;placeContext;local Time;local Time zoneOffset;local Timezone Offset;timestamp;web;url;webPageDetails;web page Details;webReferrer;web Referrer;landscape;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: e3f507e010ea2a32042b53d46795d87e82e3fb72
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---

# Automatiskt insamlad information

Adobe Experience Platform Web SDK samlar automatiskt in ett antal informationsdelar utan specialkonfigurationer. Den här informationen kan dock inaktiveras om det behövs med `context` i `configure` -kommando. [Se Konfigurera SDK](../fundamentals/configuring-the-sdk.md). Nedan finns en lista över dessa informationsdelar. Namnet inom parentes anger den sträng som ska användas när kontexten konfigureras.

## Enhet (`device`)

Information om enheten. Detta inkluderar inte data som kan slås upp på serversidan från användaragentsträngen.

### Skärmhöjd

| **Sökväg i nyttolast:** | **Exempel:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Skärmens höjd i pixlar.

### Skärmorientering

| **Sökväg i nyttolast:** | **Möjliga värden:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` eller `portrait` |

Skärmens orientering.

### Skärmbredd

| **Sökväg i nyttolast:** | **Exempel:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Skärmens bredd (i pixlar).

## Miljö (`environment`)

Information om webbläsarmiljön.

### Miljötyp

Webbläsare

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Den typ av miljö som upplevelsen upplevde. Adobe Experience Platform Web SDK anger alltid detta till `browser`.

### Höjd på visningsruta

| **Sökväg i nyttolast:** | **Exempel:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Höjden på webbläsarens innehållsområde (i pixlar).

### Bredd på visningsruta

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Bredden på webbläsarens innehållsområde (i pixlar).

## Implementeringsinformation

Information om SDK som används för att samla in händelsen.

### Namn

| **Sökväg i nyttolast:** | **Exempel:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

SDK-identifierare (Software Development Kit).  I det här fältet används en URI för att förbättra unika identifierare som tillhandahålls av olika programbibliotek. När det fristående biblioteket används är värdet `https://ns.adobe.com/experience/alloy`. När biblioteket används som en del av taggtillägget är värdet `https://ns.adobe.com/experience/alloy+reactor`.

### Version

| **Sökväg i nyttolast:** | **Exempel:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

När det fristående biblioteket används är värdet helt enkelt biblioteksversionen. När biblioteket används som en del av taggtillägget är det biblioteksversionen och taggtilläggsversionen som är kopplad till ett plustecken (+). Om biblioteksversionen till exempel var 2.1.0 och taggtilläggsversionen var 2.1.3, skulle värdet vara `2.1.0+2.1.3`.

### Miljö {#environment}

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Den miljö där data samlades in. Den här inställningen är alltid inställd på `browser`.

## Montera kontext (`placeContext`) {#place-context}

Information om slutanvändarens plats.

### Lokal tid

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Lokal tidsstämpel för slutanvändaren i förenklat utökat ISO-format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Lokal tidszonsförskjutning

| **Sökväg i nyttolast:** | **Exempel:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Antal minuter som användaren är förskjuten från GMT.

## Tidsstämpel

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Tidsstämpeln för händelsen.  Den här delen av kontexten kan inte tas bort.

UTC-tidsstämpel för slutanvändaren i förenklat utökat ISO-format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Webbinformation (`web`)

Information om sidan som användaren är på.

### Aktuell sidadress

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

Den aktuella sidans URL.

### Referent-URL

| **Sökväg i nyttolast:** | **Exempel:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

URL-adressen till föregående sida som besöktes.
