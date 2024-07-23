---
title: onBeforeEventSend
description: Lär dig hur du konfigurerar Web SDK för att registrera en JavaScript-funktion som kan ändra data som du skickar precis innan dessa data skickas till Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# `onBeforeEventSend`

Med `onBeforeEventSend`-återanropet kan du registrera en JavaScript-funktion som kan ändra de data du skickar precis innan dessa data skickas till Adobe. Med det här återanropet kan du ändra objektet `xdm` eller `data`, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. Data skickas inte till Adobe.

## Konfigurera före händelsens sändning av återanrop med hjälp av taggtillägget Web SDK {#tag-extension}

Klicka på knappen **[!UICONTROL Provide on before event send callback code]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Med den här kommandoknappen öppnas ett modalt fönster där du kan infoga den önskade koden.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Data Collection] och markera sedan knappen **[!UICONTROL Provide on before event send callback code]**.
1. Den här knappen öppnar ett modalt fönster med en kodredigerare. Infoga den önskade koden och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka på **[!UICONTROL Save]** under tilläggsinställningarna och publicera sedan ändringarna.

I kodredigeraren har du tillgång till följande variabler:

* **`content.xdm`**: [XDM](../sendevent/xdm.md)-nyttolasten för händelsen.
* **`content.data`**: [data](../sendevent/data.md)-objektnyttolasten för händelsen.
* **`return true`**: Avsluta återanropet omedelbart och skicka data till Adobe med de aktuella värdena i `content` -objektet.
* **`return false`**: Avsluta återanropet omedelbart och avbryt överföringen av data till Adobe.

Alla variabler som definierats utanför `content` kan användas, men inkluderas inte i nyttolasten som skickas till Adobe.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Undvik att returnera `false` vid den första händelsen på en sida. Om `false` returneras för den första händelsen kan personaliseringen påverkas negativt.

## Konfigurera på före händelsemeddelande av återanrop med Web SDK JavaScript-biblioteket {#library}

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
