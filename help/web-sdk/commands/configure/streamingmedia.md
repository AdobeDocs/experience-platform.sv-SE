---
title: mediaCollection
description: Konfigurera Web SDK för att samla in data om medieanvändning på dina webbegenskaper.
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# `streamingMedia`

The `streamingMedia` kan du samla in data om mediesessioner på din webbplats.

De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de samlats in kan du skicka dessa data till Adobe Experience Platform och/eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

## Förutsättningar {#prerequisites}

Använd `streamingMedia` som ingår i Web SDK, måste du uppfylla följande krav:

* Kontrollera att du har tillgång till Adobe Experience Platform och/eller Adobe Analytics.
* Du måste använda Web SDK version 2.20.0 eller senare. Se [Web SDK - installationsöversikt](../../install/overview.md) om du vill lära dig hur du installerar den senaste versionen.
* Aktivera **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** för den datastream du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera funktionen Direktuppspelning av media i Web SDK-konfigurationen, som visas på den här sidan, antingen via [taggtillägg](#tag-extension) eller via [JavaScript-bibliotek](#library).

## Konfigurera direktuppspelande media med hjälp av taggtillägget Web SDK {#tag-extension}

Följ stegen nedan för att konfigurera direktuppspelande media i Web SDK-taggtillägget.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Konfigurera **[!UICONTROL Streaming Media]** inställningarna enligt beskrivningen i [Konfigurationssida för SDK-taggtillägg](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Konfigurera direktuppspelningsmedia med JavaScript-biblioteket för Web SDK {#library}

Om du vill konfigurera direktuppspelande media i Web SDK använder du egenskaperna som beskrivs nedan.

När du anropar `configure` kommando, lägga till `streamingMedia` -objekt.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Egenskap | Typ | Obligatoriskt | Beskrivning |
|---------|----------|---------|---------|
| `channel` | Sträng | Ja | Namnet på den kanal där direktuppspelad mediainsamling sker. Exempel: `Video channel`. |
| `playerName` | Sträng | Ja | Namnet på mediespelaren. |
| `appVersion` | Sträng | Nej | Mediespelarprogrammets version. |
| `mainPingInterval` | Heltal | Nej | Fästfrekvens för huvudinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan variera från `10` till `50` sekunder.  Om inget värde anges används standardvärdet när du använder [automatiskt spårade sessioner](../createmediasession.md#automatic). |
| `adPingInterval` | Heltal | Nej | Fästfrekvens för annonsinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan variera från `1` till `10` sekunder. Om inget värde anges används standardvärdet när du använder [automatiskt spårade sessioner](../createmediasession.md#automatic). |
