---
title: Hantera webbhändelser i SDK
description: Beskriver vad displayhändelser är och hur du kan använda dem i Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personalisering;visa händelser;sendEvent;renderDecision;applyPropositions;propositions;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Hantera webbhändelser i SDK

Visningshändelser talar om för personaliserings- eller analystjänster att ett visst stycke personaliserat innehåll visades för användaren. Att skicka visningshändelser förbättrar rapporteringsnoggrannheten genom att hjälpa system längre fram i kedjan att skilja mellan innehåll som var *begärt* och innehåll som *faktiskt visades*.

## Skicka visningshändelser automatiskt

Automatiska visningshändelser är vanligtvis det enklaste alternativet. De skickas omedelbart när Web SDK har återgett kvalificerat innehåll från svaret `sendEvent`, vilket kan förbättra rapportens precision.

Om du vill skicka visningshändelser automatiskt använder du ett `sendEvent`-anrop som ställer in `renderDecisions` på `true` och ställer in `personalization.sendDisplayEvent` på `true` (eller utelämnar det, eftersom `true` är standard):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Automatiska visningshändelser är beroende av SDK-hanterad återgivning. Om du återger innehåll manuellt (inklusive genom att använda `applyPropositions`) måste du skicka visningshändelser explicit med `sendEvent`.

## Skicka visningshändelser i efterföljande `sendEvent` samtal

Att inkludera visningshändelser i ett senare `sendEvent`-anrop är användbart när du vill bifoga ytterligare sidinläsningsdata som inte är tillgängliga när du begär personalisering. Det används ofta vid implementering av [händelser för översta och nedersta sidan](/help/collection/use-cases/personalization/top-bottom-page-events.md). Korrekt implementering av visningshändelser på det här sättet hjälper till att undvika problem med [studsfrekvensen](https://experienceleague.adobe.com/sv/docs/analytics/components/metrics/bounce-rate) i Adobe Analytics.

1. På det första `sendEvent`-anropet (ofta överst på sidan) begär och återger du innehåll, men inaktiverar automatiska visningshändelser genom att ställa in `renderDecisions` på `true` och `personalization.sendDisplayEvent` på `false`:

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Senare (ofta längst ned på sidan) anropar du `sendEvent` med en XDM-nyttolast som innehåller visningshändelser för utkast som har renderats sedan föregående begäran genom att ange [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) till `true`:

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Endast automatiskt återgivna utkast som hade inaktiverad visning inkluderas när `includeRenderedPropositions` används.

## Skicka visningshändelser för manuellt återgivna förslag

Om du återger innehåll själv (antingen helt manuellt eller med `applyPropositions`) måste du skicka visningshändelser explicit med kommandot `sendEvent`. Anropa `sendEvent` med en XDM-nyttolast som innehåller följande egenskaper:

* `_experience.decisioning.propositions` som innehåller de återgivna propositionerna `id`, `scope` och `scopeDetails`
* `_experience.decisioning.propositionEventType.display` inställd på `1`

I följande två exempel används den här hjälpfunktionen för att skapa XDM-nyttolasten för visningshändelser:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

I följande exempel används manuell återgivning med visningshändelser:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

I följande exempel används kommandot `applyPropositions` med visningshändelser. Den kedjar `sendEvent`, `applyPropositions` och sedan ytterligare `sendEvent` tillsammans:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Vanliga misstag att undvika

* **Skicka visningshändelser innan återgivningen avslutas**: Skicka visningshändelser när den automatiska återgivningen har slutförts, när `applyPropositions` har matchats eller när den manuella återgivningslogiken har slutförts.
* **Skicka visningshändelser för förslag som du inte återgav**: Inkludera endast förslag som faktiskt visades för användaren.
* **Släpper`scopeDetails`**: Inkludera `scopeDetails` från förslagsobjektet när visningshändelser skickas.
