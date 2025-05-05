---
title: Återge anpassat innehåll med Adobe Experience Platform Web SDK
description: Lär dig återge personaliserat innehåll med Adobe Experience Platform Web SDK.
keywords: personalisering;renderDecision;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Återge personaliserat innehåll

Adobe Experience Platform Web SDK stöder hämtning av anpassat innehåll från personaliseringslösningar för Adobe, inklusive [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=sv) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=sv-SE).

Dessutom driver Web SDK personaliseringsfunktioner på samma sida och nästa sida genom Adobe Experience Platform personaliseringsmål, till exempel [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) och [en anpassad personaliseringsanslutning](../../destinations/catalog/personalization/custom-personalization.md). Mer information om hur du konfigurerar Experience Platform för anpassning av samma sida och nästa sida finns i den [dedikerade guiden](../../destinations/ui/activate-edge-personalization-destinations.md).

Innehåll som har skapats i Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=sv-SE) och Adobe Journey Optimizer [Web Campaign-gränssnittet](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=sv-SE) kan hämtas och återges automatiskt av SDK. Innehåll som har skapats i Adobe Target [formulärbaserade Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=sv-SE), Adobe Journey Optimizer [kodbaserad Experience Channel](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/code-based-experience/get-started-code-based) eller Offer decisioning kan inte återges automatiskt av SDK. Istället måste du begära det här innehållet med SDK och sedan återge innehållet manuellt.

## Återge innehåll automatiskt {#automatic}

När du skickar händelser till servern kan du ange alternativet `renderDecisions` till `true`. Om du gör det tvingas SDK att automatiskt återge allt anpassat innehåll som är kvalificerat för automatisk återgivning.

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

## Återge innehåll manuellt {#manual}

Om du vill få åtkomst till innehåll för personalisering kan du tillhandahålla en callback-funktion som anropas efter att SDK har fått ett lyckat svar från servern. Återanropet tillhandahålls som ett `result`-objekt, som kan innehålla en `propositions`-egenskap som innehåller returnerat personaliseringsinnehåll. Nedan visas ett exempel på hur du kan tillhandahålla en callback-funktion när du skickar en händelse.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

I det här exemplet är `result.propositions`, om det finns, en matris som innehåller personaliseringsförslag som är relaterade till händelsen. Som standard innehåller den endast förslag som är berättigade till automatisk återgivning.

Arrayen `propositions` kan se ut ungefär som i det här exemplet:

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

I exemplet var alternativet `renderDecisions` inte inställt på `true` när kommandot `sendEvent` kördes, så SDK försökte inte att automatiskt återge något innehåll. SDK hämtade dock fortfarande automatiskt det innehåll som är berättigat till automatisk återgivning, och om du vill göra det kunde du återge det manuellt. Observera att egenskapen `renderAttempted` har angetts till `false` för varje förslagsobjekt.

Om du i stället skulle ha angett alternativet `renderDecisions` som `true` när du skickade händelsen, skulle SDK ha försökt att återge alla förslag som är berättigade till automatisk återgivning (enligt beskrivningen ovan). Därför skulle egenskapen `renderAttempted` för vart och ett av förslagsobjekten ha angetts till `true`. Du behöver inte återge dessa förslag manuellt i det här fallet.

Än så länge har vi bara diskuterat personaliseringsinnehåll som kan återges automatiskt (dvs. innehåll som har skapats i Adobe Target Visual Experience Composer eller Adobe Journey Optimizer Web Campaign-gränssnitt). Om du vill hämta anpassat innehåll _som inte_ är kvalificerat för automatisk återgivning måste du begära innehållet genom att fylla i alternativet `decisionScopes` när du skickar händelsen. Ett omfång är en sträng som identifierar ett visst förslag som du vill hämta från servern.

Här är ett exempel:

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

I det här exemplet returneras och inkluderas i `result.propositions`-arrayen om det finns förslag på servern som matchar omfånget `salutation` eller `discount`. Observera att alla förslag som kvalificerar för automatisk återgivning kommer att inkluderas i `propositions`-arrayen, oavsett hur du konfigurerar alternativen för `renderDecisions` eller `decisionScopes`. Arrayen `propositions` skulle i det här fallet se ut som i det här exemplet:

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

Nu kan du återge offertinnehåll när du vill. I det här exemplet är det förslag som matchar omfånget `discount` ett HTML-förslag som skapats med Adobe Target formulärbaserade Experience Composer. Om du har ett element på sidan med ID:t `daily-special` och vill återge innehållet från `discount`-utkastet till elementet `daily-special` gör du följande:

1. Extrahera utdrag från objektet `result`.
1. Slinga igenom varje förslag och söker efter förslaget med omfånget `discount`.
1. Om du hittar ett förslag går du igenom varje objekt i utkastet och letar efter det objekt som innehåller HTML. (Det är bättre att kontrollera än att anta.)
1. Om du hittar ett objekt som innehåller innehåll från HTML söker du efter elementet `daily-special` på sidan och ersätter HTML med det anpassade innehållet.
1. Skicka en `display`-händelse när innehållet har återgetts.

Koden ser ut så här:

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
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

SDK ger möjligheter att [hantera flimmer](../personalization/manage-flicker.md) under personaliseringsprocessen.

## Rendera utkast i ensidiga program utan att öka mätvärdena {#applypropositions}

Med kommandot `applyPropositions` kan du återge eller köra en array med förslag från [!DNL Target] eller Adobe Journey Optimizer till ensidiga program, utan att öka värdena för [!DNL Analytics] och [!DNL Target]. Detta ökar rapporteringsnoggrannheten.

>[!IMPORTANT]
>
>Om utkast för `__view__`-omfånget (eller en webbyta) återges vid sidinläsning, kommer flaggan `renderAttempted` att anges till `true`. Kommandot `applyPropositions` återger inte de `__view__`-omfångsargument (eller webbytförslag) som har flaggan `renderAttempted: true`.

### Använd fall 1: Återge förslag på en enkelsidig programvy

Det användningsfall som beskrivs i exemplet nedan återger de tidigare hämtade och återgivna kundvagnsvisningsförslagen utan att skicka visningsmeddelanden.

I exemplet nedan aktiveras kommandot `sendEvent` vid en vyändring och det resulterande objektet sparas i en konstant.

När vyn eller komponenten uppdateras anropas kommandot `applyPropositions`, med förslagen från det föregående `sendEvent`-kommandot, för att återge visningsförslagen igen.

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
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
    "propositions": cartPropositions
});
```

### Användningsfall 2: Återge förslag som inte har någon väljare

Det här användningsexemplet gäller upplevelser som skapats med [!DNL Target Form-based Experience Composer] eller Adobe Journey Optimizer [kodbaserad Experience Channel](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/code-based-experience/get-started-code-based).

Du måste ange väljaren, åtgärden och omfattningen i anropet till `applyPropositions`.

`actionTypes` stöds:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

            alloy("sendEvent", {
                "xdm": {
                    "eventType": "decisioning.propositionDisplay",
                    "_experience": {
                        "decisioning": {
                            "propositions": [{
                              	"id": id,
                                "scope": scope,
                              	"scopeDetails": scopeDetails
                            }],
                            "propositionEventType": {
                                "display": 1
                            }
                        }
                    }
                }
            });
        }
    });
});
```

Om du inte anger några metadata för ett beslutsomfång återges inte de associerade förslagen.
