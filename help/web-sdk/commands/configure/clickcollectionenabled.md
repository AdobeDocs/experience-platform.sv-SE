---
title: clickCollectionEnabled
description: Kontrollera om länkklickningsdata samlas in automatiskt.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# `clickCollectionEnabled`

The `clickCollectionEnabled` egenskapen är ett booleskt värde som avgör om Web SDK automatiskt samlar in länkdata. Den här egenskapen är värdefull om du föredrar att spåra länkdata manuellt.

Om det inte är inaktiverat fylls följande XDM-element automatiskt i med data:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## Automatisk länkspårningslogik

Web SDK spårar alla klick på `<a>` och `<area>` HTML-element om det inte har en `onClick` -attribut. Klickningar fångas med en [hämtning](https://www.w3.org/TR/uievents/#capture-phase) klicka på händelseavlyssnaren som är kopplad till dokumentet. När användaren klickar på en giltig länk körs följande logik i rätt ordning:

1. Om länken matchar villkor baserade på värden i [`downloadLinkQualifier`](downloadlinkqualifier.md)eller om länken innehåller en `download` HTML-attribut, `xdm.web.webInteraction.type` är inställd på `"download"`.
1. Om länkmåldomänen skiljer sig från den aktuella `window.location.hostname`, `xdm.web.webInteraction.type` är inställd på `"exit"`.
1. Om länken inte är berättigad till något av `"download"` eller `"exit"`, `xdm.web.webInteraction.type` är inställd på `"other"`.

I samtliga fall `xdm.web.webInteraction.name` är inställt på länktextetiketten och `xdm.web.webInteraction.URL` är inställd på länkens mål-URL. Om du även vill ange länknamnet till URL:en kan du åsidosätta det här XDM-fältet med [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## Aktivera automatisk länkspårning med taggtillägget Web SDK

Välj **[!UICONTROL Enable click data collection]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Aktivera automatisk länkspårning med JavaScript-biblioteket för Web SDK

Ange `clickCollectionEnabled` boolesk när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du föredrar att ange manuellt `xdm.web.webInteraction.type` och `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
