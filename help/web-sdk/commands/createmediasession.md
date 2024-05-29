---
title: createMediaSession
description: Lär dig hur du konfigurerar Web SDK för att hantera mediesessioner automatiskt
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---


# `createMediaSession`

The `createMediaSession` kommandot ingår i Web SDK `streamingMedia` -komponenten. Du kan använda den här komponenten för att samla in data relaterade till mediesessioner på din webbplats. Se `streamingMedia` [dokumentation](configure/streamingmedia.md) om du vill lära dig hur du konfigurerar den här komponenten.

De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de samlats in kan du skicka dessa data till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview), för att sammanställa mätvärden. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

Du kan skapa mediesessioner i Web SDK på två sätt:

* [Automatiskt spårade mediesessioner](#automatic) tillåta Web SDK att hantera sändning av mediepinghändelser till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Frekvensen för dessa pingar bestäms av konfigurationsinställningarna för [streamingMedia](configure/streamingmedia.md) -komponenten.
* [Manuellt spårade mediesessioner](#manual) ger dig större kontroll över sändning av sessionsping-händelser till [Adobe Analytics per contenuti in streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Dessutom kan du lagra `sessionID` för mediesessioner.

## Skapa en automatiskt spårad mediesession {#automatic}

Om du vill börja spåra en mediesession automatiskt ringer du `createMediaSession` metod med alternativen som beskrivs nedan:

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
| `getPlayerDetails` | Funktion | Ja | En funktion som returnerar spelarinformationen. Den här återanropsfunktionen anropas av Web SDK innan varje mediahändelse för `playerId` tillhandahålls. |
| `xdm.eventType ` | Objekt | Nej | Mediehändelsetypen. Om det inte anges anges detta automatiskt `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Sessionsinformationsobjektet. The `sessionDetails` -objektet ska innehålla egenskaper för sessionsinformation. Se [Media Collection-schema](../../xdm/data-types/media-collection-details.md) mer information. |


## Skapa en manuellt spårad mediesession {#manual}

Om du vill börja spåra en mediesession manuellt anropar du `createMediaSession` metod med alternativen som beskrivs nedan:

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
| `xdm.eventType` | Objekt | Nej | Mediehändelsetypen. Om det inte anges anges det automatiskt `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Sessionsinformationsobjektet. The `sessionDetails` -objektet ska innehålla egenskaper för sessionsinformation. Se [Media Collection-schema](../../xdm/data-types/media-collection-details.md) mer information. |
| `xdm.mediaCollection.playhead` | Heltal | Ja | Aktuellt spelhuvud. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nej | Kvaliteten på upplevelsedatainformationen. Se [Media Collection-schema](../../xdm/data-types/media-collection-details.md) mer information. |
