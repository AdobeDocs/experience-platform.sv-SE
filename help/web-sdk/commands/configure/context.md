---
title: kontext
description: Samla automatiskt in data om enheter, miljö eller plats.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# `context`

The `context` -egenskapen är en array med strängar som avgör vad Web SDK kan samla in automatiskt. Även om dessa data kan ge mycket värde kan det vara bra att utelämna en del av dessa data så att du kan följa organisationens sekretesspolicy.

## Sammanhangsnyckelord och XDM-element

Om du inkluderar ett givet kontextnyckelord fyller Web SDK automatiskt i alla associerade XDM-element. Om du vill utesluta ett visst XDM-element och samtidigt tillåta andra, kan du ta bort värden med [`onBeforeEventSend`](onbeforeeventsend.md). Om du skickar flera händelser på en sida innehåller Web SDK dessa fält på varje `SendEvent` ring.

### Webb

The `"web"` nyckelordet samlar in information om den aktuella sidan.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Sidans URL | Den aktuella sidans URL. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referent-URL | URL-adressen till föregående sida som besöktes. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Enhet

The `"device"` nyckelordet samlar in information om användarens enhet.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Skärmhöjd | Skärmens höjd i pixlar. | `xdm.device.screenHeight` | `900` |
| Skärmbredd | Skärmens bredd i pixlar. | `xdm.device.screenWidth` | `1440` |
| Skärmorientering | Skärmens orientering. | `xdm.device.screenOrientation` | `landscape` eller `portrait` |

{style="table-layout:auto"}

### Miljö

The `"environment"` nyckelordet samlar in information om användarens webbläsare.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Miljötyp | Den typ av miljö som upplevelsen upplevde. Web SDK anger alltid det här fältet som `browser`. | `xdm.environment.type` | `browser` |
| Höjd på visningsruta | Höjden på webbläsarens innehållsområde i pixlar. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Bredd på visningsruta | Bredden på webbläsarens innehållsområde i pixlar. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Montera kontext

The `"placeContext"` nyckelordet samlar in information om användarens plats.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Lokal tid | Lokal tidsstämpel för slutanvändaren i förenklad utökad [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) format. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokal tidszonsförskjutning | Antalet minuter som användaren är förskjuten från GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Tips för hög entropi-klient

The `"highEntropyUserAgentHints"` nyckelordet samlar in detaljerad information om användarens enhet. Dessa data inkluderas i HTTP-huvudet för den begäran som skickas till Adobe. När data har kommit in i Edge-nätverket fyller XDM-objektet i sin respektive XDM-sökväg. Om du anger respektive XDM-sökväg i `sendEvent` -anropet har företräde framför HTTP-rubrikvärdet.

Om du använder enhetssökningar när [konfigurera ditt datastream](/help/datastreams/configure.md), kan data rensas bort till förmån för enhetssökningsvärden. Vissa klienttipsfält och enhetssökningsfält kan inte finnas i samma träff.

| Dimension | Beskrivning | HTTP-huvud | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- | --- |
| Operativsystemversion | Operativsystemets version. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Arkitektur | Den underliggande processorarkitekturen. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Enhetsmodell | Namnet på den enhet som används. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Bitness | Antalet bitar som den underliggande processorarkitekturen stöder. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Webbläsarleverantör | Företaget som skapade webbläsaren. Tipset low entropy `Sec-CH-UA` samlar också in det här elementet. | `Sec-CH-UA-Full-Version-List` | | |
| Webbläsarnamn | Webbläsaren används. Tipset low entropy `Sec-CH-UA` samlar också in det här elementet. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Webbläsarversion | Den viktiga versionen av webbläsaren. Tipset low entropy `Sec-CH-UA` samlar också in det här elementet. Exakt webbläsarversion samlas inte in automatiskt. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Samla in kontextinformation med taggtillägget Web SDK

Kontextinformationsinställningen är en kombination av alternativknappar och kryssrutor när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Varje kryssruta mappas till ett kontextnyckelord.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] välj sedan antingen **[!UICONTROL All default context information]** eller **[!UICONTROL Specific context information]**.
1. Om du väljer **[!UICONTROL Specific context information]** markerar du kryssrutan bredvid varje element för kontextinformation som du vill använda.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Samla in kontextinformation med Web SDK JavaScript-biblioteket

Ange `context` matris med strängar när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar SDK:n, kommer all kontextinformation förutom `"highEntropyUserAgentHints"` samlas in som standard. Ange den här egenskapen om du vill samla in klienttips med hög entropi, eller om du vill utelämna annan kontextinformation från datainsamlingen. Strängar kan inkluderas i vilken ordning som helst.

>[!NOTE]
>
>Om du vill samla in all kontextinformation, inklusive tips för hög entropi-klient, måste du ta med alla värden i `context` arraysträng. Standardvärdet `context` värde utelämnas `highEntropyUserAgentHints`och om du anger `context` egenskapen, alla utelämnade värden samlar inte in data.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
