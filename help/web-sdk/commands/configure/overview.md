---
title: Konfigurera Adobe Experience Platform Web SDK
description: Använd konfigurationskommandot för att ange nödvändiga inställningar när du använder Web SDK.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# Konfigurera Adobe Experience Platform Web SDK

Konfigurationen för Web SDK görs med `configure` -kommando. Att konfigurera Web SDK är ett viktigt och obligatoriskt steg som måste utföras när biblioteket eller taggtillägget används.

## Konfigurationsinställningar med tillägget Web SDK-tagg

Navigera till [konfigurationssida för taggtillägg](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.

Dessa konfigurationsinställningar ställs in när du använder tillägget för att skicka data till Adobe.

## Konfigurationsinställningar med JavaScript-biblioteket för Web SDK

Kör `configure` -kommando. Det här kommandot krävs innan du kan anropa andra Web SDK-kommandon, som [`sendEvent`](../sendevent/overview.md). Egenskaperna [`edgeConfigId`](edgeconfigid.md) och [`orgId`](orgid.md) krävs. Alla andra egenskaper är valfria, beroende på organisationens implementeringskrav.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
