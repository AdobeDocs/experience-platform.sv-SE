---
title: Versionsinformation om Google Data Layer Extension
description: Den senaste versionsinformationen om taggtillägget Google Data Layer i Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: c1bad7d5414e62f4d77f7d5903f4b2bf4d9081f8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Versionsinformation om tillägget Google Data Layer

## Version 1.0.4

* Allmän betaversion av tillägget.

## Version 1.0.6

* Tillägg av åtgärd för att återställa datalagret till det beräknade läget.
* Åtgärda buggar i dataelement som förhindrar hämtning av värden från det beräknade läget.

## Version 1.1.1

En avsevärd förbättring och felkorrigering som är resultatet av betatestningsfeedback.

* Korrigerar ett problem där ett tomt dataelement för Google datalagertillägg som används i en regel som inte är datalager (t.ex. inläst bibliotek) returnerar datalagret, inte det beräknade läget.
* Korrigerar ett problem där datalagrets beräknade tillstånd inte överfördes från hjälpen i händelser vid tidpunkten för händelseutlösandet, utan i stället vid tidpunkten för regelkörningen.
* Lägger till en växlingsknapp i dataelementsdialogrutan där användaren kan välja om endast värden från händelser ska returneras.
* Korrigerar ett problem där händelsehistoriken inte fångades upp korrekt av regelhändelseavlyssnare.
* Förbättrad mindre kodskärpa.

## Version 1.2.0

* Lägger till en åtgärd som ska skickas till datalagret med hjälp av en multifältdialogruta med nyckelvärden.
* Korrigerar ett fel som förhindrar att tillägget läses in när taggar distribueras synkront.
* Korrigerar ett fel som orsakade ett fel när ett dataelement sparades under vissa omständigheter.
* Lägger till dokumentation i händelsedialogrutan som förklarar användningen av händelseobjektet Tags.
* Lägger till en varning om oändliga slingor i händelsedialogrutan.

## Version 1.2.2

* Lägger till stöd för Google Analytics-gtag()-händelser.
