---
title: clickCollectionEnabled
description: Lär dig hur du konfigurerar Web SDK för att kontrollera om länkklicksdata samlas in automatiskt.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '344'
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

Den här variabeln hanteras automatiskt av taggtillägget. Du behöver inte ange den explicit. Om något av följande väljs när [taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) konfigureras, samlas relevanta länkspårningsdata in:

* [!UICONTROL Collect internal link clicks]
* [!UICONTROL Collect external link clicks]
* [!UICONTROL Collect download link clicks]

Mer information finns i [`clickCollection`](clickcollection.md).

## Aktivera automatisk länkspårning med Web SDK JavaScript-biblioteket {#library}

Ange det booleska värdet `clickCollectionEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du föredrar att ställa in `xdm.web.webInteraction.type` och `xdm.web.webInteraction.value` manuellt.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
