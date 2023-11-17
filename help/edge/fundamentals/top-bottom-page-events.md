---
title: Använda sidhändelser uppifrån och ned
description: I den här artikeln beskrivs hur du använder de övre och nedre delarna av sidhändelser i Web SDK.
source-git-commit: 221a9348803e111a1842b3abf2e74f7408da5994
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# Använda sidhändelser i början och slutet av Web SDK

När ni vill leverera personaliserade upplevelser till era kunder är en webbsidas laddningstid avgörande.

För att optimera inläsningstiden och leverera personalisering så snabbt som möjligt stöder Web SDK konfigurationen av sidans övre och nedre del.

Överkant och nederkant av sidhändelser beskriver en metod för asynkron inläsning av olika element på sidan, samtidigt som sidans inläsningstid hålls som ett minimum.

Den här konfigurationen minimerar den tid som en användare måste vänta tills det anpassade innehållet har lästs in.

När det gäller mätnoggrannhet kan Adobe Analytics ignorera sidhändelser, vilket leder till exaktare mätvärden eftersom bara en sidträff registreras (längst ned i sidhändelsen).

## Användningsfall {#use-cases}

En sportklädhandlare vill leverera personaliserade upplevelser till sina kunder och samtidigt minimera användarnas friktion när de besöker deras webbplats, samtidigt som de kan samla in besöksstatistik på ett korrekt sätt.

Genom att använda sidans övre och nedre del i Web SDK kan marknadsföringsteamet konfigurera sin personaliseringsleverans på det optimala sättet:

* Web SDK skickar en personaliseringsbegäran som läses in så fort sidan börjar läsas in. Det här är en toppnod i en sidhändelse.
* När sidan har lästs in spelas en sidvisningshändelse in. Detta sker senare under sidinläsningen. Det här är längst ned i sidhändelsen.

## Exempel på händelsen överst på sidan {#top-of-page}

Kodexemplet nedan visar ett exempel på en sidhändelsekonfiguration som begär personalisering men inte gör det [skicka visningshändelser](../personalization/display-events.md#send-sendEvent-calls) för automatiskt renderade utskick. The [visningshändelser](../personalization/display-events.md#send-sendEvent-calls) kommer att skickas som en del av den nedre delen av sidan.

>[!BEGINTABS]

>[!TAB Händelse överst på sidan]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parameter | Obligatoriskt/valfritt | Beskrivning |
|---|---|---|
| `type` | Obligatoriskt | Ställ in den här parametern på `decisioning.propositionFetch`. Den här speciella händelsetypen talar om för Adobe Analytics att den här händelsen ska släppas. När du använder Customer Journey Analytics kan du också ställa in ett filter för att släppa dessa händelser. |
| `renderDecisions` | Obligatoriskt | Ställ in den här parametern på `true`. Den här parametern anger för Web SDK att återge beslut som returneras av Edge Network. |
| `personalization.sendDisplayEvent` | Obligatoriskt | Ställ in den här parametern på `false`. Detta förhindrar att visningshändelser skickas. |

>[!ENDTABS]

## Längst ned i sidhändelseexempel {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Automatiskt återgivna förslag]

Kodexemplet nedan visar ett exempel på en nedre sidhändelsekonfiguration som skickar visningshändelser för förslag som automatiskt återges på sidan men för vilka visningshändelser ignorerades i [överst på sidan](#top-of-page) -händelse.

>[!NOTE]
>
>I det här scenariot måste du anropa händelsen längst ned på sidan _efter_ överst på sida ett. Men händelsen längst ned på sidan behöver inte vänta tills den översta sidan på sidan är slutförd.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Obligatoriskt/valfritt | Beskrivning |
|---|---|---|
| `personalization.includeRenderedPropositions` | Obligatoriskt | Ställ in den här parametern på `true`. Detta gör att det går att skicka visningshändelser som har inaktiverats högst upp i sidhändelsen. |
| `xdm` | Valfritt | Använd det här avsnittet om du vill inkludera alla data som behövs för sidhändelseslutet längst ned. |

>[!TAB Manuellt återgivna utdrag]

Kodexemplet nedan innehåller ett exempel på en nedre sidhändelsekonfiguration som skickar visningshändelser för förslag som återges manuellt på sidan (dvs. för anpassade beslutsomfattningar eller ytor).

>[!NOTE]
>
>I det här scenariot måste händelsen längst ned på sidan vänta tills händelsen längst upp på sidan har slutförts, för att återge utkastet och registrera händelsen längst ned på sidan.

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| Parameter | Obligatoriskt/valfritt | Beskrivning |
|---|---|---|
| `xdm._experience.decisioning.propositions` | Obligatoriskt | I det här avsnittet definieras de manuellt återgivna utdragen. Du måste inkludera förslaget `ID`, `scope`och `scopeDetails`. Läs dokumentationen om hur du [återge personalisering manuellt](../personalization/rendering-personalization-content.md#manually) om du vill ha mer information om hur du spelar in visningshändelser för manuellt återgivet innehåll. Manuellt återgivet personaliseringsinnehåll måste inkluderas i slutet av sidträffen. |
| `xdm._experience.decisioning.propositionEventType` | Obligatoriskt | Ställ in den här parametern på `display: 1`. |
| `xdm` | Valfritt | Använd det här avsnittet om du vill inkludera alla data som behövs för sidhändelseslutet längst ned. |

>[!ENDTABS]


## Enkelsidigt program med sidträffar upptill och nedtill {#spa-example}


>[!BEGINTABS]

>[!TAB Vy för första sidan]

Exemplet nedan innehåller tillägget `xdm.web.webPageDetails.viewName` parameter. Det är det som gör det till ett ensidigt program. The `viewName` i det här exemplet är den vy som läses in på sidan.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Andra sidvyn (alternativ 1)]

I det här exemplet finns ingen anledning att göra en siddelning uppifrån och ned eftersom sidans personalisering redan har hämtats.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB Andra sidvyn (alternativ 2)]

Om du fortfarande behöver fördröja sidträffens nederkant kan du använda `applyPropositions` för sidträffens överkant. Eftersom ingen personalisering behöver hämtas och inga analysdata behöver registreras, behöver du inte göra någon begäran till Edge Network.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

## GitHub-exempel {#github-sample}

Exemplet finns på [den här adressen](https://github.com/adobe/alloy-samples/tree/main/top-and-bottom) visar hur du kan använda Experience Platform och Web SDK för att begära personalisering överst på sidan och skicka analysdata längst ned. Du kan hämta exemplet och köra det lokalt för att förstå hur sidans övre och nedre del fungerar.
