---
title: getIdentity
description: Hämta en besökares identitet utan att skicka händelsedata.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 5f8a9938eaccfd2eeabc75c56608f11819a81ffa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# `getIdentity`

När du kör kommandot [`sendEvent`](sendevent/overview.md) får Web SDK automatiskt besökarens identitet om det inte redan finns någon.

Med kommandot `getIdentity` kan du hämta ett besökar-ID utan att skicka händelsedata.

Om du behöver separata anrop för att generera ett besökar-ID och skicka data kan du använda det här kommandot.

Kommandot `getIdentity` går igenom följande flöde för att hämta `ECID`.

1. Du använder Web SDK för att anropa antingen `getIdentity` eller [`appendIdentityToUrl`](appendidentitytourl.md).
1. Web SDK väntar på medgivande.
1. Web SDK kontrollerar om namnområdet `ECID` begärdes för anropet. Som standard inkluderas alltid namnutrymmet `ECID`.
1. Web SDK läser cookien `kndctr` och returnerar dess värde som `ECID`, om det finns. Detta returnerar bara värdet `ECID`, men inte värdet `regionId`.
1. Om identitetscookien `kndctr` inte har angetts eller namnområdet `"CORE"` har begärts, skickar Web SDK en begäran till Edge Network.
1. Edge Network returnerar både `ECID` och `regionId` (och `CORE ID`, om det begärs).

## Hämta identitet med taggtillägget Web SDK

SDK-taggtillägget för webben erbjuder inte det här kommandot via taggtilläggets användargränssnitt. Använd den anpassade kodredigeraren med JavaScript bibliotekssyntax.

## Hämta identitet med Web SDK JavaScript-biblioteket

Kör kommandot `getIdentity` när du anropar den konfigurerade instansen av Web SDK. Följande alternativ är tillgängliga när du konfigurerar det här kommandot:

* **`namespaces`**: En array med namnutrymmen. Standardvärdet är `["ECID"]`. Andra värden som stöds är:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  Du kan begära [!DNL ECID] och [!DNL CORE ID] samtidigt. Exempel: `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`**: Ett [datastream-konfigurationsåsidosättningsobjekt](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Svarsobjekt

Om du bestämmer dig för att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`identity.ECID`**: En sträng som innehåller besökarens ECID.
* **`identity.CORE`**: En sträng som innehåller besökarens CORE ID.
* **`edge.regionID`**: Ett heltal som representerar den Edge Network-region som webbläsaren stötte på när en identitet hämtades. Det är samma som det gamla Audience Manager positioneringstipset.
