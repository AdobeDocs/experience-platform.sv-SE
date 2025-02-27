---
title: appendIdentityToUrl
description: Leverera personaliserade upplevelser mer exakt mellan appar, webben och olika domäner.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 7c262e5819f8e3488c5ddd5a0221d1c52c28c029
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# `appendIdentityToUrl`

Med kommandot `appendIdentityToUrl` kan du lägga till en användaridentifierare i URL:en som en frågesträng. Den här åtgärden gör att du kan föra en besökares identitet mellan domäner, vilket förhindrar att besökarantal dupliceras för datauppsättningar som innehåller både domäner och kanaler. Det finns på Web SDK version 2.11.0 eller senare.

Frågesträngen som genereras och läggs till i URL:en är `adobe_mc`. Om Web SDK inte kan hitta ett ECID, anropas slutpunkten `/acquire` för att generera ett.

>[!NOTE]
>
>Om samtycke inte har angetts returneras URL:en från den här metoden oförändrad. Det här kommandot körs omedelbart, det väntar inte på någon uppdatering av medgivandet.

## Bifoga identitet till URL med Web SDK-tillägget {#extension}

En URL-adress läggs till som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Redirect with identity]**.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

Det här kommandot används vanligtvis med en viss regel som lyssnar efter klickningar och kontrollerar vilka domäner du vill använda.

+++Villkor för regelhändelse

Utlöses när någon klickar på en ankartagg med egenskapen `href`.

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

## Bifoga identitet till URL med hjälp av SDK Web-biblioteket

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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Svarsobjekt

Om du bestämmer dig för att [hantera svar](command-responses.md) med det här kommandot innehåller svarsobjektet **`url`**, den nya URL-adressen med identitetsinformation som lagts till som en frågesträngsparameter.
