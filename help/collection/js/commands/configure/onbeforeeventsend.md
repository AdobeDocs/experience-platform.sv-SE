---
title: onBeforeEventSend
description: Lär dig hur du konfigurerar Web SDK för att registrera en JavaScript-funktion som kan ändra de data du skickar precis innan dessa data skickas till Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

Med `onBeforeEventSend`-återanropet kan du registrera en JavaScript-funktion som kan ändra de data du skickar precis innan dessa data skickas till Adobe. Med det här återanropet kan du ändra objektet `xdm` eller `data`, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen och **data skickas inte till Adobe.**

Registrera `onBeforeEventSend`-återanropet när du kör kommandot `configure`. Du kan ändra variabelnamnet `content` till vilket värde som helst genom att ändra parametervariabeln inuti den infogade funktionen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

Du kan också registrera en egen funktion i stället för en infogad funktion.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## Konfigurera före händelsens sändning av återanrop med hjälp av taggtillägget Web SDK

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med hjälp av [konfigurationsinställningarna för datainsamling](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback).
