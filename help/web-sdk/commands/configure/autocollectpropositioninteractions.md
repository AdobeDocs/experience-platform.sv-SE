---
title: autoCollectPropositionInteractions
description: Lär dig hur du konfigurerar Experience Platform Web SDK att automatiskt samla in länkdata.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: 55c656e7fd08e98b75c20f0688a6697baf533291
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# `autoCollectPropositionInteractions`

Egenskapen `autoCollectPropositionInteractions` är en valfri inställning som avgör om Web SDK ska samla in offertinteraktioner automatiskt.

Värdet är en karta över beslutsfattare, där vart och ett har ett värde som anger hur automatiska offertinteraktioner ska hanteras.

## Värden som stöds {#supported-values}

Som standard samlas _always_ in automatiskt för Adobe Journey Optimizer (`AJO`) och _never_ samlas in för Adobe Target (`TGT`).

Standardvärdet `autoTrackPropositionInteractions` visas nedan.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Se tabellen nedan för de konfigurationsvärden som stöds för varje beslutsprovider.

| Värde | Beskrivning |
| --- | --- |
| `always` | [!DNL Web SDK] samlar alltid automatiskt in `interact`-händelser för alla element som är kopplade till ett förslag. |
| `never` | [!DNL Web SDK] samlar aldrig automatiskt in `interact`-händelser för element som är kopplade till ett förslag. |
| `decoratedElementsOnly` | [!DNL Web SDK] samlar automatiskt in `interact`-händelser för element som är kopplade till ett förslag, men bara om elementet innehåller dataattribut som anger en etikett eller token. |

## Automatisk spårning av interaktion med förslag {#logic}

När du aktiverar automatisk spårning av förslagsinteraktion, samlas alla klick i ett förslagselement som har återgetts till DOM automatiskt in av [!DNL Web SDK]. Detta inkluderar alla upplevelser som automatiskt återges för DOM av [!DNL Web SDK] och upplevelser som återges för DOM med kommandot [`applyPropositions`](../applypropositions.md).

### Dataattribut {#data-attributes}

Du kan använda dataattribut på element för att lägga till specificitet i en interaktion.

| Namn | Dataattribut | Beskrivning |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | När etikettdataattributet finns i ett element som klickats inkluderas det med den interaktionsinformation som skickas till [!DNL Edge Network]. [!DNL Web SDK] söker efter ett etikettdataattribut som börjar med elementet som klickats och går upp i DOM-trädet. [!DNL Web SDK] använder den första etiketten som hittas. |
| [!DNL Token] | `data-aep-click-token` | Använd den här token när du använder beslutsprinciper i [Adobe Journey Optimizer-kodbaserade kampanjer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Du kan använda denna token för att avgöra vilket beslutsprincipobjekt som klickades på. När tokendatattribut finns på ett element som du klickat på inkluderas det med den interaktionsinformation som skickas till Edge Network. [!DNL Web SDK] söker efter ett tokendataattribut som börjar med elementet som klickats och går upp i DOM-trädet. [!DNL Web SDK] använder den första token som hittas. |
| [!DNL Interact ID] | `data-aep-interact-id` | [!DNL Web SDK] lägger automatiskt till detta unika ID i behållarelement när utkast återges. Webb-SDK använder det här ID:t för att korrelera [!DNL DOM]-element med förslag. Eftersom detta är ett ID som krävs av [!DNL Web SDK], bör du inte ändra det på något sätt. Du kan ignorera det. |

**Exempel**

Se kodfragmentet nedan för att se ett exempel på hur du använder dataattribut.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### Kommandot `applyPropositions` {#apply-propositions}

Läs [`applyPropositions`](../applypropositions.md)-dokumentationen om du vill veta hur det här kommandot fungerar.

Kommandot `applyPropositions` är ett praktiskt sätt att återge utkast till [!DNL DOM]. För kodbaserade kampanjer med `JSON` kan du emellertid använda det här kommandot för att korrelera ett befintligt [!DNL DOM] -element (eller det som programkoden återger till skärmen baserat på `JSON`-värdena) med ett förslag.

Den här korrelationen aktiverar automatisk interaktionsspårning för det elementet och tilldelar det elementet rätt förslag. För att uppnå detta anger du `actionType` till `track`.

**Exempel**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Aktivera automatiska förslag och interaktioner klickspårning via taggtillägget Web SDK {#tag-extension}

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-autentiseringsuppgifter.
1. Navigera till **Datainsamling** > **Taggar**.
1. Välj önskad taggegenskap.
1. Navigera till **Tillägg** och välj sedan **Konfigurera** på Adobe Experience Platform Web SDK-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Data Collection]** och markera kryssrutan **Aktivera förslag och spårning av interaktionslänk**.
1. Välj **Spara** och publicera sedan ändringarna.

## Aktivera automatisk spårning av interaktionslänkar i Web SDK JavaScript-biblioteket {#library}

Spåra förslag är aktiverat som standard i [!DNL Web SDK]. Du kan dock konfigurera det ytterligare med värdet `autoCollectPropositionInteractions` när du kör kommandot [`configure`](../configure/overview.md).

Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `{"AJO": "always", "TGT": "never"}`. Om du inte vill spåra offertinteraktioner automatiskt anger du värdet till `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoCollectPropositionInteractions": {"AJO": "always", "TGT": "never"}
});
```
