---
title: subscribeRulesetItems
description: Prenumerera på innehållskort för en viss yta med kommandot subscribeRulesetItems.
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---


# `subscribeRulesetItems`

Med kommandot `subscribeRulesetItems` kan du prenumerera på erbjudanden som är resultatet av färdiga regeluppsättningar. Du kan göra detta genom att ange vilka ytor och scheman som ska filtreras efter och tillhandahålla en callback-funktion.

Alla tidslinjaler utvärderas så tar återanropsfunktionen emot ett `result`-objekt med en array med förslag i det.

>[!IMPORTANT]
>
>Kommandot `subscribeRulesetItems` är det enda sättet att få förslag som kommer från regeluppsättningar, eftersom de inte returneras tillsammans med [`sendEvent`](sendevent/overview.md)-resultat.

## Kommandoalternativ {#command-options}

Det här kommandot tar ett `options`-objekt med följande egenskaper:

| Egenskap | Typ | Beskrivning |
| --- | --- | --- |
| `surfaces` | Strängarray | En lista med ytor. Förslag tas endast emot av återanropsfunktionen om de matchar en av de ytor som finns här. |
| `schemas` | Strängarray | En lista med scheman. Förslag tas endast emot av återanropsfunktionen om de matchar ett av schemana som anges här. |
| `callback` | Funktion | En callback-funktion som anropas när -satser är resultatet av färdiga regeluppsättningar. Callback-funktionen tar emot två parametrar när den anropas: `result` och `collectEvent`. Mer information finns i [callback-parametrar](#callback-parameters). |

### Parametrar för återanrop {#callback-parameters}

Callback-funktionen tar emot de två parametrar som beskrivs i tabellen nedan när den anropas.

| Parameter | Typ | Beskrivning |
| --- | --- | --- |
| `result` | Objekt | Det här objektet innehåller en `propositions`-matris.  De här förslagen är det direkta resultatet av färdiga regeluppsättningar. Objektet `result` är strukturerat på samma sätt som det [ result-objekt ](command-responses.md) som returneras av `sendEvent` med en `then` -sats. |
| `collectEvent` | Funktion | En smidig funktion som du kan använda för att skicka Edge Network-händelser för att spåra interaktioner, skärmar och andra händelser. |

### Funktionen `collectEvent` {#collectevent-function}

Funktionen `collectEvent` är en praktisk funktion som du kan använda för att skicka Edge Network-händelser för att spåra interaktioner, visningar och andra händelser. Den godkänner de två parametrar som beskrivs i tabellen nedan.

| Parameter | Typ | Beskrivning |
| --- | --- | --- |
| Händelsetyp | Sträng | En sträng som anger vilken projektionshändelsetyp som ska genereras. Händelsetyper som stöds är `display`, `interact` eller `dismiss`. |
| `propositions` | Array | En array med förslag som motsvarar händelsen. |

## Prenumerera på innehållskort med taggtillägget Web SDK {#tag-extension}

Följ stegen nedan om du vill prenumerera på innehållskort via användargränssnittet Taggar.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Under [!UICONTROL Events] väljer du en befintlig händelse eller skapar en ny.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in **[!UICONTROL Event Type]** på **[!UICONTROL Subscribe ruleset items]**.
1. Markera de scheman och ytor som du vill prenumerera på innehållskort för, till höger på skärmen.
1. Välj **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Prenumerera på innehållskort med Web SDK JavaScript-biblioteket {#library}

Följande exempelkod prenumererar på `web://mywebsite.com/#welcome`-ytan för innehållskort och använder bekvämlighetsmetoden `collectEvent` för att generera `display`-händelser för alla förslag.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
