---
title: clickCollection
description: Finjustera inställningarna för klicksamlingen.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# `clickCollection`

Objektet `clickCollection` innehåller flera variabler som hjälper dig att kontrollera automatiskt insamlade länkdata. Använd dessa variabler när du vill ta med eller exkludera typer av länkar från datainsamling.

[`clickCollectionEnabled`](clickcollectionenabled.md) måste aktiveras.

Den stöds i Web SDK 2.25.0 eller senare.

Följande variabler är tillgängliga i objektet `clickCollection`:

* **`clickCollection.internalLinkEnabled`**: Ett booleskt värde som avgör om länkar inom den aktuella domänen spåras automatiskt. Till exempel `https://example.com/index.html` till `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Ett booleskt värde som avgör om biblioteket spårar länkar som kvalificeras som hämtningar baserat på egenskapen [`downloadLinkQualifier`](downloadlinkqualifier.md).
* **`clickCollection.externalLinkEnabled`**: Ett booleskt värde som avgör om länkar till externa domäner spåras automatiskt. Till exempel `https://example.com` till `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Ett booleskt värde som avgör om biblioteket väntar till nästa sida för att skicka länkspårningsdata. När nästa sida läses in kombinerar du länkspårningsdata med sidans load-händelse. Om du aktiverar det här alternativet minskas antalet händelser som du skickar till Adobe. Om `internalLinkEnabled` är inaktiverat händer ingenting.
* **`clickCollection.sessionStorageEnabled`**: Ett booleskt värde som avgör om länkspårningsdata lagras i sessionslagring i stället för lokala variabler. Om `internalLinkEnabled` eller `eventGroupingEnabled` är inaktiverade händer ingenting.

  Adobe rekommenderar starkt att du aktiverar den här variabeln när du använder `eventGroupingEnabled` utanför enkelsidiga program. Om `eventGroupingEnabled` är aktiverat när `sessionStorageEnabled` är inaktiverat och du klickar på en ny sida, försvinner länkspårningsdata eftersom de inte bevaras i sessionslagringen. Eftersom enkelsidiga program vanligtvis inte navigerar till en ny sida krävs inte sessionslagring för SPA sidor.
* **`filterClickDetails`**: En återanropsfunktion som ger fullständig kontroll över länkspårningsdata som du samlar in. Du kan använda den här återanropsfunktionen för att ändra, dölja eller avbryta sändning av länkspårningsdata. Det här återanropet är användbart när du vill utesluta viss information, t.ex. personligt identifierbar information i länkar.

## Klicka på samlingsinställningarna med tillägget Web SDK-tagg

Välj något av följande alternativ när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md):

* [!UICONTROL Collect internal links]
   * [!UICONTROL Event grouping options]:
      * [!UICONTROL No event grouping]
      * [!UICONTROL Event grouping using session storage]
      * [!UICONTROL Event grouping using local object]
* [!UICONTROL Collect external links]
* [!UICONTROL Collect download links]
* [!UICONTROL Filter click properties]

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Data Collection] och välj önskade inställningar för klicksamlingen.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

Callback-funktionen [!UICONTROL Filter click properties] öppnar en anpassad kodredigerare där du kan infoga önskad kod. I kodredigeraren har du tillgång till följande variabler:

* **`content.clickedElement`**: DOM-elementet som klickades på.
* **`content.pageName`**: Sidnamnet när klickningen inträffade.
* **`content.linkName`**: Namnet på den klickade länken.
* **`content.linkRegion`**: Området för den klickade länken.
* **`content.linkType`**: Typ av länk (avsluta, hämta eller annat).
* **`content.linkURL`**: Den klickade länkens mål-URL.
* **`return true`**: Avsluta återanropet omedelbart med de aktuella variabelvärdena.
* **`return false`**: Avsluta återanropet omedelbart och avbryt datainsamlingen.

Alla variabler som definierats utanför `content` kan användas, men inkluderas inte i nyttolasten som skickas till Adobe.

## Klicka på samlingsinställningarna med Web SDK JavaScript-biblioteket

Ange önskade variabler i objektet `clickCollection` när du kör kommandot [`configure`](overview.md). Om den inte anges beror standardinställningarna för det här objektet på värdet [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: Matchar `clickCollectionEnabled`
* `downloadLinkEnabled`: Matchar `clickCollectionEnabled`
* `externalLinkEnabled`: Matchar `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardvärdet är `false`; måste aktiveras explicit
* `sessionStorageEnabled`: Standardvärdet är `false`; måste aktiveras explicit
* `filterClickDetails`: Innehåller ingen funktion; måste registreras explicit

>[!TIP]
>Adobe rekommenderar att du aktiverar `eventGroupingEnabled` när `internalLinkEnabled` är aktiverat, eftersom det minskar antalet händelser som räknas in i den avtalsenliga användningen.

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
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
