---
title: Versionsinformation för Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versionsinformation;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Versionsinformation

## Version 2.3.0

* Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
* Ytterligare stöd för personalisering för ensidiga applikationer.
* Förbättrad kompatibilitet med annan JavaScript-kod som kan skriva över `window.console` API:er.
* Felkorrigering: `sendBeacon` användes inte när `documentUnloading` var inställt på `true` eller när länkklick spårades automatiskt.
* Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
* Felkorrigering: Vissa webbläsarfel som innehåller en skrivskyddad `message`-egenskap hanterades inte korrekt, vilket resulterade i att ett annat fel exponerades för kunden.
* Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0

* Felkorrigering: Opt-in-objektet blockerade Alloy från att ringa anrop när `idMigrationEnabled` är `true`.
* Felkorrigering: Meddela Alloy om det finns förfrågningar om att returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0

* Ta bort kommandot `syncIdentity` och stöd för att skicka dessa ID:n i kommandot `sendEvent`.
* Stöd för IAB 2.0 Consent Standard.
* Stöd för att skicka ytterligare ID:n i kommandot `setConsent`.
* Stöd för att åsidosätta `datasetId` i kommandot `sendEvent`.
* Bildskärmar för supportallokering ([Läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Skicka `environment: browser` i kontextdata för implementeringsinformation.
