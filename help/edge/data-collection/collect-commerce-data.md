---
title: Samla in information om handel, produkter och beställningar med Adobe Experience Platform Web SDK
description: Lär dig hur du lägger till produktrelaterade data eller en kundvagn med Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 1%

---

# Samla in information om handel, produkter och beställningar

Om din organisation säljer produkter eller tjänster kan du använda den här sidan som vägledning för hur du spårar dessa produkter och tjänster.

Den här sidan använder XDM [Commerce Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) fältgrupp.

Fältgruppen består av två huvuddelar:

* The `commerce` -objekt. Med det här objektet kan du ange vilka åtgärder som ska utföras för `productListItems` array.
* The `productListItems` array.

>[!TIP]
>
>Om du känner till Adobe Analytics kan du `commerce` objektet innehåller data som liknar e-handelshändelser i `events` variabel. The `productListItems` objektarrayen innehåller data som liknar `products` variabel.

## The `commerce` object {#commerce-object}

I det här avsnittet beskrivs fälten som finns i `commerce` -objekt.

>[!TIP]
>
>Ett mått har två fält: `id` och `value`. Oftast använder du bara `value` fält (till exempel `'value':1`). The `id` kan du ange en unik identifierare för spårning när måttet skickades. Läs XDM-dokumentationen för [Mät](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) för mer information.

| Mät | Rekommendation | Beskrivning |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Valfritt | En kundvagn är inte längre tillgänglig eller kan köpas av användaren. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Rekommenderas varmt | En användare söker inte längre efter produkter utan håller på att köpa en produkt. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Rekommenderas varmt | En produkt läggs till i en lista. Var noga med att ange produkten i `productListItems` samtidigt. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Valfritt | En ny produktlista skapas. Till exempel skapas en ny kundvagn. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Rekommenderas varmt | En produkt tas bort från en produktlista. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Valfritt | En produktlista återaktiveras av användaren. Detta sker ofta i återmarknadsföringskampanjer. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Rekommenderas varmt | En lista över produkter visas. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Rekommenderas varmt | En vy över en produkt har inträffat. Var noga med att ställa in produkten som den visas i `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Rekommenderas varmt | En beställning godkänns. Måste ha en produktlista. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Valfritt | En produkt sparas för framtida bruk. |

{style="table-layout:auto"}

### `Commerce` objektexempel

Expandera avsnittet nedan för att se ett exempel på ett Web SDK-kommando med ett fält från `commerce` -objekt.

+++`productViews`

En grundläggande SDK för webben `sendEvent` anrop `productViews` fält till `1`:

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

## The `order` object {#order-object}

The `commerce` -objektet innehåller ett dedikerat objekt för att samla in orderinformation. Detta kallas för `order` -objekt.

I det här avsnittet beskrivs alla fält som stöds av `order` -objekt.

| Fält | Alternativ | Rekommendation | Beskrivning |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta för ordersumman. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Listan över betalningar på en order. A [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) innehåller följande: |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Valfritt | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta för betalningsmetoden. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Rekommenderas varmt | Betalningens värde i den angivna valutakoden. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Rekommenderas varmt | Betalningstyp (till exempel `credit_card`, `gift_card`, `paypal`). Se listan med [kända värden](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) för mer information. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Valfritt | Ett unikt ID för den här betalningstransaktionen. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Rekommenderas varmt | Summan för den här ordern efter att alla rabatter och skatter har tillämpats. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Rekommenderas varmt | Den unika identifierare som säljaren har tilldelat det här köpet. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Valfritt | En unik identifierare som tilldelats av köparen för detta inköp. |

### Exempel på orderobjekt

Expandera avsnittet nedan för att se ett exempel på ett Web SDK-kommando med `commerce` -objekt.

+++`Order` objektexempel

En Web SDK `sendEvent` anrop `order` objekt som gäller för flera produkter i `productListItems` array:

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

Produktlistan anger vilka produkter som är relaterade till motsvarande åtgärd. Det är en lista på [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Varje produkt har flera valfria fält.

| Fält | Rekommendation | Beskrivning |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Valfritt | The [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) produktvaluta. Det här fältet gäller vanligtvis bara när du har flera produkter i produktlistan med olika valutakoder. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Rekommenderas varmt | Ange bara det här fältet när det är tillämpligt. Det är till exempel inte möjligt att ställa in `productView` -händelse eftersom olika variationer av produkten kan ha olika priser, men på en `productListAdds` -händelse. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Rekommenderas varmt | Produktens XDM-ID. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Rekommenderas varmt | Den metod som användes för att lägga till en produktartikel i listan av besökaren. Använd med `productListAdds` och används endast när en produkt läggs till i listan. Exempel: `add to cart button`, `quick add`och `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Rekommenderas varmt | Visningsnamnet eller produktens läsbara namn. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Rekommenderas varmt | Antalet enheter som kunden har angett att de behöver av produkten. Bör anges `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`och så vidare. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Rekommenderas varmt | Lagringsenhet. Det är den unika identifieraren för produkten. |

### Exempel på produktlistor

Expandera avsnitten nedan om du vill se exempel på Web SDK-kommandon med `productListItems` -objekt.

+++`productListItems` exempel

En Web SDK `sendEvent` anrop `productViews` för flera produkter i `productListItems` array:

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

+++`productListAdds` exempel

En Web SDK `sendEvent` anrop `productListAdds` händelse för flera produkter i `productListItems` array:

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

+++`checkouts` exempel

En Web SDK `sendEvent` anrop `checkouts` händelse för flera produkter i `productListItems` array:

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
