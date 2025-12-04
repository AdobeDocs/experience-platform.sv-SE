---
title: Konfigurationsinställningar för datainsamling
description: Konfigurera datainsamlingsinställningar i Web SDK-taggtillägget.
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Konfigurationsinställningar för datainsamling

I det här konfigurationsavsnittet kan du bestämma hur data samlas in över tillägget.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Data collection]**.

![Bild som visar datainsamlingsinställningarna för SDK-taggtillägget för webben i användargränssnittet för taggar.](../assets/web-sdk-ext-collection.png)

Följande alternativ är tillgängliga:

## [!UICONTROL On before event send callback]

En callback-funktion som utvärderar och ändrar nyttolasten som skickas till Adobe. I kodredigeraren har du tillgång till följande variabler:

* **`content.xdm`**: XDM-nyttolasten för händelsen.
* **`content.data`**: Dataobjektets nyttolast för händelsen.
* **`return true`**: Avsluta återanropet omedelbart och skicka data till Adobe med de aktuella värdena i `content` -objektet.
* **`return false`**: Avsluta återanropet omedelbart och avbryt överföringen av data till Adobe.

Alla variabler som definierats utanför `content` kan användas, men inkluderas inte i nyttolasten som skickas till Adobe.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. **Data skickas inte till Adobe.**

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

Det här återanropet motsvarar taggen [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) i JavaScript-biblioteket.

## [!UICONTROL Collect internal link clicks]

En kryssruta som aktiverar insamling av länkspårningsdata internt till din webbplats eller egenskap. Den här kryssrutan motsvarar taggen [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) i JavaScript-biblioteket. När du markerar den här kryssrutan visas alternativ för händelsegruppering:

* **[!UICONTROL No event grouping]**: Länkspårningsdata skickas till Adobe i olika händelser. Länkklickningar som skickas i olika händelser kan öka den avtalsenliga användningen av data som skickas till Adobe Experience Platform.
* **[!UICONTROL Event grouping using session storage]**: Lagra länkspårningsdata i sessionslager fram till nästa sidvyhändelse. Vid nästa händelse som betraktas som en&quot;sidvy&quot; sammanfogas data för den lagrade länkspårningen med händelsenyttolasten&quot;sidvy&quot;. Adobe rekommenderar att den här inställningen aktiveras när interna länkar spåras.
* **[!UICONTROL Event grouping using local object]**: Lagra länkspårningsdata i ett lokalt objekt fram till nästa sidvyhändelse. Om en besökare navigerar till en ny webbläsarsida förloras länkspårningsdata. Den här inställningen är mest användbar för enkelsidiga program.

Taggbiblioteket hanterar en viss händelse som en&quot;sidvy&quot; när följande element ingår i nyttolasten:

* `xdm.web.webPageDetails.name` innehåller ett strängvärde
* `xdm.web.webPageDetails.pageViews.value` är större än `0`

## [!UICONTROL Collect external link clicks]

En kryssruta som aktiverar samlingen av externa länkar. Den här kryssrutan motsvarar taggen [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) i JavaScript-biblioteket.

## [!UICONTROL Collect download link clicks]

En kryssruta som aktiverar samlingen med nedladdningslänkar. Den här kryssrutan motsvarar taggen [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) i JavaScript-biblioteket.

## [!UICONTROL Download link qualifier]

Ett reguljärt uttryck som kvalificerar en länk-URL som en nedladdningslänk. Den här strängen motsvarar taggen [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) i JavaScript-biblioteket.

## [!UICONTROL Filter click properties]

En callback-funktion som utvärderar och ändrar klickrelaterade egenskaper före samlingen. Den här funktionen körs före [!UICONTROL On before event send callback] och är taggen som motsvarar [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) i JavaScript-biblioteket. I kodredigeraren har du tillgång till följande variabler:

* **`content.clickedElement`**: DOM-elementet som klickades på.
* **`content.pageName`**: Sidnamnet när klickningen inträffade.
* **`content.linkName`**: Namnet på den klickade länken.
* **`content.linkRegion`**: Området för den klickade länken.
* **`content.linkType`**: Typ av länk (avsluta, hämta eller annat).
* **`content.linkURL`**: Den klickade länkens mål-URL.
* **`return true`**: Avsluta återanropet omedelbart med de aktuella variabelvärdena.
* **`return false`**: Avsluta återanropet omedelbart och avbryt datainsamlingen.
* Alla variabler som definierats utanför `content` kan användas, men inkluderas inte i nyttolasten som skickas till Adobe.

>[!TIP]
>
>Fältet **[!UICONTROL On before link click send]** är ett föråldrat återanrop som bara är synligt för egenskaper som redan har det konfigurerat. Det är taggen som motsvarar [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) i JavaScript-biblioteket. Använd motringningen **[!UICONTROL Filter click properties]** för att filtrera eller justera klickdata, eller använd **[!UICONTROL On before event send callback]** för att filtrera eller justera den totala nyttolasten som skickas till Adobe. Om både **[!UICONTROL Filter click properties]**-återanropet och **[!UICONTROL On before link click send]**-återanropet är inställda körs bara **[!UICONTROL Filter click properties]**-återanropet.

## Kontextinställningar

Samla in besöksinformation automatiskt, vilket fyller i specifika XDM-fält åt dig. Välj **[!UICONTROL All default context information]** eller **[!UICONTROL Specific context information]**. Det är taggen som motsvarar [`context`](/help/collection/js/commands/configure/context.md) i JavaScript-biblioteket.

* **[!UICONTROL Web]**: Samlar in information om den aktuella sidan.
* **[!UICONTROL Device]**: Samlar in information om användarens enhet.
* **[!UICONTROL Environment]**: Samlar in information om användarens webbläsare.
* **[!UICONTROL Place context]**: Samlar in information om användarens plats.
* **[!UICONTROL High entropy user-agent hints]**: Samlar in mer detaljerad information om användarens enhet.
