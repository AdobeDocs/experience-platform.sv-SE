---
title: getMediaAnalyticsTracker
description: Lär dig hur du skapar ett spårningsobjekt för medieanalys och använder det för att spåra mediahändelser.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# `getMediaAnalyticsTracker`

Det här Web SDK-kommandot hämtar en Media Analytics-spårare. Du kan använda det här kommandot för att skapa en objektinstans och sedan, med samma API:er som de som finns i [Media JS-biblioteket](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), spåra mediahändelser.

Kommandot `getMediaAnalyticsTracker` returnerar det gamla API:t för medieanalys.

| Metodnamn | Beskrivning | Syntax |
|---|---|---|
| `getInstance` | Skapar en instans av media för att spåra uppspelningssessionen. | `Media.getInstance()` |
| `createMediaObject` | Skapar ett objekt som innehåller medieinformation. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Skapar ett objekt som innehåller adbreak-information. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Skapar ett objekt som innehåller annonsinformation. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Skapar ett objekt som innehåller kapitelinformation. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Skapar ett objekt som innehåller lägesinformation. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createStateObject(name)` |
| `createQoEObject` | Skapar ett objekt som innehåller QoE-information. Returnerar ett tomt objekt om ogiltiga parametrar skickas. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Förekomstmetoder

| Metodnamn | Beskrivning | Syntax |
|---|---|---|
| `trackSessionStart` | Spåra avsikten att starta uppspelningen. Detta startar en spårningssession på mediespårarinstansen. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Spåra uppspelning eller återupptagning av media efter en tidigare paus. | `trackerInstance.trackPlay()` |
| `trackPause` | Spåra mediapaus. | `trackerInstance.trackPause()` |
| `trackComplete` | Spåra media klart. Anropa den här metoden endast när mediet har visats fullständigt. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Spåra slutet av en visningssession. Anropa den här metoden även om användaren inte ser mediet för att slutföra det. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Spåra ett fel som inträffade under medieuppspelning. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Spåra en anpassad händelse. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Uppdatera spelhuvudets position. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Uppdatera upplevelsens kvalitet. | `trackerInstance.updateQoEObject(qoe)` |

## Konstanter

| Konstantnamn | Beskrivning | Värde |
|---|---|---|
| `MediaType` | Medietyp | `Video`, `Audio` |
| `StreamType` | Strömtyp | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Detta definierar standardmetadatanycklarna för videoströmmar | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Detta definierar standardmetadatanycklarna för ljudströmmar. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Detta definierar standardmetadatanycklarna för annonser. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Detta definierar typen av en spårningshändelse. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Detta definierar standardvärden för spårning av spelarstatus. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |

## Hämta spårningsfunktionen för Media Analytics med SDK-taggtillägget för webben

Webbtaggtillägget för SDK är lika med det här kommandot som åtgärden [**[!UICONTROL Get Media Analytics tracker]**](/help/tags/extensions/client/web-sdk/actions/get-media-analytics-tracker.md).
