---
title: appendIdentityToUrl
description: Leverera personaliserade upplevelser mer exakt mellan appar, webben och olika domäner.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# `appendIdentityToUrl`

The `appendIdentityToUrl` kan du lägga till en användaridentifierare till URL:en som en frågesträng. Den här åtgärden gör att du kan föra en besökares identitet mellan domäner, vilket förhindrar att besökarantal dupliceras för datauppsättningar som innehåller både domäner och kanaler. Det finns på Web SDK version 2.11.0 eller senare.

Frågesträngen som genereras och läggs till i URL:en är `adobe_mc`. Om Web SDK inte kan hitta ett ECID anropas `/acquire` slutpunkt för att generera en.

>[!NOTE]
>
>Om samtycke inte har angetts returneras URL:en från den här metoden oförändrad. Det här kommandot körs omedelbart, det väntar inte på någon uppdatering av medgivandet.

## Lägg till identitet i URL med hjälp av Web SDK-tillägget

En URL-adress läggs till som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Redirect with identity]**.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

Det här kommandot används vanligtvis med en viss regel som lyssnar efter klickningar och kontrollerar vilka domäner du vill använda.

+++Villkor för regelhändelse

Utlöses när en ankartagg med en `href` -egenskapen klickas.

* **[!UICONTROL Extension]**: Kärna
* **[!UICONTROL Event type]**: Klicka
* **[!UICONTROL When the user clicks on]**: Specifika element
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Regelhändelse](../assets/id-sharing-event-configuration.png)

+++

+++Regelvillkor

Utlöses bara på önskade domäner.

* **[!UICONTROL Logic type]**: Normal
* **[!UICONTROL Extension]**: Kärna
* **[!UICONTROL Condition Type]**: Värdejämförelse
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Matchar Regex
* **[!UICONTROL Right Operand]**: Ett reguljärt uttryck som matchar de önskade domänerna. Exempel: `adobe.com$|behance.com$`

![Regelvillkor](../assets/id-sharing-condition-configuration.png)

+++

+++Regelåtgärd

Lägg till identiteten i URL:en.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Omdirigera med identitet

![Regelåtgärd](../assets/id-sharing-action-configuration.png)

+++

## Lägg till identitet i URL med JavaScript-biblioteket för Web SDK

Kör `appendIdentityToUrl` med en URL som parameter. Metoden returnerar en URL med identifieraren tillagd som en frågesträng.

```js
alloy("appendIdentityToUrl",document.location);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Svarsobjekt

Om du väljer att [hantera svar](command-responses.md) med det här kommandot innehåller svarsobjektet **`url`**, den nya URL-adressen med identitetsinformation som har lagts till som en frågesträngsparameter.
