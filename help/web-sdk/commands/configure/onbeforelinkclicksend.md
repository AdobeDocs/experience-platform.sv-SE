---
title: onBeforeLinkClickSend
description: Återanrop som körs precis innan data för länkspårning skickas.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

The `onBeforeLinkClickSend` Med callback kan du registrera en JavaScript-funktion som kan ändra länkspårningsdata som du skickar precis innan dessa data skickas till Adobe. Med det här återanropet kan du ändra `xdm` eller `data` -objekt, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan. Den stöds i Web SDK 2.15.0 eller senare.

Det här återanropet körs bara när [`clickCollectionEnabled`](clickcollectionenabled.md) är aktiverat. If `clickCollectionEnabled` är inaktiverat, det här återanropet körs inte. Om båda `onBeforeEventSend` och `onBeforeLinkClickSend` innehåller registrerade funktioner, `onBeforeLinkClickSend` funktionen körs först. När `onBeforeLinkClickSend` funktionen är klar, `onBeforeEventSend` funktionen körs sedan.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. Data skickas inte till Adobe.

## Klicka på Skicka återanrop före länken med hjälp av taggtillägget Web SDK

Välj **[!UICONTROL Provide on before link click event send callback code]** knapp när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Med den här kommandoknappen öppnas ett modalt fönster där du kan infoga den önskade koden.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. Markera knappen med etiketten **[!UICONTROL Provide on before link click event send callback code]**.
1. Den här knappen öppnar ett modalt fönster med en kodredigerare. Infoga den önskade koden och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka **[!UICONTROL Save]** publicera ändringarna under tilläggsinställningarna.

I kodredigeraren kan du lägga till, redigera och ta bort element i `content` -objekt. Det här objektet innehåller nyttolasten som skickas till Adobe. Du behöver inte definiera `content` eller kapsla in kod i en funktion. Alla variabler som definierats utanför `content` kan användas, men ingår inte i nyttolasten som skickas till Adobe.

>[!TIP]
>
>Objekten `content.xdm`, `content.data`och `content.clickedElement` definieras alltid i det här sammanhanget, så du behöver inte kontrollera om de finns. Vissa variabler i dessa objekt är beroende av implementeringen och datalagret. Adobe rekommenderar att du kontrollerar om det finns odefinierade värden i dessa objekt för att förhindra JavaScript-fel.

Anta att du vill utföra följande åtgärder:

* Ändra den aktuella sidans URL
* Fånga det klickade elementet i en Adobe Analytics-eVar
* Ändra länktypen från &quot;other&quot; till &quot;download&quot;

Motsvarande kod i det modala fönstret skulle vara följande:

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

Lika med [`onBeforeEventSend`](onbeforeeventsend.md)kan du `return true` för att omedelbart slutföra funktionen, eller `return false` för att omedelbart avbryta sändning av data. Om du avbryter sändningen av data i `onBeforeLinkClickSend` när båda `onBeforeEventSend` och `onBeforeLinkClickSend` innehåller registrerade funktioner, `onBeforeEventSend` funktionen körs inte.

## On before link click send callback using the Web SDK JavaScript library

Registrera `onBeforeLinkClickSend` återanrop när programmet körs `configure` -kommando. Du kan ändra `content` variabelnamn till ett värde som du vill ha genom att ändra parametervariabeln inuti den infogade funktionen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

Du kan också registrera en egen funktion i stället för en infogad funktion.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
