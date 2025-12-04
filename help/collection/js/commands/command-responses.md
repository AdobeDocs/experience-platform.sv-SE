---
title: Hantera kommandosvar
description: Hantera svar från kommandon med JavaScript-löften.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Hantera kommandosvar

Vissa Web SDK-kommandon kan returnera ett objekt som innehåller data som kan vara användbara för din organisation. Du kan välja vad du vill göra med dessa data. Kommandosvar är värdefulla för förslag och destinationer eftersom de kräver att Edge Network data fungerar effektivt.

Kommandosvar använder JavaScript [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), som fungerar som proxy för ett värde som inte är känt när löftet skapas. När värdet är känt är löftet&quot;löst&quot; med värdet.

Använd metoderna `then` och `catch` för att avgöra när ett kommando lyckas eller misslyckas. Du kan utelämna antingen `then` eller `catch` om deras syften inte är viktiga för implementeringen.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Alla löften som returneras från kommandon använder ett `result`-objekt. Du kan till exempel hämta biblioteksinformation från objektet `result` med kommandot [`getLibraryInfo`](getlibraryinfo.md):

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Innehållet i det här `result`-objektet beror på en kombination av vilka kommandon du använder och användarens samtycke. Om en användare inte har gett sitt samtycke för ett visst ändamål innehåller svarsobjektet endast information som kan ges i samband med vad användaren har gett sitt samtycke till.

## Kommandosvar med taggtillägget Web SDK

SDK-taggtillägget för webben som motsvarar kommandosvaren är en regel som prenumererar på händelsen [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete). Du kan sedan inkludera åtgärder som [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) eller [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) till den här regeln.
