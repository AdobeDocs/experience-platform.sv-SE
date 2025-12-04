---
title: clickCollection
description: Finjustera inställningarna för klicksamlingen.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

Objektet `clickCollection` innehåller flera variabler som hjälper dig att kontrollera automatiskt insamlade länkdata. Använd dessa variabler när du vill ta med eller exkludera typer av länkar från datainsamling. Det stöds i Web SDK version 2.25.0 eller senare.

Den här variabeln kräver allt av följande:

* [`clickCollectionEnabled`](clickcollectionenabled.md) måste aktiveras.
* Om du använder `clickCollection.filterClickDetails` måste den borttagna metoden [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) vara tom.
* Händelsens nyttolast måste innehålla ett värde i `xdm.web.webPageDetails.name` vid något tillfälle under besökarens besök.

Om implementeringen inte uppfyller alla ovanstående krav gör det här objektet ingenting.

Följande egenskaper är tillgängliga i objektet `clickCollection`:

| Egenskap | Typ | Beskrivning |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Avgör om länkar inom den aktuella domänen spåras automatiskt. `https://example.com/index.html` till `https://example.com/product.html` skulle till exempel betraktas som en intern länk. |
| **`downloadLinkEnabled`** | `boolean` | Avgör om biblioteket spårar länkar som kvalificerar sig som hämtningar baserat på egenskapen [`downloadLinkQualifier`](downloadlinkqualifier.md). |
| **`externalLinkEnabled`** | `boolean` | Avgör om länkar till externa domäner spåras automatiskt. `https://example.com` till `https://example.net` skulle till exempel betraktas som en extern länk. |
| **`eventGroupingEnabled`** | `boolean` | Avgör om biblioteket väntar till nästa sidvyhändelse för att skicka länkspårningsdata. Biblioteket hanterar en händelse som en&quot;sidvy&quot; när följande element ingår i nyttolasten:<ul><li>`xdm.web.webPageDetails.name` innehåller ett strängvärde</li><li>`xdm.web.webPageDetails.pageViews.value` är större än `0`</li></ul>När händelsen&quot;sidvy&quot; läses in kombinerar biblioteket lagrade länkspårningsdata med resten av data i händelsen. Om du aktiverar det här alternativet minskas det totala antalet händelser som du skickar till Adobe. Om `internalLinkEnabled` är inaktiverat händer ingenting. |
| **`sessionStorageEnabled`** | `boolean` | Avgör om länkspårningsdata lagras i sessionslager i stället för lokala variabler. Om `internalLinkEnabled` eller `eventGroupingEnabled` är inaktiverade händer ingenting.<br>Adobe rekommenderar att du aktiverar den här variabeln när du använder `eventGroupingEnabled` utanför enkelsidiga program. Om `eventGroupingEnabled` är aktiverat när `sessionStorageEnabled` är inaktiverat och du klickar på en ny sida, försvinner länkspårningsdata eftersom de inte bevaras i sessionslagringen. Eftersom enkelsidiga program vanligtvis inte navigerar till en ny sida krävs inte sessionslagring för SPA-sidor. |
| **`filterClickDetails`** | `function` | En återanropsfunktion som ger fullständig kontroll över länkspårningsdata som du samlar in. Du kan använda den här återanropsfunktionen för att ändra, dölja eller avbryta sändning av länkspårningsdata. Det här återanropet är användbart när du vill utesluta viss information, t.ex. personligt identifierbar information i länkar. |

Om du inte anger det här objektet i kommandot [`configure`](overview.md) beror standardinställningarna för det här objektet på värdet [`clickCollectionEnabled`](clickcollectionenabled.md):

* `internalLinkEnabled`: Matchar `clickCollectionEnabled`
* `downloadLinkEnabled`: Matchar `clickCollectionEnabled`
* `externalLinkEnabled`: Matchar `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardvärdet är `false`; måste aktiveras explicit
* `sessionStorageEnabled`: Standardvärdet är `false`; måste aktiveras explicit
* `filterClickDetails`: Innehåller ingen funktion; måste registreras explicit

>[!TIP]
>
>Adobe rekommenderar att du aktiverar `eventGroupingEnabled` när `internalLinkEnabled` är aktiverat eftersom det minskar antalet händelser som räknas in i den avtalsenliga användningen.

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

## Konfigurera klicksamling för SDK-taggtillägg för webben

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med hjälp av [konfigurationsinställningarna för datainsamling](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
