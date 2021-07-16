---
title: Villkorstyper för webbtillägg
description: Lär dig hur du definierar en biblioteksmodul av typen condition för ett taggtillägg i en webbegenskap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Villkorstyper för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En biblioteksmodul för en villkorstyp har ett mål: utvärdera om något är sant eller falskt. Det som utvärderas är upp till dig.

>[!NOTE]
>
>Det här dokumentet innehåller villkorstyper för webbtillägg. Om du utvecklar ett kanttillägg läser du i guiden för [villkorstyper för kanttillägg](../edge/condition-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i taggtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Om du till exempel vill utvärdera om användaren finns på värden `example.com` kan din modul se ut så här:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Tänk dig en situation där du vill göra värdnamnet konfigurerbart av Adobe Experience Platform-användaren. Du kan tillåta användaren att ange ett värdnamn och sedan spara värdnamnet till inställningsobjektet. Objektet kan se ut ungefär så här:

```js
{
  "hostname": "example.com"
}
```

Om du vill använda det användardefinierade värdnamnet måste modulen ändras till följande:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Sammanhangsberoende händelsedata

Ett andra argument skickas till modulen som innehåller sammanhangsberoende information om händelsen som utlöste regeln. Det kan vara bra i vissa fall och kan nås på följande sätt:

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
