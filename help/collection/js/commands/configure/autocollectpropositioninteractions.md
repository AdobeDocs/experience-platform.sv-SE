---
title: autoCollectPropositionInteractions
description: Samla in data automatiskt när någon klickar på en länk.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

Egenskapen `autoCollectPropositionInteractions` är en valfri inställning som avgör om Web SDK automatiskt samlar in offertinteraktioner. Värdet är en karta över beslutsfattare, där vart och ett har ett värde som anger hur automatiska offertinteraktioner ska hanteras.

När du aktiverar automatisk spårning av offertinteraktion, samlas alla klick i ett förslagselement som renderas till DOM automatiskt in av Web SDK. Den här samlingen innehåller alla upplevelser som automatiskt återges för DOM av Web SDK och upplevelser som återges för DOM med kommandot [`applyPropositions`](../applypropositions.md).

Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `{"AJO": "always", "TGT": "never"}`. Om du inte vill spåra offertinteraktioner automatiskt anger du värdet till `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Egenskaper som stöds i det här objektet är:

| Egenskap | Beskrivning |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Möjliga värden för varje egenskap är:

| Värde | Beskrivning |
| --- | --- |
| **`always`** | Samla alltid automatiskt in `interact`-händelser för alla element som är kopplade till ett förslag. |
| **`never`** | Samla aldrig automatiskt in `interact`-händelser för element som är kopplade till ett förslag. |
| **`decoratedElementsOnly`** | Samla automatiskt in `interact`-händelser för element som är kopplade till ett förslag om elementet innehåller dataattribut som anger en etikett eller token. |

## Dataattribut {#data-attributes}

Du kan använda dataattribut på element för att lägga till specificitet i en interaktion.

| Namn | Dataattribut | Beskrivning |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | När etikettdataattributet finns på ett element som klickats inkluderas det i den interaktionsinformation som skickas till Edge Network. Web SDK söker efter ett etikettdataattribut som börjar med elementet som klickas och går upp i DOM-trädet. Web SDK använder den första etiketten som hittas. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Använd den här token när du använder beslutsprinciper i [Adobe Journey Optimizer-kodbaserade kampanjer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Du kan använda denna token för att avgöra vilket beslutsprincipobjekt som klickades på. När tokendatattributet finns på ett element som du klickat på inkluderas det med interaktionsinformationen som skickas till Edge Network. Web SDK söker efter ett tokendataattribut som börjar med elementet som klickas och går upp i DOM-trädet. Web SDK använder den första variabeln som hittas. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Web SDK lägger automatiskt till detta unika ID i behållarelement vid återgivning av utkast. Webb-SDK använder detta ID för att korrelera DOM-element med förslag. Eftersom detta är ett ID som krävs av Web SDK bör du inte ändra det på något sätt. Du kan ignorera det. |

## Exempel

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Använda `autoCollectPropositionInteractions` med kommandot `applyPropositions` {#apply-propositions}

Kommandot [`applyPropositions`](../applypropositions.md) är ett praktiskt sätt att återge utkast till DOM. När det gäller kodbaserade kampanjer med JSON kan du emellertid använda det här kommandot för att korrelera ett befintligt DOM-element (eller det som programkoden återges på skärmen baserat på JSON-värdena) med ett förslag.

Den här korrelationen aktiverar automatisk interaktionsspårning för det elementet och tilldelar det elementet rätt förslag. För att uppnå detta anger du `actionType` till `track`.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Konfigurera automatisk offertinteraktion för SDK-taggtillägg för webben

Följande två listrutor när du konfigurerar taggtillägget Web SDK är taggrekvivalenten för det här objektet:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
