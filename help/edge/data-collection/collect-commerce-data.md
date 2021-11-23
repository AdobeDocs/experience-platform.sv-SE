---
title: Samla in handels- och produktinformation med Adobe Experience Platform Web SDK
description: Lär dig hur du lägger till produktrelaterade data eller en kundvagn med Adobe Experience Platform Web SDK.
keywords: produkter;handel;mått;mått;order;cartAbandons;checkouts;productListAdds;productListOpen;productListRemovals;productListReopens;productListViews;productViews;purchasing;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 22d15dde62f3113167684c7a76a2265e6f0e7bab
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 1%

---

# Samla in information om handel och produkter

Om du har produkter på din webbplats är detta en standarduppsättning med saker som du kanske vill skicka för att få ut så mycket som möjligt av Adobe. Även om detta är ett förslag ger det en mycket stark uppsättning data redan från början.

Det här dokumentet använder [Handelsinformation för ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) schemafältgrupp. The `commerce` fältgruppen är uppdelad i två delar: den `commerce` -objektet och `productListItems` array. The `commerce` kan du ange vilka åtgärder som ska utföras på `productListItems` array.

>[!TIP]
>
>Om du känner till Adobe Analytics kan du `commerce` är mest närbesläktad med `events` variabel. The `productListItems` är mer närbesläktat med `products` variabel.

## Åtgärder för produkter

Nedan finns en lista med `measures` finns i `commerce` -objekt.

>[!TIP]
>
>Ett mått har två fält: `id` och `value`. Oftast använder du `value` endast fält (till exempel `'value':1`). The `id` I kan du ange en unik identifierare som du kan använda för att hålla reda på när åtgärden skickades. Läs XDM-dokumentationen för [Mät](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Mät** | **Rekommendation** | **Beskrivning** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Valfritt | En kundvagn är inte längre tillgänglig eller kan köpas av användaren. |
| [utcheckningar](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Rekommenderas varmt | En användare söker inte längre efter produkter utan håller på att köpa en produkt. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Rekommenderas varmt | En produkt läggs till i en lista. Var noga med att ange produkten i `productListItems` samtidigt. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Valfritt | En ny produktlista skapas. (Till exempel skapas en ny kundvagn.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Rekommenderas varmt | En produkt tas bort från en produktlista. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Valfritt | En produktlista återaktiveras av användaren. Detta sker ofta i återmarknadsföringskampanjer. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Rekommenderas varmt | En lista över produkter visas. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Rekommenderas varmt | En vy över en produkt inträffade. Var noga med att ställa in produkten som den visas i `productListItems`. |
| [köp](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Rekommenderas varmt | En beställning godkänns. Måste ha en produktlista. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Valfritt | En produkt sparas för framtida bruk. |

Här är ett exempel på hur du ställer in dessa `Measures` i SDK.

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

Handelsobjektet har också ett särskilt fält för att samla in orderdetaljer som kallas `order`.

| **Order** | **Alternativ** | **Rekommendation** | **Beskrivning** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta för ordersumman. |
| [betalningar[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Listan över betalningar på en order. A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) innehåller följande: |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Valfritt | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta för betalningsmetoden. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Rekommenderas varmt | Betalningens värde i den angivna valutakoden. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Rekommenderas varmt | Betalningstyp (t.ex. `credit_card`, `gift_card`, `paypal`). Se listan med [kända värden](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) för mer information. |
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

Produktlistan anger vilka produkter som är relaterade till motsvarande åtgärd. Det är en lista på [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Varje produkt har ett antal valfria fält.

| **Fält** | **Rekommendation** | **Beskrivning** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Valfritt | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) för produkten. Detta är bara användbart när du kan ha produkter med olika valutakoder och när det gäller produkter. Exempel: när du köper eller lägger till i kundvagnen. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Rekommenderas varmt | Ska endast anges när det är tillämpligt. Det är till exempel inte möjligt att ställa in `productView` eftersom olika variationer av produkten kan ha olika priser, men på en `productListAdds`. |
| [produkt](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Rekommenderas varmt | Produktens XDM-ID. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Rekommenderas varmt | Den metod som användes för att lägga till en produktartikel i listan av besökaren. Använd `productListAdds` och bör endast användas när en produkt läggs till i förteckningen. Exempel `add to cart button`, `quick add`och `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Rekommenderas varmt | Detta anges som produktens visningsnamn eller läsbara namn. |
| [kvantitet](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Rekommenderas varmt | Antalet enheter som kunden har angett att de behöver av produkten. Bör anges `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`och så vidare. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Rekommenderas varmt | Lagringsenhet. Det är den unika identifieraren för produkten. |

## Exempel

`productViews` event

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

`productListAdds` event

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

`checkouts` event

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

`order` event

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
