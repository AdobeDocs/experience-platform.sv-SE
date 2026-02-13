---
title: Återge automatiskt förslag på DOM-åtgärder
description: Använd Web SDK för att automatiskt återge lämpliga DOM-åtgärdsförslag och hantera vanliga SPA-återgivningsscenarier.
keywords: personalisering;renderDecision;dom-action;sendEvent;applyPropositions;single page application;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Återge DOM-åtgärdsförslag automatiskt

Använd det här mönstret när ditt personaliseringssvar innehåller förslagsobjekt med schemat:

**`https://ns.adobe.com/personalization/dom-action`**

Dessa objekt innehåller vanligtvis en väljare och en åtgärdstyp (till exempel `setHtml`) som Web SDK kan använda automatiskt när `renderDecisions` aktiveras.

## &#x200B;1. Hantera flimmer (valfritt)

Om du behöver förhindra flimmer när personaliserat innehåll används ska du använda den rekommenderade metoden för flimmerhantering för implementeringen. Se [Hantera flimmer](manage-flicker.md) för tillgängliga alternativ.

## &#x200B;2. Begär och återge de beslut som gäller automatisk återgivning

Ange `renderDecisions` som `true` när du anropar kommandot `sendEvent`. Egenskapen `renderDecisions` är som standard false om den utelämnas.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Om du behöver begära specifika placeringar kan du inkludera `personalization.decisionScopes`:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Mer information finns i objektet [`personalization`](/help/collection/js/commands/sendevent/personalization.md) i kommandot [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;3. Visa händelser

Om du ställer in `renderDecisions` på `true` och antingen ställer in `personalization.sendDisplayEvent` på `true` eller utelämnar det, skickar Web SDK visningshändelser omedelbart efter att personaliseringen har renderats.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Se [Hantera visningshändelser](display-events.md) för alternativa alternativ som uppfyller implementeringens behov, t.ex. när du använder [händelser på övre och nedre sidan](top-bottom-page-events.md).

## &#x200B;4. SPA-vy ändras och återgivning sker

För enkelsidiga program ska du inkludera en `viewName` om händelser som ändras i visningen.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Om SPA återger användargränssnittet för samma vy utan att hämta något nytt beslut kan du återanvända tidigare returnerade förslag:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Mer information finns i [`applyPropositions`](/help/collection/js/commands/applypropositions.md).

>[!NOTE]
>
>Kommandot `applyPropositions` skickar inte automatiskt visningshändelser. Om du behöver spela in &quot;display&quot; för återgivningsscenarier kan du läsa [Hantera visningshändelser](display-events.md).
