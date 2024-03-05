---
title: onBeforeEventSend
description: Återanrop som körs precis innan data skickas.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# `onBeforeEventSend`

The `onBeforeEventSend` Med callback kan du registrera en JavaScript-funktion som kan ändra de data du skickar precis innan dessa data skickas till Adobe. Med det här återanropet kan du ändra `xdm` eller `data` -objekt, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. Data skickas inte till Adobe.

## On before event send callback using the Web SDK tag extension

Välj **[!UICONTROL Provide on before event send callback code]** knapp när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Med den här kommandoknappen öppnas ett modalt fönster där du kan infoga den önskade koden.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du knappen **[!UICONTROL Provide on before event send callback code]**.
1. Den här knappen öppnar ett modalt fönster med en kodredigerare. Infoga den önskade koden och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka **[!UICONTROL Save]** publicera ändringarna under tilläggsinställningarna.

I kodredigeraren kan du lägga till, redigera och ta bort element i `content` -objekt. Det här objektet innehåller nyttolasten som skickas till Adobe. Du behöver inte definiera `content` eller kapsla in kod i en funktion. Alla variabler som definierats utanför `content` kan användas, men ingår inte i nyttolasten som skickas till Adobe.

>[!TIP]
>
>Objekten `content.xdm` och `content.data` definieras alltid i det här sammanhanget, så du behöver inte kontrollera om de finns. Vissa variabler i dessa objekt är beroende av implementeringen och datalagret. Adobe rekommenderar att du kontrollerar om det finns odefinierade värden i dessa objekt för att förhindra JavaScript-fel.

Om du till exempel vill:

* Lägg till XDM-elementet `xdm.commerce.order.purchaseID`
* Tvinga alla tecken i `xdm.marketing.trackingCode` till gemener
* Ta bort `xdm.environment.operatingSystemVersion`
* Om en händelsetyp är en länkklickning skickar du data omedelbart oavsett koden nedan
* Avbryt sändning av data till Adobe om en robot upptäcks

Motsvarande kod i det modala fönstret skulle vara följande:

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

>[!NOTE]
>
>Undvik att returnera `false` på den första händelsen på en sida. Returnerar `false` den första händelsen kan påverka personaliseringen negativt.

## On before event send callback using the Web SDK JavaScript library

Registrera `onBeforeEventSend` återanrop när programmet körs `configure` -kommando. Du kan ändra `content` variabelnamn till ett värde som du vill ha genom att ändra parametervariabeln inuti den infogade funktionen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
