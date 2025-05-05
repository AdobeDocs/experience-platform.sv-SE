---
title: Händelsetyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig hur du använder händelsetyper från Adobe Experience Platform Web SDK-tillägget i Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b37bf09e3ec16f29d6acee3bca71463fa2c876ce
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 0%

---

# Händelsetyper

Den här sidan beskriver de Adobe Experience Platform-händelsetyper som finns i taggtillägget Adobe Experience Platform Web SDK. Dessa används för att [skapa regler](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=sv-SE) och ska inte blandas ihop med fältet `eventType` i [`xdm` object](/help/web-sdk/commands/sendevent/xdm.md).

## Övervakningkrok utlöses {#monitoring-hook-triggered}

Adobe Experience Platform Web SDK innehåller övervakningskopplingar som du kan använda för att övervaka olika systemhändelser. De här verktygen är användbara när du vill utveckla egna felsökningsverktyg och hämta Web SDK-loggar.

Fullständig information om vilka parametrar varje övervakningshändelse innehåller finns i [dokumentationen för Web SDK-övervakning av kopplingar](../../../../web-sdk/monitoring-hooks.md).

![Taggar användargränssnittsbilden som visar typen för Övervakningshändelse ](assets/monitoring-hook-triggered.png)

Web SDK-taggtillägget stöder följande övervakningskopplingar:

* **[!UICONTROL onInstanceCreated]**: Den här övervakningshändelsen utlöses när du har skapat en ny Web SDK-instans.
* **[!UICONTROL onInstanceConfigured]**: Den här övervakningshändelsen utlöses av Web SDK när kommandot [`configure`](../../../../web-sdk/commands/configure/overview.md) har lösts
* **[!UICONTROL onBeforeCommand]**: Den här övervakningshändelsen utlöses av Web SDK innan något annat kommando körs. Du kan använda den här övervakningsfunktionen för att hämta konfigurationsalternativen för ett specifikt kommando.
* **[!UICONTROL onCommandResolved]**: Den här övervakningshändelsen utlöses innan kommandolöftet löses. Du kan använda den här funktionen för att se kommandoalternativen och resultatet.
* **[!UICONTROL onCommandRejected]**: Den här övervakningshändelsen utlöses när ett kommandolöfte avvisas och innehåller information om felets orsak.
* **[!UICONTROL onBeforeNetworkRequest]**: Den här övervakningshändelsen utlöses innan en nätverksbegäran körs.
* **[!UICONTROL onNetworkResponse]**: Den här övervakningshändelsen utlöses när webbläsaren får ett svar.
* **[!UICONTROL onNetworkError]**: Den här övervakningshändelsen utlöses när nätverksbegäran misslyckas.
* **[!UICONTROL onBeforeLog]**: Den här övervakningshändelsen utlöses innan Web SDK loggar något till konsolen.
* **[!UICONTROL onContentRendering]**: Den här övervakningshändelsen aktiveras av komponenten `personalization` och hjälper dig att felsöka återgivningen av personaliseringsinnehållet. Den här händelsen kan ha olika status:
   * `rendering-started`: Anger att Web SDK håller på att återge förslag. Innan Web SDK börjar återge ett beslutsområde eller en vy kan du i objektet `data` se de förslag som ska återges av komponenten `personalization` och scopenamnet.
   * `no-offers`: Anger att ingen nyttolast har tagits emot för de begärda parametrarna.
   * `rendering-failed`: Anger att Web SDK inte kunde återge ett förslag.
   * `rendering-succeeded`: Anger att återgivningen har slutförts för ett beslutsområde.
   * `rendering-redirect`: Anger att Web SDK kommer att köra en omdirigeringsdisposition.
* **[!UICONTROL onContentHiding]**: Den här övervakningshändelsen utlöses när ett fördolt format används eller tas bort.


## [!UICONTROL Send event complete]

