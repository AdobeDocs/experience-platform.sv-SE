---
title: Åtgärdstyper för webbtillägg
description: Lär dig hur du definierar en biblioteksmodul av åtgärdstyp för ett taggtillägg i en webbegenskap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Åtgärdstyper för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En biblioteksmodul för en åtgärdstyp är avsedd att utföra en fördefinierad åtgärd. Det är helt och hållet upp till dig. Vill du skicka en aviseringssignal, visa ett erbjudande, tacka användaren för att han/hon besöker dig, spara en cookie eller öppna en supportchatt?

>[!IMPORTANT]
>
>Det här dokumentet innehåller åtgärdstyper för webbtillägg. Om du utvecklar ett kanttillägg läser du i guiden för [åtgärdstyper för kanttillägg](../edge/action-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i taggtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Om du till exempel vill göra meddelandet konfigurerbart av Adobe Experience Platform-användaren kan du tillåta att användaren skriver in och sparar ett meddelande i inställningsobjektet. Objektet ser ut ungefär så här:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Om du vill använda det användardefinierade meddelandet måste modulen ändras till följande:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Sammanhangsberoende händelsedata

Ett andra argument måste sedan skickas till modulen som innehåller kontextinformation om händelsen som utlöser regeln. Det kan vara bra i vissa fall och kan nås på följande sätt:

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
