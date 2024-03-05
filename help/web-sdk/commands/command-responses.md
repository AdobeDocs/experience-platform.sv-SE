---
title: Hantera kommandosvar
description: Hantera svar från kommandon med JavaScript-löften.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Hantera kommandosvar

Vissa Web SDK-kommandon kan returnera ett objekt som innehåller data som kan vara användbara för din organisation. Du kan välja vad du vill göra med dessa data. Kommandosvar är värdefulla för förslag och mål eftersom de kräver Edge Network-data för att fungera effektivt.

Kommandosvar använder JavaScript [löften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), fungerar som en proxy för ett värde som inte är känt när löftet skapas. När värdet är känt är löftet&quot;löst&quot; med värdet.

## Hantera kommandosvar med tillägget Web SDK-tagg

Skapa en regel som prenumererar på **[!UICONTROL Send event complete]** -händelse som en del av en regel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Events]väljer du en befintlig händelse eller skapar en händelse.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Event Type] till **[!UICONTROL Send event complete]**.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

Du kan sedan inkludera åtgärderna **[!UICONTROL Apply propositions]** eller **[!UICONTROL Apply response]** till den här regeln.

1. När du visar regeln som skapats eller redigerats ovan väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Apply propositions]** eller **[!UICONTROL Apply response]**, beroende på önskat beteende.
1. Ange åtgärdens önskade fält och klicka sedan på **[!UICONTROL Keep Changes]**.

## Hantera kommandosvar med JavaScript-biblioteket för Web SDK

Använd `then` och `catch` metoder för att avgöra när ett kommando lyckas eller misslyckas. Du kan antingen utelämna `then` eller `catch` om deras syften inte är viktiga för er implementering.

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

Alla löften som returneras från kommandon använder en `result` -objekt. Du kan till exempel hämta biblioteksinformation från `result` objekt med [`getLibraryInfo`](getlibraryinfo.md) kommando:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Innehållet i `result` -objektet är beroende av en kombination av vilket kommando du använder och användarens samtycke. Om en användare inte har gett sitt samtycke för ett visst ändamål innehåller svarsobjektet endast information som kan ges i samband med vad användaren har gett sitt samtycke till.
