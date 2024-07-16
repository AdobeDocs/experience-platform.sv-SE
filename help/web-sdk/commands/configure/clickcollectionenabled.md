---
title: clickCollectionEnabled
description: Lär dig hur du konfigurerar Web SDK för att kontrollera om länkklicksdata samlas in automatiskt.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# `clickCollectionEnabled`

Egenskapen `clickCollectionEnabled` är en boolesk egenskap som avgör om Web SDK automatiskt samlar in länkdata. Om du inte anger den här variabeln är standardvärdet `true`, vilket innebär att länkspårningsdata samlas in automatiskt som standard. Det är värdefullt att ange den här egenskapen till `false` om du föredrar att spåra länkdata manuellt.

När `clickCollectionEnabled` är aktiverat fylls följande XDM-element automatiskt i med data:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interna länkar, nedladdningslänkar och avslutningslänkar spåras automatiskt som standard när det här booleska alternativet är aktiverat. Om du vill ha mer kontroll över automatisk länkspårning rekommenderar Adobe att du använder objektet [`clickCollection`](clickcollection.md).

## Automatisk länkspårningslogik

Web SDK spårar alla klick på `<a>`- och `<area>` HTML-element om det inte har något `onClick`-attribut. Klickningar hämtas med en [capture](https://www.w3.org/TR/uievents/#capture-phase)-klickhändelseavlyssnare som är kopplad till dokumentet. När användaren klickar på en giltig länk körs följande logik i rätt ordning:

1. Om länken matchar villkor baserade på värden i [`downloadLinkQualifier`](downloadlinkqualifier.md), eller om länken innehåller ett `download` HTML-attribut, ställs `xdm.web.webInteraction.type` in på `"download"` (om `clickCollection.downloadLinkEnabled` är aktiverat).
1. Om måldomänen för länken skiljer sig från den aktuella `window.location.hostname` anges `xdm.web.webInteraction.type` till `"exit"` (om `clickCollection.exitLinkEnabled` är aktiverat).
1. Om länken inte uppfyller kraven för antingen `"download"` eller `"exit"` ställs `xdm.web.webInteraction.type` in på `"other"`.

I samtliga fall är `xdm.web.webInteraction.name` inställd på länktextetiketten och `xdm.web.webInteraction.URL` är inställd på länkens mål-URL. Om du även vill ange länknamnet till URL:en kan du åsidosätta det här XDM-fältet med hjälp av `filterClickDetails`-återanropet i `clickCollection`-objektet.

## Aktivera automatisk länkspårning med taggtillägget Web SDK {#tag-extension}

Markera kryssrutan **[!UICONTROL Enable click data collection]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Data Collection] och markera kryssrutan **[!UICONTROL Enable click data collection]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Aktivera automatisk länkspårning med Web SDK JavaScript-biblioteket {#library}

Ange det booleska värdet `clickCollectionEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du föredrar att ställa in `xdm.web.webInteraction.type` och `xdm.web.webInteraction.value` manuellt.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
