---
title: kontext
description: Samla automatiskt in data om enheter, miljö eller plats.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# `context`

Egenskapen `context` är en matris med strängar som avgör vad Web SDK kan samla in automatiskt. Även om dessa data kan ge mycket värde kan det vara bra att utelämna en del av dessa data så att du kan följa organisationens sekretesspolicy.

## Sammanhangsnyckelord och XDM-element

Om du tar med ett givet kontextnyckelord fyller Web SDK automatiskt i alla associerade XDM-element. Om du vill utesluta ett specifikt XDM-element och samtidigt tillåta andra, kan du ta bort värden med [`onBeforeEventSend`](onbeforeeventsend.md). Om du skickar flera händelser på en sida innehåller Web SDK dessa fält vid varje `SendEvent`-anrop.

### Webb

Nyckelordet `"web"` samlar in information om den aktuella sidan.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Sidans URL | Den aktuella sidans URL. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referent-URL | URL-adressen till föregående sida som besöktes. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### Enhet

Nyckelordet `"device"` samlar in information om användarens enhet.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Skärmhöjd | Skärmens höjd i pixlar. | `xdm.device.screenHeight` | `900` |
| Skärmbredd | Skärmens bredd i pixlar. | `xdm.device.screenWidth` | `1440` |
| Skärmorientering | Skärmens orientering. | `xdm.device.screenOrientation` | `landscape` eller `portrait` |

### Miljö

Nyckelordet `"environment"` samlar in information om användarens webbläsare.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Miljötyp | Den typ av miljö som upplevelsen upplevde. Web SDK anger alltid det här fältet som `browser`. | `xdm.environment.type` | `browser` |
| Höjd på visningsruta | Höjden på webbläsarens innehållsområde i pixlar. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Bredd på visningsruta | Bredden på webbläsarens innehållsområde i pixlar. | `xdm.environment.browserDetails.viewportWidth` | `642` |

### Montera kontext

Nyckelordet `"placeContext"` samlar in information om användarens plats.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Lokal tid | Lokal tidsstämpel för slutanvändaren i förenklat utökat [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)-format. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokal tidszonsförskjutning | Antalet minuter som användaren är förskjuten från GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Landskod | Slutanvändarens landskod. | `xdm.placeContext.geo.countryCode` | `US` |
| Statsprovins | Slutanvändarens landskod. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitude | Slutanvändarens latitud. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitud | Slutanvändarens longitud. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

### Tidsstämpel

Nyckelordet `"timestamp"` samlar in information om händelsens tidsstämpel. Den här kontexten inkluderas alltid och kan inte tas bort.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Tidsstämpel för händelsen | UTC-tidsstämpel för slutanvändaren i förenklat utökat [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)-format. | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### Implementeringsinformation

Nyckelordet `implementationDetails` samlar in information om den SDK-version som används för att samla in händelsen.

| Dimension | Beskrivning | XDM-sökväg | Exempelvärde |
| --- | --- | --- | --- |
| Namn | Identifieraren för SDK (Software Development Kit). I det här fältet används en URI för att förbättra unika identifierare som tillhandahålls av olika programbibliotek. | `xdm.implementationDetails.name` | När det fristående biblioteket används är värdet `https://ns.adobe.com/experience/alloy`. När biblioteket används som en del av taggtillägget är värdet `https://ns.adobe.com/experience/alloy+reactor`. |
| Version | Programvaruutvecklingsverktyget (SDK). | `xdm.implementationDetails.version` | När det fristående biblioteket används är värdet biblioteksversionen. När biblioteket används som en del av taggtillägget är värdet biblioteksversionen och taggtilläggsversionen som är kopplad till en `+`. Om biblioteksversionen till exempel är `2.1.0` och taggtilläggsversionen är `2.1.3` blir värdet `2.1.0+2.1.3`. |
| Miljö | Den miljö där data samlades in. Det här fältet är alltid inställt på `browser` när du använder JavaScript-biblioteket. | `xdm.implementationDetails.environment` | `browser` |

### Tips för hög entropi-klient {#high-entropy-client-hints}

