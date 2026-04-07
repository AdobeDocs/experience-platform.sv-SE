---
title: subscribeRulesetItems
description: Prenumerera på innehållskort för en viss yta med kommandot subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: 3ecfc2258e63a34a739ab8b296437c357d1dd9d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# `subscribeRulesetItems`

Med kommandot `subscribeRulesetItems` kan du prenumerera på erbjudanden som är resultatet av färdiga regeluppsättningar. Du kan göra detta genom att ange vilka ytor och scheman som ska filtreras efter och tillhandahålla en callback-funktion.

Regler utvärderas varje gång ett [`sendEvent`](sendevent/overview.md)-kommando skickas. Callback-funktionen tar emot ett `result`-objekt med en array med argument inuti.

>[!IMPORTANT]
>
>Kommandot `subscribeRulesetItems` är det enda sättet att få förslag som kommer från regeluppsättningar, eftersom de inte returneras tillsammans med [`sendEvent`](sendevent/overview.md)-resultat. Du måste konfigurera din prenumeration innan du anropar `sendEvent` för att se till att offerter hämtas.


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

Ovanstående kod prenumererar på `web://example.com/#welcome`-ytan för innehållskort och använder `collectEvent`-bekvämlighetsmetoden för att generera `display`-händelser för alla förslag.

## Kommandoalternativ {#command-options}

Det här kommandot tar ett `options`-objekt med följande egenskaper:

| Egenskap | Typ | Beskrivning |
| --- | --- | --- |
| `surfaces` | Strängarray | En lista med ytor. Förslag tas endast emot av återanropsfunktionen om de matchar en av de ytor som finns här. |
| `schemas` | Strängarray | En lista med scheman. Förslag tas endast emot av återanropsfunktionen om de matchar ett av schemana som anges här. |
| `callback` | Funktion | En callback-funktion som anropas när -satser är resultatet av färdiga regeluppsättningar. Callback-funktionen tar emot två parametrar när den anropas: `result` och `collectEvent`. Mer information finns i [callback-parametrar](#callback-parameters). |

>[!TIP]
>
>Du kan prenumerera på flera ytor och scheman i ett enda kommando genom att skicka ytterligare värden till arrayerna `surfaces` och `schemas`.

### Parametrar för återanrop {#callback-parameters}

Callback-funktionen tar emot de två parametrar som beskrivs i tabellen nedan när den anropas.

| Parameter | Typ | Beskrivning |
| --- | --- | --- |
| `result` | Objekt | Det här objektet innehåller en `propositions`-matris.  De här förslagen är det direkta resultatet av färdiga regeluppsättningar. Objektet `result` är strukturerat på samma sätt som det [&#x200B; result-objekt &#x200B;](command-responses.md) som returneras av `sendEvent` med en `then` -sats. |
| `collectEvent` | Funktion | En smidig funktion som du kan använda för att skicka Edge Network-händelser för att spåra interaktioner, skärmar och andra händelser. |

### Funktionen `collectEvent` {#collectevent-function}

Funktionen `collectEvent` är en praktisk funktion som du kan använda för att skicka Edge Network-händelser för att spåra interaktioner, skärmar och andra händelser. Den godkänner de två parametrar som beskrivs i tabellen nedan.

| Parameter | Typ | Beskrivning |
| --- | --- | --- |
| Händelsetyp | Sträng | En sträng som anger vilken projektionshändelsetyp som ska genereras. Händelsetyper som stöds är `display`, `interact` eller `dismiss`. |
| `propositions` | Array | En array med förslag som motsvarar händelsen. |


Funktionen `collectEvent` kan anropas oberoende utanför återanropet. Det kan vara praktiskt att anropa den här funktionen när du spårar en interaktion eller en uppsägning vid en senare tidpunkt, t.ex. som svar på en användaråtgärd.

```js
collectEvent("interact", propositions);
```

## Prenumerera på innehållskort med hjälp av taggtillägget Web SDK

SDK-taggtillägget för webben som motsvarar kommandosvaren är en regel som prenumererar på händelsen [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). Med händelsen kan du ange önskade scheman och ytor.
