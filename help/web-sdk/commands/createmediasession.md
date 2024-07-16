---
title: createMediaSession
description: Lär dig hur du konfigurerar Web SDK för att hantera mediesessioner automatiskt
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---

# `createMediaSession`

Kommandot `createMediaSession` är en del av Web SDK `streamingMedia` -komponenten. Du kan använda den här komponenten för att samla in data relaterade till mediesessioner på din webbplats. Mer information om hur du konfigurerar den här komponenten finns i `streamingMedia` [documentation](configure/streamingmedia.md).

De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de har samlats in kan du skicka dessa data till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview) för att samla in mätvärden. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

Du kan skapa mediesessioner i Web SDK på två sätt:

* [Automatiskt spårade mediesessioner](#automatic) gör att Web SDK kan hantera sändning av mediaspingshändelser till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Frekvensen för dessa pingar bestäms av konfigurationsinställningarna för komponenten [streamingMedia](configure/streamingmedia.md).
* [Manuellt spårade mediesessioner](#manual) ger dig större kontroll över sändningen av sessionsping-händelser till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Dessutom kan du lagra `sessionID` för mediesessioner.

## Skapa en automatiskt spårad mediesession {#automatic}

Om du vill börja spåra en mediesession automatiskt anropar du metoden `createMediaSession` med alternativen som beskrivs nedan:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Egenskap | Typ | Obligatoriskt | Beskrivning |
|---------|----------|---------|---------|
| `playerId` | Sträng | Ja | Spelar-ID, en unik identifierare som representerar mediesessionen. |
| `getPlayerDetails` | Funktion | Ja | En funktion som returnerar spelarinformationen. Den här återanropsfunktionen anropas av Web SDK innan varje mediahändelse för `playerId` som anges. |
| `xdm.eventType ` | Objekt | Nej | Mediehändelsetypen. Om det inte anges ställs den automatiskt in på `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Sessionsinformationsobjektet. Objektet `sessionDetails` ska innehålla egenskaper för sessionsinformation. Mer information finns i dokumentationen för [Media Collection-schemat](../../xdm/data-types/media-collection-details.md). |


## Skapa en manuellt spårad mediesession {#manual}

Om du vill börja spåra en mediesession manuellt anropar du metoden `createMediaSession` med alternativen som beskrivs nedan:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Egenskap | Typ | Begärd | Beskrivning |
|---------|----------|---------|---------|
| `xdm.eventType` | Objekt | Nej | Mediehändelsetypen. Om den inte anges anges den automatiskt till `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Sessionsinformationsobjektet. Objektet `sessionDetails` ska innehålla egenskaper för sessionsinformation. Mer information finns i dokumentationen för [Media Collection-schemat](../../xdm/data-types/media-collection-details.md). |
| `xdm.mediaCollection.playhead` | Heltal | Ja | Aktuellt spelhuvud. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nej | Kvaliteten på upplevelsedatainformationen. Mer information finns i dokumentationen för [Media Collection-schemat](../../xdm/data-types/media-collection-details.md). |
