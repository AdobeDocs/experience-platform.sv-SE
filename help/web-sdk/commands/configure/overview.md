---
title: Konfigurera Adobe Experience Platform Web SDK
description: Använd konfigurationskommandot för att ange nödvändiga inställningar när du använder Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Konfigurera Adobe Experience Platform Web SDK

Konfigurationen för Web SDK görs med kommandot `configure`. Att konfigurera Web SDK är ett viktigt och obligatoriskt steg som måste utföras när biblioteket eller taggtillägget används.

## Konfigurera Web SDK med hjälp av taggtillägget {#configure-tag-extension}

Följ stegen nedan för att konfigurera Web SDK via taggtillägget.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Gå till konfigurationssidan för [Web SDK-taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) om du vill ha mer information om alla konfigurationsalternativ.

Dessa konfigurationsinställningar ställs in när du använder tillägget för att skicka data till Adobe.

## Konfigurera Web SDK med JavaScript-biblioteket {#configure-js}

Kör kommandot `configure`. Det här kommandot krävs innan du kan anropa andra Web SDK-kommandon, till exempel [`sendEvent`](../sendevent/overview.md).

Egenskaperna [`datastreamId`](datastreamid.md) och [`orgId`](orgid.md) krävs. Alla andra egenskaper är valfria, beroende på organisationens implementeringskrav.

Innehållsförteckningen i den här användarhandboken innehåller detaljerad information om alla kommandon som stöds.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
