---
title: Händelsetyper för webbtillägg
description: Lär dig hur du definierar en biblioteksmodul av händelsetyp för ett webbtillägg i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---

# Händelsetyper för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

I en taggregel är en händelse en aktivitet som måste inträffa för att en regel ska kunna utlösas. Ett webbtillägg kan till exempel innehålla en händelsetyp av typen&quot;gest&quot; som letar efter en viss mus- eller pekgest. När gesten är klar utlöses regeln av händelselogiken.

En biblioteksmodul för en händelsetyp är utformad för att identifiera när en aktivitet inträffar och sedan anropa en funktion för att utlösa en associerad regel. Händelsen som identifieras kan anpassas. Kan till exempel identifiera när en användare gör en viss gest, rullar snabbt eller interagerar med något.

Det här dokumentet beskriver hur du definierar händelsetyper för ett webbtillägg i Adobe Experience Platform.

>[!NOTE]
>
>I det här dokumentet förutsätts det att du känner till biblioteksmoduler och hur de är integrerade i webbtillägg. I översikten [biblioteksmodulens formatering](./format.md) finns en introduktion till implementeringen innan du återgår till den här guiden.

Händelsetyper definieras av tillägg och består vanligtvis av följande:

1. En [vy](./views.md) i användargränssnittet för datainsamling som gör att användare kan ändra inställningar för händelsen.
2. En biblioteksmodul som skickas inom taggens körningsbibliotek för att tolka inställningarna och för att bevaka att en viss aktivitet inträffar.

`module.exports` acceptera både  `settings` och  `trigger` parametrar. Detta gör att händelsetypen kan anpassas.

```js
module.exports = function(settings, trigger) { … };
```

| Parameter | Beskrivning |
| --- | --- |
| `settings` | Ett objekt som innehåller inställningar som användaren har konfigurerat i händelsetypens vy. Du har fullständig kontroll över vad som hamnar i det här objektet. |
| `trigger` | En funktion som modulen ska anropa när regeln ska aktiveras. Det finns en 1:1-relation mellan ett `settings`-objekt, en `trigger`-funktion och en regel. Det innebär att den utlösarfunktion som du fick för en regel inte kan användas för att utlösa en annan regel. |

>[!NOTE]
>
>Den exporterade funktionen anropas en gång för varje regel som har konfigurerats att använda din händelsetyp.

Om du använder aktiviteten på fem sekunder som ett exempel, har aktiviteten utförts efter fem sekunder och regeln utlöses. Modulen ser ut ungefär som i det här exemplet.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Om du vill att längden ska kunna konfigureras av Adobe Experience Platform-användaren måste du ange och spara en varaktighet för inställningsobjektet. Objektet kan se ut ungefär så här:

```js
{
  "duration": 25000
}
```

För att använda den användardefinierade varaktigheten måste modulen uppdateras för att inkludera den.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Skicka kontextuella händelsedata

När en regel aktiveras är det ofta användbart att ge mer information om händelsen som inträffade. Användare som skapar regler kan finna att den här informationen är användbar för att uppnå ett visst beteende. Om en marknadsförare till exempel vill skapa en regel där en analysfyr skickas varje gång användaren sveper över skärmen. Tillägget måste tillhandahålla en `swipe`-händelsetyp så att markören kan använda den här händelsetypen för att utlösa rätt regel. Om man utgår ifrån att marknadsföraren vill inkludera den vinkel som svepen inträffade i beacon, skulle detta vara svårt att göra utan att lämna ytterligare information. Om du vill ange ytterligare information om händelsen som inträffade skickar du ett objekt när du anropar funktionen `trigger`. Exempel:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Marknadsföraren kan sedan använda det här värdet på en analysfyr genom att ange värdet `%event.swipeAngle%` i ett textfält. De kan även komma åt `event.swipeAngle` inifrån andra sammanhang (som en anpassad kodsåtgärd). Det går att inkludera andra typer av valfri händelseinformation som kan vara användbar för en marknadsförare på samma sätt.

### [!DNL nativeEvent]

Om din händelsetyp baseras på en systemspecifik händelse (om tillägget till exempel har en `click`-händelsetyp) rekommenderar vi att du ställer in egenskapen `nativeEvent` enligt följande.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Detta kan vara användbart för marknadsförare som försöker komma åt information från den inbyggda händelsen, som markörkoordinater.

### [!DNL element]

Om det finns en stark relation mellan ett element och händelsen som inträffade bör du ställa in egenskapen `element` på elementets DOM-nod. Om tillägget till exempel har händelsetypen `click` och du tillåter marknadsförare att konfigurera den så att regeln bara aktiveras om ett element med ID:t `herobanner` har valts. Om användaren i det här fallet väljer en hjältebanderoll bör du anropa `trigger` och ställa in `element` på hjältebanderollens DOM-nod.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Regelordningen följs

Taggar gör att användarna kan beställa regler. En användare kan till exempel skapa två regler som både använder händelsetypen orientation-change och för att anpassa den ordning i vilken reglerna ska köras. Anta att Adobe Experience Platform-användaren anger ordningsvärdet `2` för orienteringsändringshändelsen i regel A och ordningsvärdet `1` för orienteringsändringshändelsen i regel B. Detta anger att när orienteringen ändras på en mobil enhet ska regel B utlösas före regel A (regler med lägre ordningsvärden utlöses först).

Som vi nämnt tidigare anropas den exporterade funktionen i vår händelsemodul en gång för varje regel som har konfigurerats att använda vår händelsetyp. Varje gång den exporterade funktionen anropas skickas en unik `trigger`-funktion som är kopplad till en viss regel. I det scenario som beskrivs ovan anropas den exporterade funktionen en gång med en `trigger`-funktion som är kopplad till regel B och sedan en gång till med en `trigger`-funktion som är kopplad till regel A. Regel B kommer först eftersom användaren har gett den ett lägre ordningsvärde än regel A. När vår biblioteksmodul upptäcker en orienteringsändring är det viktigt att vi anropar `trigger`-funktionerna i samma ordning som de angavs i biblioteksmodulen.

Observera, i exempelkoden nedan, att när en orienteringsändring identifieras anropas utlösarfunktioner i samma ordning som de angavs för den exporterade funktionen:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Detta säkerställer att den användarspecificerade ordern upprätthålls.

En felaktig implementering skulle vara en implementering som anropar utlösarfunktionerna i en annan ordning:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Naturliga programmeringsmetoder har vanligtvis en korrekt ordning, men det är viktigt att du är medveten om konsekvenserna och utvecklas i enlighet med detta.
