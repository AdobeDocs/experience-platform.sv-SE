---
title: Versionsinformation för Adobe Experience Platform Web SDK
seo-title: Versionsinformation för Adobe Experience Platform Web SDK
description: Versionsinformation för Adobe Experience Platform Web SDK.
seo-description: Versionsinformation för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Versionsinformation

## Version 2.3.0

* Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
* Ytterligare stöd för personalisering för ensidiga applikationer.
* Förbättrad kompatibilitet med annan JavaScript-kod som kan skriva över API: `window.console` er.
* Felkorrigering: `sendBeacon` användes inte när `documentUnloading` var inställt på `true` eller när länkklick spårades automatiskt.
* Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
* Felkorrigering: Vissa webbläsarfel som innehåller en skrivskyddad `message` egenskap hanterades inte på rätt sätt, vilket resulterade i att ett annat fel exponerades för kunden.
* Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0

* Felkorrigering: Opt-in-objektet blockerade Alloy från att ringa anrop när `idMigrationEnabled` är `true`.
* Felkorrigering: Meddela Alloy om det finns förfrågningar om att returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0

* Ta bort `syncIdentity` kommandot och stödet för att skicka dessa ID:n i `sendEvent` kommandot.
* Stöd för IAB 2.0 Consent Standard.
* Stöd för att skicka ytterligare ID:n i `setConsent` kommandot.
* Stöd för att åsidosätta `datasetId` i `sendEvent` kommandot.
* Bildskärmar med stöd för legering ([läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Skicka kontextdata `environment: browser` för implementeringsdetaljer.
