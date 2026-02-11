---
title: clickCollectionEnabled
description: Lär dig hur du konfigurerar Web SDK för att kontrollera om länkklicksdata samlas in automatiskt.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 4d251ff7323e83ac5c47b5817f81e8fde64cb7d9
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `clickCollectionEnabled`

Egenskapen `clickCollectionEnabled` är en boolesk egenskap som avgör om Web SDK automatiskt samlar in länkdata. Om du inte anger den här variabeln är standardvärdet `true`, vilket innebär att länkspårningsdata samlas in automatiskt som standard. Det är värdefullt att ange den här egenskapen till `false` om du föredrar att spåra länkdata manuellt.

När `clickCollectionEnabled` är aktiverat fylls följande XDM-element automatiskt i med data:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interna länkar, nedladdningslänkar och avslutningslänkar spåras automatiskt som standard när det här booleska alternativet är aktiverat. Om du vill ha större kontroll över automatisk länkspårning rekommenderar Adobe att du använder objektet [`clickCollection`](clickcollection.md).

## Automatisk länkspårningslogik

SDK spårar alla klick på `<a>`- och `<area>` HTML-element om det inte har något `onClick`-attribut. Klickningar hämtas med en [capture](https://www.w3.org/TR/uievents/#capture-phase)-klickhändelseavlyssnare som är kopplad till dokumentet. När användaren klickar på en giltig länk körs följande logik i rätt ordning:

1. Om länken matchar villkor baserade på värden i [`downloadLinkQualifier`](downloadlinkqualifier.md), eller om länken innehåller ett `download` HTML-attribut, ställs `xdm.web.webInteraction.type` in på `"download"` (om `clickCollection.downloadLinkEnabled` är aktiverat).
1. Om måldomänen för länken skiljer sig från den aktuella `window.location.hostname` anges `xdm.web.webInteraction.type` till `"exit"` (om `clickCollection.exitLinkEnabled` är aktiverat).
1. Om länken inte uppfyller kraven för antingen `"download"` eller `"exit"` ställs `xdm.web.webInteraction.type` in på `"other"`.

I samtliga fall kontrollerar `xdm.web.webInteraction.name` det element som klickades och dess underordnade för det första icke-tomma värdet i följande ordning:

1. `innerText` (återgår till `textContent`)
1. Sammanfogade `nodeValue` från underordnade textnoder som stöds
1. `alt`-attribut
1. `title`-attribut
1. `<input value="...">`-attribut
1. `<img src="...">`-attribut
1. `aria-label`-attribut
1. `name`-attribut
1. Tom sträng

Fältet `xdm.web.webInteraction.URL` är inställt på länkens mål-URL. Om du även vill ange länknamnet till URL:en kan du åsidosätta det här XDM-fältet med hjälp av `filterClickDetails`-återanropet i `clickCollection`-objektet.

## Implementering

Ange det booleska värdet `clickCollectionEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du föredrar att ställa in `xdm.web.webInteraction.type` och `xdm.web.webInteraction.value` manuellt.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## Stöd för öppna [!DNL Shadow DOM]-element

Webb-SDK har stöd för automatisk klickspårning för länkar inuti **öppna skugg-DOM** -element.

Många moderna webbplatser använder [webbkomponenter](https://developer.mozilla.org/en-US/docs/Web/Web_Components) för att skapa återanvändbara och inkapslade gränssnittselement. De här komponenterna använder ofta en teknik som kallas [**Skugga-DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) för att hålla sin interna struktur och format åtskilda från resten av sidan.

Det finns två typer av skugga-DOM:

* **Öppna skugga-DOM:** Den interna strukturen är tillgänglig för JavaScript som körs på sidan. Andra skript kan interagera med eller inspektera innehållet i komponenten.
* **Stängd skugga-DOM:** Den interna strukturen är dold från JavaScript utanför komponenten, vilket gör den otillgänglig för spårning eller redigering.

SDK spårar automatiskt klickningar på `<a>` och `<area>` element i **öppna skugg-DOM**, precis som för länkar i huvuddokumentet. Den här spårningen ser till att länkklick i webbkomponenter som använder [!DNL Shadow DOM] inkluderas i analysdata. Klickningar i **stängda skugg-DOM:er** spåras inte eftersom deras interna struktur är dold för JavaScript-kod som körs utanför komponenten.

## Aktivera eller inaktivera klicksamling för Web SDK-taggtillägg

Mer information om hur du utför de här åtgärderna med hjälp av taggar finns i [Konfigurationsinställningar för datainsamling](/help/tags/extensions/client/web-sdk/configure/data-collection.md) i dokumentationen för Web SDK-tillägget.
