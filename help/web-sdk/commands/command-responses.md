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

Vissa Web SDK-kommandon kan returnera ett objekt som innehåller data som kan vara användbara för din organisation. Du kan välja vad du vill göra med dessa data. Kommandosvar är värdefulla för förslag och destinationer eftersom de kräver data från Edge Network för att fungera effektivt.

Kommandosvar använder JavaScript [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), som fungerar som proxy för ett värde som inte är känt när löftet skapas. När värdet är känt är löftet&quot;löst&quot; med värdet.

## Hantera kommandosvar med tillägget Web SDK-tagg

Skapa en regel som prenumererar på **[!UICONTROL Send event complete]**-händelsen som en del av en regel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Under [!UICONTROL Events] väljer du en befintlig händelse eller skapar en händelse.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Event Type] på **[!UICONTROL Send event complete]**.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

Du kan sedan inkludera åtgärderna **[!UICONTROL Apply propositions]** eller **[!UICONTROL Apply response]** i den här regeln.

1. När du visar regeln som skapats eller redigerats ovan väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Apply propositions]** eller **[!UICONTROL Apply response]**, beroende på önskat beteende.
1. Ange åtgärdens önskade fält och klicka sedan på **[!UICONTROL Keep Changes]**.

## Hantera kommandosvar med Web SDK JavaScript-biblioteket

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
