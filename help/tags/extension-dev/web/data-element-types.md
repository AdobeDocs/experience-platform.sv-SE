---
title: Dataelementtyper för webbtillägg
description: Lär dig hur du definierar en biblioteksmodul av typen data-element för ett taggtillägg i en webbegenskap.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Dataelementtyper för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

I datainsamlingstaggar är dataelement i princip alias för datadelar på en sida. Dessa data finns i frågesträngsparametrar, cookies, DOM-element eller andra platser. Ett dataelement kan refereras av regler och fungerar som en abstraktion för att komma åt dessa datadelar.

Dataelementtyperna tillhandahålls via tillägg och gör det möjligt för användare att konfigurera dataelement så att de får tillgång till datadelar på ett visst sätt. Ett tillägg kan t.ex. innehålla ett dataelement av typen&quot;lokal lagringspost&quot;, där användaren kan ange ett lokalt lagringsobjektnamn. När en regel refererar till dataelementet kan tillägget söka efter det lokala lagringsobjektets värde med hjälp av det lokala lagringsobjektets namn som användaren angav när dataelementet konfigurerades.

Det här dokumentet beskriver hur du definierar dataelementtyper för ett webbtillägg i Adobe Experience Platform.

>[!IMPORTANT]
>
>Om du utvecklar ett kanttillägg läser du i guiden för [dataelementtyper för kanttillägg](../edge/data-element-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i webbtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Dataelementtyper består vanligtvis av följande:

1. En [vy](./views.md) i användargränssnittet för datainsamling som gör att användare kan ändra inställningar för dataelementet.
2. En biblioteksmodul som skickas i taggens körningsbibliotek för att tolka inställningarna och hämta data.

Tänk dig en situation där du vill tillåta användare att hämta data från ett lokalt lagringsobjekt med namnet `productName`. Modulen kan se ut så här:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Om du vill att det lokala lagringsobjektets namn ska kunna konfigureras av Adobe Experience Platform-användaren kan du tillåta att användaren anger ett namn och sedan spara namnet i `settings`-objektet. Objektet kan se ut ungefär så här:

```js
{
  itemName: "campaignId"
}
```

Om du vill använda det användardefinierade lokala lagringsobjektnamnet måste modulen ändras till följande:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Stöd för standardvärden

Tänk på att användare kan konfigurera ett standardvärde för valfritt dataelement. Om biblioteksmodulen för dataelement returnerar värdet `undefined` eller `null` ersätts den automatiskt av det standardvärde som användaren har konfigurerat för dataelementet.

## Sammanhangsberoende händelsedata

Om dataelementet hämtas som ett resultat av att en regel aktiveras (dataelement används t.ex. i regelns villkor och åtgärder), skickas ett andra argument till modulen som innehåller sammanhangsberoende information om händelsen som utlöste regeln. Det kan vara bra i vissa fall och kan nås på följande sätt:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

Objektet `event` måste innehålla följande egenskaper:

| Egenskap | Beskrivning |
| --- | --- |
| `$type` | En sträng som beskriver tilläggets namn och händelsenamn, som förenas med en punkt. Exempel, `youtube.play`. |
| `$rule` | Ett objekt som innehåller information om den regel som körs. Objektet måste innehålla följande underegenskaper:<ul><li>`id`: ID:t för den regel som körs.</li><li>`name`: Namnet på den regel som körs.</li></ul> |

Tillägget som innehåller händelsetypen som utlöste regeln kan eventuellt lägga till annan användbar information till det här `event`-objektet.
