---
title: Samla in information om handel, produkter och beställningar med Adobe Experience Platform Web SDK
description: Lär dig hur du lägger till produktrelaterade data eller en kundvagn med Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Samla in information om handel, produkter och beställningar

Om din organisation säljer produkter eller tjänster kan du använda den här sidan som vägledning för hur du spårar dessa produkter och tjänster.

Den här sidan använder fältgruppen XDM [Commerce Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md).

Fältgruppen består av två huvuddelar:

* Objektet `commerce`. Med det här objektet kan du ange vilka åtgärder som ska utföras för `productListItems`-arrayen.
* Arrayen `productListItems`.

>[!TIP]
>
>Om du är bekant med Adobe Analytics innehåller objektet `commerce` data som liknar handelshändelser i variabeln `events`. Objektmatrisen `productListItems` innehåller data som liknar variabeln `products`.

## Objektet `commerce` {#commerce-object}

I det här avsnittet beskrivs de fält som är tillgängliga i objektet `commerce`.

>[!TIP]
>
>Ett mått har två fält: `id` och `value`. Oftast använder du bara fältet `value` (till exempel `'value':1`). I fältet `id` kan du ange en unik identifierare för spårning när måttet skickades. Mer information finns i XDM-dokumentationen för [Åtgärd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md).

| Mät | Rekommendation | Beskrivning |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Valfritt | En kundvagn är inte längre tillgänglig eller kan köpas av användaren. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Rekommenderas varmt | En användare söker inte längre efter produkter utan håller på att köpa en produkt. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Rekommenderas varmt | En produkt läggs till i en lista. Var noga med att ställa in produkten i `productListItems` samtidigt. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Valfritt | En ny produktlista skapas. Till exempel skapas en ny kundvagn. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Rekommenderas varmt | En produkt tas bort från en produktlista. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Valfritt | En produktlista återaktiveras av användaren. Detta sker ofta i återmarknadsföringskampanjer. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Rekommenderas varmt | En lista över produkter visas. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Rekommenderas varmt | En vy över en produkt har inträffat. Var noga med att ställa in produkten som visas i `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Rekommenderas varmt | En beställning godkänns. Måste ha en produktlista. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Valfritt | En produkt sparas för framtida bruk. |

{style="table-layout:auto"}

### `Commerce` objektexempel

Expandera avsnittet nedan om du vill se ett exempel på ett Web SDK-kommando med ett fält från objektet `commerce`.

+++`productViews`

Ett grundläggande SDK `sendEvent`-anrop för webben som anger att fältet `productViews` ska vara `1`:

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

+++

## Objektet `order` {#order-object}

Objektet `commerce` innehåller ett dedikerat objekt för att samla in orderinformation. Detta kallas `order`-objektet.

I det här avsnittet beskrivs alla fält som stöds av objektet `order`.

| Fält | Alternativ | Rekommendation | Beskrivning |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)-valutan för ordersumman. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Listan över betalningar på en order. En [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) innehåller följande. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Valfritt | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)-valutan för den här betalningsmetoden. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Rekommenderas varmt | Betalningens värde i den angivna valutakoden. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Rekommenderas varmt | Betalningstypen (till exempel `credit_card`, `gift_card`, `paypal`). Se listan med [kända värden](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) för mer information. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Valfritt | Ett unikt ID för den här betalningstransaktionen. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Rekommenderas varmt | Summan för den här ordern efter att alla rabatter och skatter har tillämpats. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Rekommenderas varmt | Den unika identifierare som säljaren har tilldelat det här köpet. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Valfritt | En unik identifierare som tilldelats av köparen för detta inköp. |

### Exempel på orderobjekt

Expandera avsnittet nedan om du vill se ett exempel på ett Web SDK-kommando som använder objektet `commerce`.

+++`Order` objektexempel

Ett Web SDK `sendEvent`-anrop som anger det `order` -objekt som gäller för flera produkter i `productListItems`-arrayen:

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

+++

## Produktlisteobjektet {#product-list-object}

Produktlistan anger vilka produkter som är relaterade till motsvarande åtgärd. Det är en lista med [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Varje produkt har flera valfria fält.

| Fält | Rekommendation | Beskrivning |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Valfritt | Produktens [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)-valuta. Det här fältet gäller vanligtvis bara när du har flera produkter i produktlistan med olika valutakoder. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Rekommenderas varmt | Ange bara det här fältet när det är tillämpligt. Det är till exempel inte möjligt att ange för `productView`-händelsen eftersom olika produktvarianter kan ha olika priser, men för en `productListAdds` -händelse. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Rekommenderas varmt | Produktens XDM-ID. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Rekommenderas varmt | Den metod som användes för att lägga till en produktartikel i listan av besökaren. Ange med `productListAdds` mått och används bara när en produkt läggs till i listan. Exempel är `add to cart button`, `quick add` och `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Rekommenderas varmt | Visningsnamnet eller produktens läsbara namn. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Rekommenderas varmt | Antalet enheter som kunden har angett att de behöver av produkten. Ska anges på `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` och så vidare. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Rekommenderas varmt | Lagringsenhet. Det är den unika identifieraren för produkten. |

### Exempel på produktlistor

Expandera avsnitten nedan om du vill se exempel på Web SDK-kommandon som använder objektet `productListItems`.

+++`productListItems`-exempel

Ett Web SDK `sendEvent`-anrop som anger `productViews` för flera produkter i `productListItems`-arrayen:

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

+++

+++`productListAdds`-exempel

Ett Web SDK `sendEvent`-anrop som anger `productListAdds`-händelsen för flera produkter i `productListItems`-arrayen:

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

+++

+++`checkouts`-exempel

Ett Web SDK `sendEvent`-anrop som anger `checkouts`-händelsen för flera produkter i `productListItems`-arrayen:

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

+++
