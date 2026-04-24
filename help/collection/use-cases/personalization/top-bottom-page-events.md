---
title: Konfigurera de övre och nedre sidhändelserna i Web SDK
description: I den här artikeln beskrivs hur du använder de övre och nedre delarna av sidhändelser i Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---


# Konfigurera de övre och nedre sidhändelserna i Web SDK

När du levererar personaliserade upplevelser är webbsidans laddningstid avgörande. För att minimera tiden en användare väntar på anpassat innehåll stöder Web SDK konfigurationen av sidans övre och nedre del.

Överkant och nederkant av sidhändelser beskriver en metod för asynkron inläsning av olika element på sidan samtidigt som sidans inläsningstid hålls som ett minimum:

* Sidans översta händelse begär personalisering så snart sidan börjar läsas in.
* Längst ned i sidhändelsen registreras en sidvy när sidan har lästs in.

Adobe Analytics ignorerar sidans överkant, vilket leder till exaktare mätvärden eftersom bara en sidträff spelas in (längst ned i sidhändelsen).

Du kan konfigurera topp- och bottendelen av sidhändelser på två sätt: genom att anropa SDK-biblioteket (`alloy()`) direkt eller genom att använda taggtillägget Web SDK i användargränssnittet för Adobe Experience Platform-taggar. Taggtilläggets [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-åtgärd innehåller ett [!UICONTROL Use guided events]-alternativ som förkonfigurerar fältvärden för scenarierna [!UICONTROL Request personalization] (överst på sidan) och [!UICONTROL Collect analytics] (nederst på sidan). Varje exempel nedan visar båda implementeringarna.

## Händelse överst på sidan {#top-of-page}

I exemplet nedan konfigureras en övre sidhändelse som begär personalisering, men utelämnar [visningshändelser](display-events.md) för automatiskt återgivna profiler. Dessa visningshändelser skickas i stället med längst ned i sidhändelsen.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

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
| --- | --- | --- |
| `type` | Obligatoriskt | Ställ in den här parametern på `decisioning.propositionFetch`. Den här speciella händelsetypen talar om för Adobe Analytics att den här händelsen ska släppas. När du använder Customer Journey Analytics kan du också konfigurera ett filter för att släppa dessa händelser. Mer information finns i [Edge Network händelsetyper i Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types). |
| `renderDecisions` | Obligatoriskt | Ställ in den här parametern på `true`. Den här parametern anger för Web SDK att återge beslut som returneras av Edge Network. |
| `personalization.sendDisplayEvent` | Obligatoriskt | Ställ in den här parametern på `false`. Den här parametern stoppar visning av händelser från att skickas. |

>[!TAB Webbtaggtillägg för SDK]

Konfigurera en [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-åtgärd i regeln som utlöses överst på sidan. Aktivera **[!UICONTROL Use guided events]** och välj sedan **[!UICONTROL Request personalization]**. Det här alternativet låser [!UICONTROL Type] till [!UICONTROL Decisioning Proposition Fetch], [!UICONTROL Render visual personalization decisions] till aktiverad och [!UICONTROL Automatically send a display event] till inaktiverad.

Om du vill ange dessa fält manuellt i stället låter du **[!UICONTROL Use guided events]** vara inaktiverat och konfigurerar varje fält själv.

>[!ENDTABS]

## Längst ned i sidhändelseexempel {#bottom-of-page}

### Automatiskt återgivna förslag {#bottom-auto-rendered}

Exemplet nedan konfigurerar en händelse längst ned på sidan som skickar visningshändelser för förslag som automatiskt återges på sidan men som inte visas i händelsen [top på sidan](#top-of-page).

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Obligatoriskt/valfritt | Beskrivning |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Obligatoriskt | Ställ in den här parametern på `true`. Den här parametern gör det möjligt att skicka visningshändelser som har inaktiverats i sidhändelseens överkant. |
| `xdm` | Valfritt | Använd det här objektet om du vill inkludera alla data som du vill ha för sidhändelseslutet längst ned. |

>[!TAB Webbtaggtillägg för SDK]

Konfigurera en [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-åtgärd i regeln som utlöses längst ned på sidan. Aktivera **[!UICONTROL Use guided events]** och välj sedan **[!UICONTROL Collect analytics]**. Det här alternativet låser [!UICONTROL Include rendered propositions] till aktiverat.

Om du vill ange det här fältet manuellt i stället låter du **[!UICONTROL Use guided events]** vara inaktiverat och aktiverar **[!UICONTROL Include rendered propositions]** direkt. Du kan också fylla i fältet **[!UICONTROL XDM]** med ett [ XDM-objektdataelement ](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) som innehåller siddata.

>[!ENDTABS]

### Manuellt återgivna utdrag {#bottom-manually-rendered}

Exemplet nedan konfigurerar en händelse längst ned på sidan som skickar visningshändelser för förslag som återges manuellt på sidan (det vill säga för anpassade beslutsomfattningar eller ytor).

>[!NOTE]
>
>I det här scenariot måste händelsen längst ned på sidan vänta tills den översta sidhändelsen har slutförts, så att utkasten kan återges och spelas in.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

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
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Obligatoriskt | I det här avsnittet definieras de manuellt återgivna utdragen. Du måste inkludera förslaget `id`, `scope` och `scopeDetails`. Mer information finns i [Hantera visningshändelser](display-events.md). Manuellt återgivet personaliseringsinnehåll måste inkluderas i slutet av sidhändelsen. |
| `xdm._experience.decisioning.propositionEventType` | Obligatoriskt | Ställ in den här parametern på `display: 1`. |
| `xdm` | Valfritt | Använd det här objektet om du vill inkludera alla data som du vill ha för sidhändelseslutet längst ned. |

>[!TAB Webbtaggtillägg för SDK]

Alternativet [!UICONTROL Use guided events] täcker inte det här scenariot, så konfigurera åtgärden manuellt:

1. Skapa ett [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (eller [Variabel](/help/tags/extensions/client/web-sdk/data-element-types.md#variable))-dataelement som fyller i `_experience.decisioning.propositions` med varje återgivet projekts `id`, `scope` och `scopeDetails`, och ställer in `_experience.decisioning.propositionEventType.display` på `1`. Mer information finns i [Hantera visningshändelser](display-events.md).
1. Lämna [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) inaktiverat och referera till dataelementet från fältet **[!UICONTROL Use guided events]** i **[!UICONTROL XDM]**-åtgärden för den nedre sidlinjalen.

>[!ENDTABS]

## Enkelsidigt program med sidhändelser i över- och underkant {#spa-example}

I ett enkelsidigt program måste du ange visningsnamnet för varje vyändring så att Web SDK återger rätt personalisering högst upp på sidan och registrerar rätt vy längst ned på sidan.

### Vy för första sidan {#spa-first-view}

I det här exemplet är `home` den vy som läses in på den första sidan.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

Det översta anropet begär personalisering för vyn `home` utan att registrera en Analytics-träff eller aktivera visningshändelser. Det nedre anropet registrerar sidvyn och utlöser de inaktiverade visningshändelserna. Inkludera samma `viewName` i båda anropen så att vyn spelas in konsekvent.

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

>[!TAB Webbtaggtillägg för SDK]

1. Skapa ett [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-dataelement som anger `web.webPageDetails.viewName` till vyns namn (till exempel `home`).
1. Konfigurera en översta sidåtgärd [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): aktivera **[!UICONTROL Use guided events]**, markera **[!UICONTROL Request personalization]** och referera dataelementet i fältet **[!UICONTROL XDM]**.
1. Konfigurera en nederkant av åtgärden **[!UICONTROL Send event]**: aktivera **[!UICONTROL Use guided events]**, markera **[!UICONTROL Collect analytics]** och referera till samma dataelement i fältet **[!UICONTROL XDM]** så att `viewName` matchar i båda händelserna.

>[!ENDTABS]

### Andra sidvyn - alternativ 1 {#spa-second-view-option-1}

I det här exemplet räcker det med en händelse eftersom sidans personalisering redan har hämtats.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

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

>[!TAB Webbtaggtillägg för SDK]

1. Skapa ett [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-dataelement som anger `web.webPageDetails.viewName` till den nya vyns namn (till exempel `cart`).
1. Konfigurera en enskild [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-åtgärd vid vyändringen: lämna **[!UICONTROL Use guided events]** inaktiverat, aktivera **[!UICONTROL Render visual personalization decisions]** och referera dataelementet i fältet **[!UICONTROL XDM]**.

>[!ENDTABS]

### Andra sidvyn - alternativ 2 {#spa-second-view-option-2}

Använd den här metoden när du behöver fördröja sidans nederkant (till exempel när sidans analysdata inte är klara vid tidpunkten för vyändringen). Hantera vyändringen i två steg:

1. Längst upp på sidan kan du återge de redan hämtade förslagen utan att ringa Edge Network.
1. När analysdata är klara skickar du längst ned i sidhändelsen.

Inkludera samma `viewName` i båda anropen så att vyn spelas in konsekvent.

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

Anropa [`applyPropositions`](/help/collection/js/commands/applypropositions.md) högst upp på sidan om du vill återge cachelagrade utkast för den nya vyn. Anropa sedan `sendEvent` längst ned på sidan med `includeRenderedPropositions: true` så att de inaktiverade visningshändelserna utlöses.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB Webbtaggtillägg för SDK]

1. Skapa ett [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-dataelement som anger `web.webPageDetails.viewName` till den nya vyns namn (till exempel `cart`).
1. Konfigurera en [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)-åtgärd för sidans översta händelse och ställ in fältet **[!UICONTROL View name]** på vyns namn (till exempel `cart`). Den här åtgärden återger redan hämtade förslag utan att kontakta Edge Network.
1. Konfigurera en [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-åtgärd för händelsen längst ned på sidan: aktivera **[!UICONTROL Use guided events]**, markera **[!UICONTROL Collect analytics]** och referera dataelementet i fältet **[!UICONTROL XDM]**.

>[!ENDTABS]

## GitHub-exempel {#github-sample}

[Det översta och nedersta exemplet i databasen ](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) med legeringsexempel visar hur du kan begära personalisering högst upp på sidan och skicka analysstatistik längst ned. Ladda ned exemplet och kör det lokalt för att se hur sidans övre och nedre del fungerar. Exemplet använder JavaScript-biblioteket direkt. Samma mönster används när du konfigurerar motsvarande regler i taggtillägget Web SDK.
