---
title: clickCollectionEnabled
description: Lär dig hur du konfigurerar Web SDK för att kontrollera om länkklicksdata samlas in automatiskt.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# `clickCollectionEnabled`

The `clickCollectionEnabled` egenskapen är ett booleskt värde som avgör om Web SDK automatiskt samlar in länkdata. Om du inte anger den här variabeln är standardvärdet `true` vilket innebär att länkspårningsdata samlas in automatiskt som standard. Anger den här egenskapen till `false` är värdefullt om du föredrar att spåra länkdata manuellt.

När `clickCollectionEnabled` är aktiverat fylls följande XDM-element automatiskt i med data:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interna länkar, nedladdningslänkar och avslutningslänkar spåras automatiskt som standard när det här booleska alternativet är aktiverat. Om du vill ha större kontroll över automatisk länkspårning rekommenderar Adobe att du använder [`clickCollection`](clickcollection.md) -objekt.

## Automatisk länkspårningslogik

Web SDK spårar alla klick på `<a>` och `<area>` HTML-element om det inte har en `onClick` -attribut. Klickningar fångas med en [hämtning](https://www.w3.org/TR/uievents/#capture-phase) klicka på händelseavlyssnaren som är kopplad till dokumentet. När användaren klickar på en giltig länk körs följande logik i rätt ordning:

1. Om länken matchar villkor baserade på värden i [`downloadLinkQualifier`](downloadlinkqualifier.md)eller om länken innehåller en `download` HTML-attribut, `xdm.web.webInteraction.type` är inställd på `"download"` (om `clickCollection.downloadLinkEnabled` är aktiverat).
1. Om länkmåldomänen skiljer sig från den aktuella `window.location.hostname`, `xdm.web.webInteraction.type` är inställd på `"exit"` (om `clickCollection.exitLinkEnabled` är aktiverat).
1. Om länken inte är berättigad till något av `"download"` eller `"exit"`, `xdm.web.webInteraction.type` är inställd på `"other"`.

I samtliga fall `xdm.web.webInteraction.name` är inställt på länktextetiketten och `xdm.web.webInteraction.URL` är inställd på länkens mål-URL. Om du även vill ange länknamnet till URL:en kan du åsidosätta det här XDM-fältet med hjälp av `filterClickDetails` callback i `clickCollection` -objekt.

## Aktivera automatisk länkspårning med taggtillägget Web SDK {#tag-extension}

Välj **[!UICONTROL Enable click data collection]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Aktivera automatisk länkspårning med Web SDK JavaScript-biblioteket {#library}

Ange `clickCollectionEnabled` boolesk när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du föredrar att ange `xdm.web.webInteraction.type` och `xdm.web.webInteraction.value` manuellt.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
