---
title: Återge utkast manuellt
description: Rendera offertinnehåll med hjälp av din egen gränssnittslogik (HTML, JSON eller egna scheman) och spela sedan in visningshändelser.
keywords: personalisering;propositioner;manuell återgivning;sendEvent;DecisionScopes;display events;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Återge utkast manuellt

Använd det här mönstret när du vill ha fullständig kontroll över hur förslagsobjekt tillämpas. Du skapar till exempel ett komplext användargränssnitt från JSON-innehåll eller vill använda anpassade affärsregler innan återgivningen.

## &#x200B;1. Föreslå förslag

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Mer information finns i objektet [`personalization`](/help/collection/js/commands/sendevent/personalization.md) i kommandot [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;2. Återge förslagsobjekt (exempel)

När du återger utkast manuellt kan de ta många olika former eller former. Följande är ett minimalt exempel som hittar ett förslag efter omfång och sedan tillämpar det första HTML-innehållsobjektet som hittas.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Om du återger HTML måste du se till att det är säkert för din miljö. Behandla innehållsåtergivning som en säkerhetsgräns (sanering, pålitliga källor och CSP-överväganden).

## &#x200B;3. Spela in visningshändelser för det du återger

För manuellt återgivna inlägg spelas visningshändelser in via `sendEvent` anrop som refererar till återgivna inlägg.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Mer information finns i [Hantera visningshändelser](display-events.md).

## &#x200B;4. Återgivning

När användargränssnittsändringar kräver en omrendering kör du den manuella återgivningslogiken igen mot de förslagsdata som du har cache-lagrat (eller hämtar igen, om det behövs). Om du behöver spela in en visning för återgivningsscenarier läser du [Hantera visningshändelser](display-events.md).
