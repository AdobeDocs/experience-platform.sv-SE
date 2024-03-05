---
title: getIdentity
description: Hämta en besökares identitet utan att skicka händelsedata.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# `getIdentity`

The `getIdentity` kan du hämta ett besökar-ID utan att skicka händelsedata. När du kör `sendEvent` så får Web SDK automatiskt besökarens identitet om en sådan inte redan finns.

Om du behöver separata anrop för att generera ett besökar-ID och skicka data kan du använda det här kommandot.

## Hämta identitet med taggtillägget Web SDK

Det här kommandot finns inte i taggtillägget för Web SDK via taggtilläggets användargränssnitt. Använd den anpassade kodredigeraren med JavaScript-bibliotekssyntax.

## Hämta identitet med Web SDK JavaScript-biblioteket

Kör `getIdentity` när du anropar den konfigurerade instansen av Web SDK. Följande alternativ är tillgängliga när du konfigurerar det här kommandot:

* **`namespaces`**: En array med namnutrymmen. Standardvärdet är `["ECID"]`. Giltiga värden är `["ECID"]`, `null`, eller `undefined`.
* **`edgeConfigOverrides`**: An [åsidosättningsobjekt för datastream-konfiguration](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Svarsobjekt

Om du väljer att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`identity.ECID`**: En sträng som innehåller besökarens ECID.
* **`edge.regionID`**: Ett heltal som representerar Edge Network-regionen som webbläsaren stöter på när en identitet hämtas. Det är samma sak som det gamla platstipset för Audience Manager.
