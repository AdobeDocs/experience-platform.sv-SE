---
title: Återge anpassat innehåll med Adobe Experience Platform Web SDK
description: Lär dig återge personaliserat innehåll med Adobe Experience Platform Web SDK.
keywords: personalisering;renderDecision;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Återge personaliserat innehåll

Adobe Experience Platform Web SDK stöder hämtning av anpassat innehåll från personaliseringslösningar på Adobe, inklusive [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) och [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=sv). Innehåll som skapas i Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kan hämtas och återges automatiskt av SDK:n. Innehåll som skapats i Adobe Target [formulärbaserad Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) eller Offer decisioning kan inte återges automatiskt av SDK:n. Istället måste du begära det här innehållet med SDK och sedan återge innehållet manuellt.

## Återge innehåll automatiskt

När du skickar händelser till servern kan du ange `renderDecisions` som `true`. Om du gör det tvingas SDK att automatiskt återge allt anpassat innehåll som är kvalificerat för automatisk återgivning.

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

Om du vill få åtkomst till innehåll för personalisering kan du tillhandahålla en callback-funktion som anropas efter att SDK har fått ett lyckat svar från servern. Callback-funktionen har ett `result`-objekt, som kan innehålla en `propositions`-egenskap som innehåller returnerat personaliseringsinnehåll. Nedan visas ett exempel på hur du kan tillhandahålla en callback-funktion när du skickar en händelse.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

I det här exemplet är `result.propositions`, om det finns, en matris som innehåller personaliseringsförslag relaterade till händelsen. Som standard innehåller den endast förslag som är berättigade till automatisk återgivning.

Matrisen `propositions` kan se ut ungefär som i det här exemplet:

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
    "renderAttempted": false
  }
]
```

I exemplet var inte alternativet `renderDecisions` inställt på `true` när kommandot `sendEvent` kördes, så SDK försökte inte återge något innehåll automatiskt. SDK hämtade dock fortfarande automatiskt det innehåll som är berättigat till automatisk återgivning, och om du vill göra det kunde du återge det manuellt. Observera att egenskapen `renderAttempted` för varje förslagsobjekt är `false`.

Om du i stället skulle ha angett `renderDecisions` som `true` när du skickade händelsen, skulle SDK ha försökt att återge alla förslag som är berättigade till automatisk återgivning (enligt beskrivningen ovan). Därför skulle var och en av förslagsobjekten ha egenskapen `renderAttempted` inställd på `true`. Du behöver inte återge dessa förslag manuellt i det här fallet.

Hittills har vi bara diskuterat personaliserat innehåll som är berättigat till automatisk återgivning (det vill säga allt innehåll som har skapats i Adobe Target Visual Experience Composer). Om du vill hämta anpassat innehåll _som inte är_-kvalificerat för automatisk återgivning måste du begära innehållet genom att fylla i alternativet `decisionScopes` när du skickar händelsen. Ett omfång är en sträng som identifierar ett visst förslag som du vill hämta från servern.

Här är ett exempel:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

I det här exemplet returneras och inkluderas i `result.propositions`-arrayen om det finns förslag på servern som matchar `salutation`- eller `discount`-omfånget. Observera att alla förslag som kvalificerar för automatisk återgivning kommer att inkluderas i `propositions`-arrayen, oavsett hur du konfigurerar alternativen `renderDecisions` eller `decisionScopes`. Matrisen `propositions`, i det här fallet, skulle se ut ungefär som i det här exemplet:

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
    "renderAttempted": false
  }
]
```

Nu kan du återge offertinnehåll när du vill. I det här exemplet är det förslag som matchar `discount`-omfånget ett HTML-förslag som skapats med Adobe Target Form-based Experience Composer. Om du har ett element på sidan med ID:t `daily-special` och vill återge innehållet från `discount`-utkastet till `daily-special`-elementet gör du följande:

1. Extrahera utdrag från `result`-objektet.
1. Slinga igenom varje förslag och leta efter förslaget med omfånget `discount`.
1. Om du hittar ett förslag kan du slinga igenom varje objekt i utkastet och leta efter det objekt som är HTML-innehåll. (Det är bättre att kontrollera än att anta.)
1. Om du hittar ett objekt som innehåller HTML-innehåll söker du efter elementet `daily-special` på sidan och ersätter dess HTML-kod med det anpassade innehållet.

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
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Om du använder Adobe Target motsvarar omfattningar kryssrutor på servern, förutom att alla efterfrågas samtidigt i stället för var för sig. Den globala mbox returneras alltid.

### Hantera flimmer

SDK ger möjlighet att [hantera flimmer](../personalization/manage-flicker.md) under personaliseringsprocessen.
