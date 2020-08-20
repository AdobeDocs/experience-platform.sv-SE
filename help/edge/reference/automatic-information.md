---
title: Information samlas in automatiskt
seo-title: Information som samlas in automatiskt av Adobe Experience Platform Web SDK
description: Beskrivning av all information som Adobe Experience Cloud SDK automatiskt samlar in
seo-description: Beskrivning av all information som Adobe Experience Cloud SDK automatiskt samlar in
keywords: collect information;context;configure;device;screenHeight;screen Height;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewport Height;viewportWidth;viewport Width;crowserDetails;browser details;implementationDetails;implementation Details;name;version;placeContext;localTime;local Time;localTimezoneOffset;local Timezone Offset;timestamp;web;url;webPageDetails;web Page Details;webReferrer;web Referrer;landscape;portrait;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 7%

---


# Information samlas in automatiskt

Adobe Experience Cloud SDK samlar automatiskt in ett antal informationsdelar utan specialkonfigurationer. Den här informationen kan dock inaktiveras om det behövs med hjälp av `context` alternativet i `configure` kommandot. [Se Konfigurera SDK](../fundamentals/configuring-the-sdk.md). Nedan finns en lista över dessa informationsdelar. Namnet inom parentes anger den sträng som ska användas när kontexten konfigureras.

## Device (`device`)

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

Den typ av miljö som upplevelsen mötte. Adobe Experience Platform SDK för JavaScript anges alltid `browser`.

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

SDK-identifierare (Software Development Kit).  I det här fältet används en URI för att förbättra unika identifierare som tillhandahålls av olika programbibliotek.

### Version

| **Sökväg i nyttolast:** | **Exempel:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Miljö

| **Sökväg i nyttolast:** | **Exempel:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Montera kontext (`placeContext`)

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

UTC-tidsstämpel för slutanvändaren i det förenklade utökade ISO-formatet [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

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
