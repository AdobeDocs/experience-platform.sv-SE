---
title: clickCollection
description: Finjustera inställningarna för klicksamlingen.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# `clickCollection`

The `clickCollection` -objektet innehåller flera variabler som hjälper dig att kontrollera automatiskt insamlade länkdata. Använd dessa variabler när du vill ta med eller exkludera typer av länkar från datainsamling.

Den kräver [`clickCollectionEnabled`](clickcollectionenabled.md) som ska aktiveras.

Den stöds i Web SDK 2.25.0 eller senare.

Följande variabler är tillgängliga i `clickCollection` objekt:

* **`clickCollection.internalLinkEnabled`**: Ett booleskt värde som avgör om länkar inom den aktuella domänen spåras automatiskt. Till exempel: `https://example.com/index.html` till `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Ett booleskt värde som avgör om biblioteket spårar länkar som kvalificerar sig som hämtningar baserat på [`downloadLinkQualifier`](downloadlinkqualifier.md) -egenskap.
* **`clickCollection.externalLinkEnabled`**: Ett booleskt värde som avgör om länkar till externa domäner spåras automatiskt. Till exempel: `https://example.com` till `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Ett booleskt värde som avgör om biblioteket väntar till nästa sida för att skicka länkspårningsdata. När nästa sida läses in kombinerar du länkspårningsdata med sidans load-händelse. Om du aktiverar det här alternativet minskas antalet händelser som du skickar till Adobe. If `internalLinkEnabled` är inaktiverat, gör den här variabeln ingenting.
* **`clickCollection.sessionStorageEnabled`**: Ett booleskt värde som avgör om länkspårningsdata lagras i sessionslager i stället för lokala variabler. If `internalLinkEnabled` eller `eventGroupingEnabled` är inaktiverade, gör den här variabeln ingenting.

  Adobe rekommenderar att du aktiverar variabeln när du använder `eventGroupingEnabled`. If `eventGroupingEnabled` är aktiverat när `sessionStorageEnabled` inaktiveras, om du klickar på en ny sida förlorar du länkspårningsdata eftersom de inte bevaras i sessionslagringen. Även om det går att inaktivera `sessionStorageEnabled` i enkelsidiga program är det inte idealiskt för icke-SPA sidor.
* **`filterClickDetails`**: En återanropsfunktion som ger fullständig kontroll över länkspårningsdata som du samlar in. Du kan använda den här återanropsfunktionen för att ändra, dölja eller avbryta sändning av länkspårningsdata. Det här återanropet är användbart när du vill utesluta viss information, t.ex. personligt identifierbar information i länkar.

## Klicka på samlingsinställningarna med tillägget Web SDK-tagg

Välj **[!UICONTROL Enable click data collection]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Om du aktiverar den här kryssrutan visas följande alternativ för klicksamling:

* [!UICONTROL Internal links]
   * [!UICONTROL Enable event grouping]
   * [!UICONTROL Enable session storage]
* [!UICONTROL External links]
* [!UICONTROL Download links]
* [!UICONTROL Filter click properties]

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. Välj önskade inställningar för klicksamlingen.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

The [!UICONTROL Filter click properties] callback-funktionen öppnar en anpassad kodredigerare där du kan infoga önskad kod. I kodredigeraren har du tillgång till följande variabler:

* **`content.clickedElement`**: Det DOM-element som du klickade på.
* **`content.pageName`**: Sidnamnet när klickningen inträffade.
* **`content.linkName`**: Namnet på den klickade länken.
* **`content.linkRegion`**: Området där länken klickades.
* **`content.linkType`**: Typ av länk (avsluta, ladda ned eller annat).
* **`content.linkURL`**: Mål-URL:en för den klickade länken.
* **`return true`**: Avsluta återanropet omedelbart med de aktuella variabelvärdena.
* **`return false`**: Avsluta omedelbart återanropet och avbryt datainsamlingen.

Alla variabler som definierats utanför `content` kan användas, men ingår inte i nyttolasten som skickas till Adobe.

## Klicka på samlingsinställningarna med Web SDK JavaScript-biblioteket

Ange önskade variabler i `clickCollection` -objektet när [`configure`](overview.md) -kommando. Om den inte anges beror standardinställningarna för det här objektet på värdet för [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: Matchar `clickCollectionEnabled`
* `downloadLinkEnabled`: Matchar `clickCollectionEnabled`
* `externalLinkEnabled`: Matchar `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardvärdet är `false`; måste vara explicit aktiverat
* `sessionStorageEnabled`: Standardvärdet är `false`; måste vara explicit aktiverat
* `filterClickDetails`: Innehåller ingen funktion; måste registreras explicit

>[!TIP]
>Adobe rekommenderar att du aktiverar `eventGroupingEnabled`, eftersom det minskar antalet händelser som räknas in i avtalsanvändningen.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
