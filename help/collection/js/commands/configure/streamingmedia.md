---
title: streamingMedia
description: Konfigurera Web SDK för att samla in data om medieanvändning på dina webbegenskaper.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# `streamingMedia`

Komponenten `streamingMedia` hjälper dig att samla in data relaterade till mediesessioner på din webbplats.

De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de samlats in kan du skicka dessa data till Adobe Experience Platform eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

## Förhandskrav

Om du vill använda komponenten `streamingMedia` i Web SDK måste du uppfylla följande krav:

* Se till att du har tillgång till Adobe Experience Platform eller Adobe Analytics.
* Du måste använda Web SDK version 2.20.0 eller senare. Se [installationsöversikten för Web SDK](../../install/overview.md) om du vill veta hur du installerar den senaste versionen.
* Aktivera alternativet **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** för den datastream som du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera funktionen för direktuppspelning av media i SDK på webben, så som visas på den här sidan.

Lägg till objektet `configure` när du anropar kommandot `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Egenskap | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| **`channel`** | Sträng | Ja | Namnet på den kanal där direktuppspelad mediainsamling sker. Exempel: `Video channel`. |
| **`playerName`** | Sträng | Ja | Namnet på mediespelaren. |
| **`appVersion`** | Sträng | Nej | Mediespelarprogrammets version. |
| **`mainPingInterval`** | Heltal | Nej | Fästfrekvens för huvudinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `10` och `50` sekunder.  Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](../createmediasession.md#automatic) används. |
| **`adPingInterval`** | Heltal | Nej | Fästfrekvens för annonsinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `1` och `10` sekunder. Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](../createmediasession.md#automatic) används. |

## Direktuppspelad mediekonfiguration med hjälp av taggtillägget Web SDK

De här inställningarna kan konfigureras i taggtillägget för Web SDK med [Konfigurationsinställningar för direktuppspelande media](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
