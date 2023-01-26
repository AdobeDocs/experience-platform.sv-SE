---
title: Återge anpassat innehåll med Adobe Experience Platform Web SDK
description: Lär dig återge personaliserat innehåll med Adobe Experience Platform Web SDK.
keywords: personalisering;renderDecision;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# Återge personaliserat innehåll

Adobe Experience Platform Web SDK stöder hämtning av personaliserat innehåll från personaliseringslösningar i Adobe, inklusive [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=sv) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html).

Dessutom hanterar Web SDK personalisering på samma sida och nästa sida genom Adobe Experience Platform personaliseringsmål, som [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) och [anslutning för anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md). Mer information om hur du konfigurerar Experience Platform för anpassning av samma sida och nästa sida finns i [dedikerad guide](../../destinations/ui/configure-personalization-destinations.md).

Innehåll som skapats i Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) och Adobe Journey Optimizer [WebbCampaign-användargränssnitt](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) kan hämtas och återges automatiskt av SDK. Innehåll som skapats i Adobe Target [Formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) eller Offer decisioning kan inte återges automatiskt av SDK. Istället måste du begära det här innehållet med SDK och sedan återge innehållet manuellt.

## Återge innehåll automatiskt

När du skickar händelser till servern kan du ange `renderDecisions` alternativ till `true`. Om du gör det tvingas SDK att automatiskt återge allt anpassat innehåll som är kvalificerat för automatisk återgivning.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Återgivning av anpassat innehåll är asynkront, så du bör inte göra antaganden om när ett visst innehåll har återgetts.

## Återge innehåll manuellt

Om du vill få åtkomst till innehåll för personalisering kan du tillhandahålla en callback-funktion som anropas efter att SDK har fått ett lyckat svar från servern. Ditt återanrop är en `result` objekt, som kan innehålla ett `propositions` -egenskap som innehåller returnerat personaliseringsinnehåll. Nedan visas ett exempel på hur du kan tillhandahålla en callback-funktion när du skickar en händelse.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

I det här exemplet `result.propositions`, om det finns, är en matris som innehåller personaliseringsförslag för händelsen. Som standard innehåller den endast förslag som är berättigade till automatisk återgivning.

The `propositions` arrayen kan se ut ungefär som i det här exemplet:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

I exemplet `renderDecisions` option was inte set to `true` när `sendEvent` SDK-kommandot kördes så det gjordes inget försök att automatiskt återge något innehåll. SDK hämtade dock fortfarande automatiskt det innehåll som är berättigat till automatisk återgivning, och om du vill göra det kunde du återge det manuellt. Observera att varje förslagsobjekt har sin `renderAttempted` egenskap inställd på `false`.

Om du istället hade ställt in `renderDecisions` alternativ till `true` när händelsen skulle skickas, skulle SDK ha försökt att återge alla förslag som är berättigade till automatisk återgivning (enligt beskrivningen ovan). Därför får vart och ett av de föreslagna objekten sin `renderAttempted` egenskap inställd på `true`. Du behöver inte återge dessa förslag manuellt i det här fallet.

Än så länge har vi bara diskuterat personaliseringsinnehåll som kan återges automatiskt (dvs. innehåll som har skapats i Adobe Target Visual Experience Composer eller Adobe Journey Optimizer Web Campaign-gränssnitt). Så här hämtar du anpassat innehåll _not_ som kan återge automatiskt måste du begära innehållet genom att fylla i `decisionScopes` när händelsen skickas. Ett omfång är en sträng som identifierar ett visst förslag som du vill hämta från servern.

Här är ett exempel:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

I det här exemplet, om förslag hittas på servern som matchar `salutation` eller `discount` omfång, returneras de och inkluderas i `result.propositions` array. Observera att alla förslag som kvalificerar sig för automatisk återgivning kommer att finnas med i `propositions` -array, oavsett hur du konfigurerar `renderDecisions` eller `decisionScopes` alternativ. The `propositions` skulle i det här fallet se ut som i det här exemplet:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

Nu kan du återge offertinnehåll när du vill. I det här exemplet matchar förslaget `discount` omfånget är ett HTML-förslag som har skapats med Adobe Target formulärbaserade Experience Composer. Anta att du har ett element på sidan med ID:t för `daily-special` och vill återge innehållet från `discount` lägga in `daily-special` -element gör du följande:

1. Extrahera förslag från `result` -objekt.
1. Slinga igenom varje förslag och leta efter det med omfånget `discount`.
1. Om du hittar ett förslag går du igenom varje objekt i utkastet och letar efter det objekt som innehåller HTML. (Det är bättre att kontrollera än att anta.)
1. Om du hittar ett objekt som innehåller innehåll från HTML kan du hitta `daily-special` -element på sidan och ersätt HTML med det anpassade innehållet.
1. När innehållet har renderats skickar du en `display` -händelse.

Koden ser ut så här:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Om du använder Adobe Target motsvarar omfattningar kryssrutor på servern, förutom att alla efterfrågas samtidigt i stället för var för sig. Den globala mbox returneras alltid.

### Hantera flimmer

SDK erbjuder anläggningar för [hantera flimmer](../personalization/manage-flicker.md) under personaliseringsprocessen.

## Rendera utkast i ensidiga program utan att öka mätvärdena {#applypropositions}

The `applyPropositions` kan du återge eller köra en array med förslag från [!DNL Target] till ensidiga program, utan att öka [!DNL Analytics] och [!DNL Target] mätvärden. Detta ökar rapporteringsnoggrannheten.

>[!IMPORTANT]
>
>Om föreslår för `__view__` omfånget (eller en webbyta) återges vid sidinläsning, deras `renderAttempted` flaggan ställs in på `true`. The `applyPropositions` kommer inte att återge `__view__` förslag på omfång (eller webbyta) som har `renderAttempted: true` flagga.

### Användningsfall 1: Återge förslag på en enkelsidig programvy

Det användningsfall som beskrivs i exemplet nedan återger de tidigare hämtade och återgivna kundvagnsvisningsförslagen utan att skicka visningsmeddelanden.

I exemplet nedan är `sendEvent` -kommandot aktiveras vid en vyändring och sparar det resulterande objektet i en konstant.

När sedan vyn eller komponenten uppdateras visas `applyPropositions` -kommandot anropas med förslag från föregående `sendEvent` om du vill återge visningsförslagen.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### Användningsfall 2: Återge förslag som inte har någon väljare

Det här användningsexemplet gäller aktivitetserbjudanden som skapats med [!DNL Target Form-based Experience Composer].

Du måste ange väljaren, åtgärden och omfånget i `applyPropositions` ring.

Stöds `actionTypes` är:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

Om du inte anger några metadata för ett beslutsomfång återges inte de associerade förslagen.
