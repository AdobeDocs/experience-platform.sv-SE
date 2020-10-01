---
title: Versionsinformation för Adobe Experience Platform Web SDK
seo-title: Versionsinformation för Adobe Experience Platform Web SDK
description: Versionsinformation för Adobe Experience Platform Web SDK.
seo-description: Versionsinformation för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 1%

---


# Versionsinformation

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
