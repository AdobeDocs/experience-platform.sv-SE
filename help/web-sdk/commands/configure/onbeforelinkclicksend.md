---
title: onBeforeLinkClickSend
description: Återanrop som körs precis innan data för länkspårning skickas.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Det här återanropet är föråldrat. Använd [`filterClickDetails`](clickcollection.md) i stället.

The `onBeforeLinkClickSend` Med callback kan du registrera en JavaScript-funktion som kan ändra länkspårningsdata som du skickar precis innan dessa data skickas till Adobe. Med det här återanropet kan du ändra `xdm` eller `data` -objekt, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan. Den stöds i Web SDK 2.15.0 eller senare.

Det här återanropet körs bara när [`clickCollectionEnabled`](clickcollectionenabled.md) är aktiverat och [`filterClickDetails`](clickcollection.md) innehåller ingen registrerad funktion. If `clickCollectionEnabled` är inaktiverat, eller om `filterClickDetails` innehåller en registrerad funktion, kommer denna återanrop inte att köras. If `onBeforeEventSend` och `onBeforeLinkClickSend` båda innehåller registrerade funktioner, `onBeforeLinkClickSend` körs först.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. Data skickas inte till Adobe.

## Konfigurera före länk genom att klicka på Skicka återanrop med tillägget Web SDK-tagg {#tag-extension}

Välj **[!UICONTROL Provide on before link click event send callback code]** knapp när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Med den här kommandoknappen öppnas ett modalt fönster där du kan infoga den önskade koden.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. Markera knappen med etiketten **[!UICONTROL Provide on before link click event send callback code]**.
1. Den här knappen öppnar ett modalt fönster med en kodredigerare. Infoga den önskade koden och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka **[!UICONTROL Save]** publicera ändringarna under tilläggsinställningarna.

I kodredigeraren har du tillgång till följande variabler:

* **`content.clickedElement`**: Det DOM-element som du klickade på.
* **`content.xdm`**: XDM-nyttolasten för händelsen.
* **`content.data`**: Dataobjektets nyttolast för händelsen.
* **`return true`**: Avsluta återanropet omedelbart med de aktuella variabelvärdena. The `onBeforeEventSend` callback-funktionen körs om den innehåller en registrerad funktion.
* **`return false`**: Avsluta omedelbart återanropet och avbryt överföringen av data till Adobe. The `onBeforeEventSend` återanrop körs inte.

Alla variabler som definierats utanför `content` kan användas, men ingår inte i nyttolasten som skickas till Adobe.

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

Lika med [`onBeforeEventSend`](onbeforeeventsend.md)kan du `return true` för att slutföra funktionen omedelbart, eller `return false` för att avbryta sändning av data till Adobe. Om du avbryter sändningen av data i `onBeforeLinkClickSend` när båda `onBeforeEventSend` och `onBeforeLinkClickSend` innehåller registrerade funktioner, `onBeforeEventSend` funktionen körs inte.

## Konfigurera före länk genom att klicka på Skicka återanrop med Web SDK JavaScript-biblioteket {#library}

Registrera `onBeforeLinkClickSend` återanrop när programmet körs `configure` -kommando. Du kan ändra `content` variabelnamn till ett värde som du vill ha genom att ändra parametervariabeln inuti den infogade funktionen.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
