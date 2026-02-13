---
title: Återge HTML-erbjudanden utan väljare
description: Rendera objekt i HTML som inte innehåller väljare genom att ange metadata för applyPropositions och sedan spela in visningshändelser.
keywords: personalisering;applyPropositions;metadata;actionType;DecisionScopes;display events;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Återge HTML-erbjudanden utan väljare

Använd det här mönstret när dina förslag innehåller HTML-innehåll, men du måste ange var det ska användas (väljare) och hur det ska användas (åtgärdstyp). Du kan göra detta genom att anropa [`applyPropositions`](/help/collection/js/commands/applypropositions.md) med ett `metadata`-objekt som är keyat efter omfång. `actionType`-värden som stöds är `setHtml`, `replaceHtml` och `appendHtml`.

## &#x200B;1. Hantera flimmer (valfritt)

Om du döljer innehåll under återgivningen ansvarar du för att det visas när återgivningen är klar. Mer information finns i [Hantera flimmer](manage-flicker.md).

## &#x200B;2. Begär förslag för de omfattningar som du tänker återge

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Mer information finns i [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md).

## &#x200B;3. Rendera erbjudanden med `applyPropositions` metadata

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Spela in visningshändelser för renderade offerter

Visningshändelser skickas inte automatiskt när `applyPropositions` anropas. När återgivningen är klar använder du ett `sendEvent`-anrop som refererar till de återgivna propositionerna:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Mer information finns i [Hantera visningshändelser](display-events.md).

>[!TIP]
>
>Om du använder [händelserna längst upp och längst ned ](top-bottom-page-events.md) implementeras det här anropet för att visa poster vanligtvis i det nedre `sendEvent` anropet.

## &#x200B;5. Återgivning

Om implementeringen kräver en återgivning senare (t.ex. i ensidiga program), anropar du `applyPropositions` igen med samma argument och metadata:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Om du behöver spela in en visningshändelse för den återgivningen läser du [Hantera visningshändelser](display-events.md).
