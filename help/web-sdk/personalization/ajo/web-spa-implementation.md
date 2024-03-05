---
title: Programimplementering på en sida
description: Lär dig implementera SPA i Adobe Journey Optimizer
exl-id: 1883251b-2d59-46d3-ac74-b8657edd0325
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Implementera single-page-applikationer (SPA) {#web-spa-implementation}

Adobe Experience Platform Web SDK innehåller många funktioner som gör det möjligt för ditt företag att utföra personalisering på nästa generations klientteknik, som enkelsidiga program (SPA).

Traditionella webbplatser fungerar på&quot;sida-till-sida&quot;-navigeringsmodeller, som annars kallas flersidiga program, där webbplatsdesignen är nära kopplad till URL:er och övergångar mellan webbsidor kräver en sidladdning.

Moderna webbprogram, som appar för en sida (SPA), har i stället antagit en modell som möjliggör snabb användning av webbläsargränssnittsåtergivning, som ofta är oberoende av sidomladdning. De här upplevelserna kan triggas av kundinteraktioner som rullningar, klick och markörrörelser. I takt med att de moderna webbens paradigmer har utvecklats fungerar inte längre de traditionella generiska eventernas relevans, till exempel en sidladdning, för personalisering och experimenterande.

![Sidlivscykeldiagram.](assets/web-spa-vs-traditional-lifecycle.png)

## Fördelar med att använda Web SDK för SPA {#web-spa-benefits}

Nedan följer några fördelar med att använda Web SDK för dina enkelsidiga program:

* Möjlighet att cachelagra alla erbjudanden vid sidinläsning för att minska antalet serveranrop till ett enda serveranrop.
* Förbättra användarupplevelsen på webbplatsen avsevärt eftersom erbjudandena visas direkt via cachen, utan den fördröjning som traditionella serveranrop ger.
* Med en enda utvecklingsmiljö kan marknadsförarna skapa och köra personaliserings- och experimenteringsaktiviteter via den visuella Adobe Journey Optimizer Web Editor på SPA.

## XDM-vyer och enkelsidiga program {#web-spa-xdm}

Journey Optimizer webbeditor utnyttjar konceptet _vyer_.

Vyer är en logisk grupp av visuella element som tillsammans utgör en SPA upplevelse. Ett enkelsidigt program kan därför betraktas som en övergång genom vyer i stället för URL-adresser som baseras på användarinteraktioner. En vy kan vanligtvis representera en hel webbplats, en enstaka sida eller grupperade visuella element på en sida.

I följande exempel används en hypotetisk e-handelssajt online för att ytterligare förklara vad som är vyer.

* När du har navigerat till hemsidan befordrar en hjältebild både säsongssamlingar och de olika produktkataloger som finns på webbplatsen. I det här fallet kan en vy definieras för hela hemskärmen. Den här vyn kan helt enkelt kallas &quot;hem&quot;.

  ![Exempel på en webbsida som visar en hemsida.](assets/web-spa-home.png)

* När kunden blir mer intresserad av de produkter som företaget säljer bestämmer de sig för att klicka på **Män** länk. Liknar startsidan, hela **Män** kan definieras som en vy. Den här vyn kan heta &quot;men&quot;.

  ![Exempel på en webbbild som visar en viss vy.](assets/web-spa-men.png)

* Eftersom en vy kan definieras som en hel webbplats eller som en grupp visuella element på en webbplats, kan de fyra produkter som visas på produktwebbplatsen grupperas och betraktas som en vy. Den här vyn kan heta &quot;products&quot;.

  ![Exempel på en webbbild som visar en viss vy.](assets/web-spa-men-products.png)

* När kunden bestämmer sig för att klicka på **ALLA MÄN** om du vill utforska fler produkter på webbplatsen ändras inte webbplatsens URL i det här fallet, men här kan du skapa en vy som bara representerar den andra produktraden som visas. Vynamnet kan vara&quot;products-page-2&quot;.

* Kunden bestämmer sig för att köpa några produkter från sajten och går vidare till kassan. Själva kundvagnsskärmen kan associeras med en vy med namnet &quot;cart&quot;. Du kan också ha en annan vy i utcheckningsfönstret för att hantera de rekommenderade produkterna nedan.

  ![Exempel på en webbbild som visar en viss vy.](assets/web-spa-cart.png)

Konceptet med vyer kan utvidgas mycket mer än så. Detta är bara några exempel på vyer som kan definieras på en webbplats.

## Implementera XDM-vyer {#implement-xdm-views}

XDM-vyer kan användas i Adobe Journey Optimizer för att marknadsförarna ska kunna köra webbpersonaliserings- och experimenteringskampanjer på SPA via Journey Optimizer webbredigerare.

Detta kräver att du utför följande steg för att slutföra en engångsinstallation av en utvecklare:

1. Installera [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md) och kontrollera [krav på webbkanal](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html) sida.

2. Avgör alla XDM-vyer i ditt enkelsidiga program som du vill anpassa.

3. När du har definierat XDM-vyerna måste du implementera `sendEvent()` function with `renderDecisions` ange till `true` och motsvarande XDM-vy i enkelsidigt program. XDM-vyn måste skickas `xdm.web.webPageDetails.viewName`. I det här steget kan marknadsförarna identifiera dessa vyer inifrån Journey Optimizer webbredigerare och använda innehållsändringar för dem:

```js
 alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
   "web": {
    "webPageDetails": {
    "viewName":"home"
   }
  }
 }
});
```

>[!NOTE]
>
>På första `sendEvent()` anrop kommer alla XDM-vyer som ska återges för slutanvändaren att hämtas och cachelagras. Efterföljande `sendEvent()` anrop med skickade XDM-vyer läses från cachen och återges utan ett serveranrop.

## `sendEvent()` funktionsexempel

I det här avsnittet beskrivs två exempel som visar hur du anropar `sendEvent()` i React för en hypotetisk SPA.

### Exempel 1: A/B-teststartsida {#web-spa-sample-1}

Marknadsföringsteamet vill köra A/B-tester på hela hemsidan.

![Exempelsida för enkelsidigt program.](assets/web-spa-home.png)

För att köra A/B-tester på hela hemplatsen `sendEvent()` måste anropas med XDM `viewName` ange till `home`:

```js
function onViewChange() {

  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

  viewName = viewName || 'home'; // view name cannot be empty

  // Sanitize viewName to get rid of any trailing symbols derived from URL

  if (viewName.startsWith('#') || viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }

  alloy("sendEvent", {
    "renderDecisions": true,

    "xdm": {
      "web": {
        "webPageDetails": {
          "viewName":"home"
        }
      }
    }
  });
}

// react router v4

const history = syncHistoryWithStore(createBrowserHistory(), store);

history.listen(onViewChange);

// react router v3

<Router history={hashHistory} onUpdate={onViewChange} >
```

### Exempel 2: Personaliserade produkter {#web-spa-sample-2}

Marknadsföringsteamet vill personalisera den andra produktraden genom att ändra prisetikettens färg till röd efter att användaren har klickat för att se alla Men-produkter.

![En exempelsida med skräddarsydda produkter.](assets/web-spa-men-products.png)

```js
function onViewChange(viewName) {

    alloy("sendEvent", {
        "renderDecisions": true,
        "xdm": {
            "web": {
                "webPageDetails": {
                    "viewName": viewName
                }
            }
        }
    });
}

class Products extends Component {

    render() {
        return (

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
