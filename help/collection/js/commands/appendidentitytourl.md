---
title: appendIdentityToUrl
description: Leverera personaliserade upplevelser mer exakt mellan appar, webben och olika domäner.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

Med kommandot `appendIdentityToUrl` kan du lägga till en användaridentifierare i URL:en som en frågesträng. Den här åtgärden gör att du kan föra en besökares identitet mellan domäner, vilket förhindrar att besökarantal dupliceras för datauppsättningar som innehåller både domäner och kanaler. Det finns på Web SDK version 2.11.0 eller senare.

Frågesträngen som genereras och läggs till i URL:en är `adobe_mc`. Om Web SDK inte kan hitta ett ECID, anropas slutpunkten `/acquire` för att generera ett.

>[!NOTE]
>
>Om samtycke inte har angetts returneras URL:en från den här metoden oförändrad. Det här kommandot körs omedelbart, det väntar inte på någon uppdatering av medgivandet.

Kör kommandot `appendIdentityToUrl` med en URL som parameter. Metoden returnerar en URL med identifieraren tillagd som en frågesträng.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

Du kan lägga till en händelseavlyssnare för alla klick som tas emot på sidan och kontrollera om URL:en matchar önskade domäner. Om den gör det lägger du till identiteten i URL:en och dirigerar om användaren.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Det här kommandot stöder objektet [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Svarsobjekt

När [hanterar svar](command-responses.md) med det här kommandot innehåller svarsobjektet **`url`**, den nya URL-adressen med identitetsinformation som lagts till som en frågesträngsparameter.

## Lägg till identitet i URL med hjälp av taggtillägget Web SDK

Webbtaggtillägget för SDK som motsvarar det här kommandot är åtgärden [Omdirigera med identitet](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
