---
title: Villkorstyper för webbtillägg
description: Lär dig hur du definierar en biblioteksmodul av typen condition för ett taggtillägg i en webbegenskap.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Villkorstyper för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

I en regel utvärderas ett villkor efter att en händelse har inträffat. Alla villkor måste returnera true för att regeln ska kunna fortsätta bearbetningen. Undantaget är när användare uttryckligen placerar villkor i en&quot;undantagsbucket&quot;, vilket innebär att alla villkor i bucket måste returnera false för att regeln ska fortsätta bearbetningen.

Ett tillägg kan till exempel innehålla villkorstypen &quot;viewport contains&quot;, där användaren kan ange en CSS-väljare. När villkoret utvärderas på klientens webbplats kan tillägget hitta element som matchar CSS-väljaren och returnera om något av dem finns i användarens visningsruta.

I det här dokumentet beskrivs hur du definierar villkorstyper för ett webbtillägg i Adobe Experience Platform.

>[!NOTE]
>
>Om du utvecklar ett kanttillägg läser du i handboken [villkorstyper för kanttillägg](../edge/condition-types.md) i stället.
>
>I det här dokumentet förutsätts det att du känner till biblioteksmoduler och hur de är integrerade i webbtillägg. Om du behöver en introduktion kan du se översikten på [formatering av biblioteksmodul](./format.md) innan du återgår till den här guiden.

Villkorstyperna består vanligtvis av följande:

1. A [visa](./views.md) som visas i användargränssnittet för Experience Platform och datainsamling där användare kan ändra inställningarna för villkoret.
2. En biblioteksmodul som skickas inom taggens körningsbibliotek för att tolka inställningarna och utvärdera ett villkor.

En biblioteksmodul av typen condition har ett mål: utvärdera om något är sant eller falskt. Det som utvärderas är upp till dig.

Om du till exempel vill utvärdera om användaren finns på värden `example.com`kan din modul se ut så här:

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

The `event` -objektet måste innehålla följande egenskaper:

| Egenskap | Beskrivning |
| --- | --- |
| `$type` | En sträng som beskriver tilläggets namn och händelsenamn, som förenas med en punkt. Exempel, `youtube.play`. |
| `$rule` | Ett objekt som innehåller information om den regel som körs. Objektet måste innehålla följande underegenskaper:<ul><li>`id`: ID:t för den regel som körs.</li><li>`name`: Namnet på den regel som körs.</li></ul> |

Tillägget som anger händelsetypen som utlöste regeln kan eventuellt lägga till annan användbar information till den här `event` -objekt.
