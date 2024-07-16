---
title: getIdentity
description: Hämta en besökares identitet utan att skicka händelsedata.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# `getIdentity`

Med kommandot `getIdentity` kan du hämta ett besökar-ID utan att skicka händelsedata. När du kör kommandot `sendEvent` får Web SDK automatiskt besökarens identitet om en sådan inte redan finns.

Om du behöver separata anrop för att generera ett besökar-ID och skicka data kan du använda det här kommandot.

## Hämta identitet med taggtillägget Web SDK

Det här kommandot finns inte i taggtillägget för Web SDK via taggtilläggets användargränssnitt. Använd den anpassade kodredigeraren med JavaScript bibliotekssyntax.

## Hämta identitet med Web SDK JavaScript-biblioteket

Kör kommandot `getIdentity` när du anropar den konfigurerade instansen av Web SDK. Följande alternativ är tillgängliga när du konfigurerar det här kommandot:

* **`namespaces`**: En array med namnutrymmen. Standardvärdet är `["ECID"]`. Giltiga värden är `["ECID"]`, `null` eller `undefined`.
* **`edgeConfigOverrides`**: Ett [datastream-konfigurationsåsidosättningsobjekt](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Svarsobjekt

Om du bestämmer dig för att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`identity.ECID`**: En sträng som innehåller besökarens ECID.
* **`edge.regionID`**: Ett heltal som representerar regionen Edge Network som webbläsaren träffar på när en identitet hämtas. Det är samma sak som det gamla platstipset för Audience Manager.