Vanligtvis har din egenskap en eller flera regler som använder [[!UICONTROL Send event]-åtgärden ](action-types.md#send-event) för att skicka händelser till Adobe Experience Platform Edge Network. Varje gång en händelse skickas till Edge Network returneras ett svar med användbara data till webbläsaren. Utan händelsetypen [!UICONTROL Send event complete] har du inte åtkomst till dessa returnerade data.

Om du vill komma åt returnerade data skapar du en separat regel och lägger sedan till en [!UICONTROL Send event complete]-händelse i regeln. Den här regeln aktiveras varje gång ett lyckat svar tas emot från servern som ett resultat av en [!UICONTROL Send event]-åtgärd.

När en [!UICONTROL Send event complete]-händelse utlöser en regel, innehåller den data som returneras från servern och som kan vara användbara för att utföra vissa åtgärder. Vanligtvis lägger du till en [!UICONTROL Custom code]-åtgärd (från tillägget [!UICONTROL Core]) i samma regel som innehåller händelsen [!UICONTROL Send event complete]. I åtgärden [!UICONTROL Custom code] får din anpassade kod åtkomst till en variabel som heter `event`. Den här `event`-variabeln innehåller data som returnerats från servern.

Din regel för att hantera data som returneras från Edge Network kan se ut ungefär så här:

![](assets/send-event-complete.png)

Nedan visas några exempel på hur du utför vissa uppgifter med åtgärden [!UICONTROL Custom code] i den här regeln.

### Återge anpassat innehåll manuellt

I åtgärden Anpassad kod, som är en regel för att hantera svarsdata, kan du komma åt personaliseringsförslag som returnerats från servern. Om du vill göra det skriver du följande egen kod:

```javascript
var propositions = event.propositions;
```

Om `event.propositions` finns är det en matris som innehåller objekt för personaliseringsförslag. Förslagen i arrayen bestäms till stor del av hur händelsen skickades till servern.

I det första scenariot antar vi att du inte har markerat kryssrutan [!UICONTROL Render decisions] och inte har tillhandahållit någon [!UICONTROL decision scopes] inuti åtgärden [!UICONTROL Send event] som ansvarar för att skicka händelsen.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

I det här exemplet innehåller arrayen `propositions` bara förslag som är relaterade till händelsen som är berättigade för automatisk återgivning.

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

När händelsen skickades markerades inte kryssrutan [!UICONTROL Render decisions], vilket innebar att SDK inte försökte återge något innehåll automatiskt. SDK hämtade dock fortfarande automatiskt det innehåll som kan återges automatiskt och skickade det till dig för manuell återgivning om du vill göra det. Observera att egenskapen `renderAttempted` har angetts till `false` för varje förslagsobjekt.

Om du i stället hade markerat kryssrutan [!UICONTROL Render decisions] när du skickade händelsen, skulle SDK ha försökt att återge alla förslag som är berättigade för automatisk återgivning. Därför skulle egenskapen `renderAttempted` för vart och ett av förslagsobjekten ha angetts till `true`. Du behöver inte återge dessa förslag manuellt i det här fallet.

Hittills har du bara tittat på innehåll som är kvalificerat för automatisk återgivning (till exempel innehåll som har skapats i Adobe Target Visual Experience Composer). Om du vill hämta anpassat innehåll _som inte_ är berättigat till automatisk återgivning begär du innehållet genom att ange beslutsomfattningar med hjälp av fältet [!UICONTROL Decision scopes] i åtgärden [!UICONTROL Send event]. Ett omfång är en sträng som identifierar ett visst förslag som du vill hämta från servern.

Åtgärden [!UICONTROL Send event] skulle se ut så här:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

I det här exemplet returneras och inkluderas i `propositions`-arrayen om det finns förslag på servern som matchar omfånget `salutation` eller `discount`. Observera att förslag som kvalificerar för automatisk återgivning kommer att fortsätta inkluderas i `propositions`-arrayen, oavsett hur du konfigurerar [!UICONTROL Render decisions] - eller [!UICONTROL Decision scopes]-fälten i [!UICONTROL Send event] -åtgärden. Arrayen `propositions` skulle i det här fallet se ut som i det här exemplet:

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

Nu kan du återge offertinnehåll när du vill. I det här exemplet är det förslag som matchar omfånget `discount` ett HTML-förslag som skapats med Adobe Target formulärbaserade Experience Composer. Anta att du har ett element på sidan med ID:t `daily-special` och vill återge innehållet från `discount`-utkastet till elementet `daily-special`. Gör följande:

1. Extrahera utdrag från objektet `event`.
1. Slinga igenom varje förslag och söker efter förslaget med omfånget `discount`.
1. Om du hittar ett förslag går du igenom varje objekt i utkastet och letar efter det objekt som innehåller HTML. (Det är bättre att kontrollera än att anta.)
1. Om du hittar ett objekt som innehåller innehåll från HTML söker du efter elementet `daily-special` på sidan och ersätter HTML med det anpassade innehållet.

Din egen kod i [!UICONTROL Custom code]-åtgärden kan se ut så här:

```javascript
var propositions = event.propositions;

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
```

### Åtkomst till Adobe Target svarstoken

Personalization-innehåll som returneras från Adobe Target innehåller [svarstoken](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=sv-SE), som är information om aktivitet, erbjudande, upplevelse, användarprofil, geoinformation med mera. Dessa uppgifter kan delas med verktyg från tredje part eller användas för felsökning. Svarstoken kan konfigureras i Adobe Target användargränssnitt.

I åtgärden Anpassad kod, som är en regel för att hantera svarsdata, kan du komma åt personaliseringsförslag som returnerats från servern. Om du vill göra det skriver du följande egen kod:

```javascript
var propositions = event.propositions;
```

Om `event.propositions` finns är det en matris som innehåller objekt för personaliseringsförslag. Mer information om innehållet i `result.propositions` finns i [Återge anpassat innehåll manuellt](#manually-render-personalized-content).

Anta att du vill samla in alla aktivitetsnamn från alla utkast som automatiskt renderades av web SDK och överföra dem till en enda array. Du kan sedan skicka den enskilda arrayen till en tredje part. I det här fallet skriver du egen kod inuti [!UICONTROL Custom code]-åtgärden till:

1. Extrahera utdrag från objektet `event`.
1. Slinga igenom varje förslag.
1. Avgör om SDK återgav förslaget.
1. I så fall gör du en slinga genom varje objekt i förslaget.
1. Hämta aktivitetsnamnet från egenskapen `meta`, som är ett objekt som innehåller svarstoken.
1. Placera aktivitetsnamnet i en array.
1. Skicka aktivitetsnamnen till en tredje part.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```

## [!UICONTROL Subscribe ruleset items] {#subscribe-ruleset-items}

Med händelsetypen **[!UICONTROL Subscribe ruleset items]** kan du prenumerera på Adobe Journey Optimizer-innehållskort för en yta. När reglerna utvärderas får det återanrop som ges till det här kommandot ett resultatobjekt med förslag som innehåller innehållskortets data.

![Bild av användargränssnittet för Experience Platform-taggar som visar händelsetypen för objekt i prenumerationsregeluppsättningen.](assets/subscribe-ruleset-items.png)

Den här händelsetypen stöder följande konfigurerbara egenskaper:

* **[!UICONTROL Schemas]**: En matris med scheman som du vill prenumerera på innehållskort för. Du kan ange scheman manuellt eller genom att ange ett dataelement.
* **[!UICONTROL Surfaces]**: En array med ytor som du vill prenumerera på innehållskort för. Du kan ange ytorna manuellt eller genom att ange ett dataelement.
