---
title: Vyn Tilläggsversioner
description: Den här guiden innehåller detaljerad information om vyn Tillägg och versioner i Adobe Experience Platform Assurance.
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Vyn Tilläggsversioner

I vyn Tilläggsversion kan du snabbt beställa och visa vilka Adobe Experience Platform-mobiltillägg du har installerat och om de är uppdaterade i en klient som är ansluten till en Assurance-session.

## Kom igång med vyerna för tilläggsversioner

När [du har konfigurerat Assurance](../tutorials/implement-assurance.md) väljer du **[!UICONTROL Extension Versions]** i vyn **Hem**

![Tilläggsversioner](./images/versions/versions-extension.png)

## Kontrollera om din version är uppdaterad

I den här vyn visar en tabell både den senaste versionen av varje Mobile SDK samt den aktuella versionen som du har installerat, om tillämpligt. När en version är synkroniserad med den senaste versionen visas ett grönt märke för den installerade versionen. Annars visas emblemet i rött.

![Jämförelse av tilläggsversioner](./images/versions/versions-extension-version.png)

## Exportera versioner

I vyns övre högra hörn kan du välja **[!UICONTROL Export Versions]** som ger dig en JSON-nyttolast med all tilläggsinformation samt den plattform som används av klienten. Du kan välja att exportera dessa data till en JSON-fil eller kopiera dem till Urklipp.

![Export av tilläggsversioner](./images/versions/versions-extension-export.png)
