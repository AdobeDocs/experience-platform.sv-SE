---
title: Samla in handels- och produktinformation med Adobe Experience Platform Web SDK
description: Lär dig hur du lägger till produktrelaterade data eller en kundvagn med Adobe Experience Platform Web SDK.
keywords: produkter;handel;mått;mått;order;cartAbandons;checkouts;productListAdds;productListOpen;productListRemovals;productListReopens;productListViews;productViews;purchasing;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseNumber;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---


# Samla in information om handel och produkter

Om du har produkter på din webbplats är detta en standarduppsättning med saker som du kanske vill skicka för att få ut så mycket som möjligt av Adobe. Även om detta är ett förslag ger det en mycket stark uppsättning data redan från början.

Det här dokumentet använder [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)-mixen. `commerce`-blandningen delas upp i två delar: `commerce`-objektet och `productListItems`-arrayen. Med `commerce`-objektet kan du ange vilka åtgärder som ska utföras för `productListItems`-arrayen.

>[!TIP]
>
>Om du känner till Adobe Analytics är `commerce` mest närbesläktat med variabeln `events`. `productListItems` är närmare relaterat till variabeln `products`.

## Åtgärder för produkter

Nedan finns en lista med `measures` som är tillgänglig i `commerce`-objektet.

>[!TIP]
>
>Ett mått har två fält: `id` och `value`. För det mesta kommer du endast att använda fältet `value` (till exempel `'value':1`). I fältet `id` kan du ange en unik identifierare som du kan använda för att hålla reda på när måttet skickades. Se XDM-dokumentationen för [Mät](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Mät** | **Rekommendation** | **Beskrivning** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Valfritt | En kundvagn är inte längre tillgänglig eller kan köpas av användaren. |
| [utcheckningar](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Rekommenderas varmt | En användare söker inte längre efter produkter utan håller på att köpa en produkt. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Rekommenderas varmt | En produkt läggs till i en lista. Var noga med att ställa in produkten i `productListItems` samtidigt. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Valfritt | En ny produktlista skapas. (Till exempel skapas en ny kundvagn.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Rekommenderas varmt | En produkt tas bort från en produktlista. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Valfritt | En produktlista återaktiveras av användaren. Detta sker ofta i återmarknadsföringskampanjer. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Rekommenderas varmt | En lista över produkter visas. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Rekommenderas varmt | En vy över en produkt inträffade. Var noga med att ange att produkten ska visas i `productListItems`. |
| [köp](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Rekommenderas varmt | En beställning godkänns. Måste ha en produktlista. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Valfritt | En produkt sparas för framtida bruk. |

Här är ett exempel på hur du ställer in dessa `Measures` i SDK:n.

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

Handelsobjektet har också ett särskilt fält för att samla in orderinformation som kallas `order`.

| **Order** | **Alternativ** | **Rekommendation** | **Beskrivning** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Valutan [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) för ordersumman. |
| [betalningar[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Listan över betalningar på en order. En [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) innehåller följande: |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Valfritt | Valutan [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) för den här betalningsmetoden. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Rekommenderas varmt | Betalningens värde i den angivna valutakoden. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Rekommenderas varmt | Betalningstypen (till exempel `credit_card`, `gift_card`, `paypal`). Se listan med [kända värden](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) för mer information. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Valfritt | Ett unikt ID för den här betalningstransaktionen. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Rekommenderas varmt | Summan för den här ordern efter att alla rabatter och skatter har tillämpats. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Mycket rekommenderat | Den unika identifierare som säljaren har tilldelat det här köpet. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Valfritt | En unik identifierare som tilldelats av köparen för detta inköp. |

Här är ett exempel på ett vanligt köp i SDK.

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

## Produktlistor

Produktlistan anger vilka produkter som är relaterade till motsvarande åtgärd. Det är en lista med [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Varje produkt har ett antal valfria fält.

| **Fält** | **Rekommendation** | **Beskrivning** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Valfritt | Produktens [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)-valuta. Detta är bara användbart när du kan ha produkter med olika valutakoder och när det gäller produkter. Exempel: när du köper eller lägger till i kundvagnen. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Rekommenderas varmt | Ska endast anges när det är tillämpligt. Det är till exempel inte möjligt att ange `productView` eftersom olika varianter av produkten kan ha olika priser, men på en `productListAdds`. |
| [produkt](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Rekommenderas varmt | Produktens XDM-ID. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Rekommenderas varmt | Den metod som användes för att lägga till en produktartikel i listan av besökaren. Anges med `productListAdds`-mått och ska endast användas när en produkt läggs till i listan. Exempel är `add to cart button`, `quick add` och `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Rekommenderas varmt | Detta anges som produktens visningsnamn eller läsbara namn. |
| [kvantitet](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Rekommenderas varmt | Antalet enheter som kunden har angett att de behöver av produkten. Ska anges på `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` och så vidare. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Rekommenderas varmt | Lagringsenhet. Det är den unika identifieraren för produkten. |

## Exempel

`productView` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

`productView` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

`checkout` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

`purchase` event

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```