Nyckelordet `"highEntropyUserAgentHints"` samlar in detaljerad information om användarens enhet. Dessa data inkluderas i HTTP-huvudet för den begäran som skickas till Adobe. När data har anlänt till Edge-nätverket fyller XDM-objektet i sin respektive XDM-sökväg. Om du anger respektive XDM-sökväg i ditt `sendEvent`-anrop har den företräde framför HTTP-rubrikvärdet.

Om du använder enhetssökningar när [du konfigurerar ditt datastream](/help/datastreams/configure.md) kan data rensas till förmån för enhetssökningsvärden. Vissa klienttipsfält och enhetssökningsfält kan inte finnas i samma träff.

| Egenskap | Beskrivning | HTTP-huvud | XDM-sökväg | Exempel |
| --- | --- | --- | --- | --- |
| Operativsystemversion | Operativsystemets version. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Arkitektur | CPU underliggande arkitektur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Enhetsmodell | Namnet på den enhet som används. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitness | Antalet bitar som den underliggande CPU-arkitekturen stöder. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Webbläsarleverantör | Företaget som skapade webbläsaren. Det låga entropytipset `Sec-CH-UA` samlar också in det här elementet. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Webbläsarnamn | Webbläsaren används. Det låga entropytipset `Sec-CH-UA` samlar också in det här elementet. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Webbläsarversion | Den viktiga versionen av webbläsaren. Det låga entropytipset `Sec-CH-UA` samlar också in det här elementet. Exakt webbläsarversion samlas inte in automatiskt. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

Mer information finns i [Klienttips för användaragent](/help/collection/use-cases/client-hints.md).

### Referent för engångsanalys {#one-time-analytics-referrer}

Nyckelordet `"oneTimeAnalyticsReferrer"` skickar endast ett referensvärde till Adobe Analytics vid det första icke-beslutande `sendEvent`-anropet för en sida. Det primära användningsområdet för det här kontextnyckelordet är att förhindra att dimensionen [Referer](https://experienceleague.adobe.com/sv/docs/analytics/components/dimensions/referrer) i Adobe Analytics fylls av träffar som i första hand används i integreringar med Analytics och Target.

Om ett angivet `sendEvent`-kommando använder en beslutshändelsetyp (`decisioning.propositionFetch`, `decisioning.propositionDisplay`, `decisioning.propositionInteract`), ignoreras det när den första `sendEvent` beräknas på en sida. Om referensvärdet ändras på sidan och ett annat `sendEvent` aktiveras, inkluderas det nya referensvärdet i nyttolasten. Detta villkor gör att funktionen kan användas med enkelsidiga program.

När ett duplicerat referensvärde upptäcks ställs `data.__adobe.analytics.referrer` in på en tom sträng (`""`) i biblioteket.
Om du ställer in det här dataobjektfältet på en tom sträng raderas värdet när en träff kommer till Adobe Analytics eftersom dataobjektet skriver över ett XDM-objektmotsvarande fält. Det påverkar inte XDM-objektet, vilket innebär att data kan fortsätta att skickas till en Experience Platform-datauppsättning om du inkluderar flera tjänster i en datastream.

## Implementering

Ange strängarrayen `context` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar SDK samlas all kontextinformation förutom `"highEntropyUserAgentHints"` och `"oneTimeAnalyticsReferrer"` in som standard. Ange den här egenskapen om du vill samla in klienttips med hög entropi, eller om du vill utelämna annan kontextinformation från datainsamlingen. Strängar kan inkluderas i vilken ordning som helst.

>[!TIP]
>
>Om du vill samla in all kontextinformation, inklusive tips för hög entropi-klient, måste du ta med alla värden i `context`-arraysträngen. Standardvärdet `context` utelämnar `"highEntropyUserAgentHints"` och `"oneTimeAnalyticsReferrer"`. Om du anger egenskapen `context` samlar inga utelämnade värden in data.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"]
});
```

## Samla in kontextinformation med taggtillägget Web SDK

Se [Kontextinställningar](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings) under konfigurationsinställningar för datainsamling i dokumentationen för SDK-taggtillägg för webben.
