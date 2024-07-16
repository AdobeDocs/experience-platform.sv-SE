---
title: streamingMedia
description: Konfigurera Web SDK för att samla in data om medieanvändning på dina webbegenskaper.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# `streamingMedia`

Komponenten `streamingMedia` hjälper dig att samla in data relaterade till mediesessioner på din webbplats.

De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de samlats in kan du skicka dessa data till Adobe Experience Platform och/eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

## Förhandskrav {#prerequisites}

Om du vill använda komponenten `streamingMedia` i Web SDK måste du uppfylla följande krav:

* Kontrollera att du har tillgång till Adobe Experience Platform och/eller Adobe Analytics.
* Du måste använda Web SDK version 2.20.0 eller senare. Se [Web SDK-installationsöversikten](../../install/overview.md) för att lära dig hur du installerar den senaste versionen.
* Aktivera alternativet **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** för den datastream som du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera funktionen Direktuppspelning av media i Web SDK-konfigurationen, som visas på den här sidan, antingen via [taggtillägget](#tag-extension) eller via [JavaScript-biblioteket](#library).

## Konfigurera direktuppspelande media med hjälp av taggtillägget Web SDK {#tag-extension}

Följ stegen nedan för att konfigurera direktuppspelande media i Web SDK-taggtillägget.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Konfigurera inställningarna för **[!UICONTROL Streaming Media]** enligt beskrivningen på [konfigurationssidan för Web SDK-taggtillägg](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Konfigurera direktuppspelningsmedia med Web SDK JavaScript-biblioteket {#library}

Om du vill konfigurera direktuppspelande media i Web SDK använder du egenskaperna som beskrivs nedan.

Lägg till objektet `streamingMedia` när du anropar kommandot `configure`.

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
| `mainPingInterval` | Heltal | Nej | Fästfrekvens för huvudinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `10` och `50` sekunder.  Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](../createmediasession.md#automatic) används. |
| `adPingInterval` | Heltal | Nej | Fästfrekvens för annonsinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `1` och `10` sekunder. Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](../createmediasession.md#automatic) används. |
