---
title: Utföra kommandon
seo-title: Använda SDK-kommandon för Adobe Experience Platform
description: Lär dig hur du kör Experience Platform Web SDK-kommandon
seo-description: Lär dig hur du kör Experience Platform Web SDK-kommandon
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Kör kommandon

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

När baskoden har implementerats på webbsidan kan du börja köra kommandon med SDK:n. Du behöver inte vänta på att den externa filen \(`alloy.js`\) ska läsas in från servern innan du kör kommandon. Om SDK inte har lästs in helt köas och bearbetas kommandona av SDK så snart som möjligt.

Kommandon körs med följande syntax.

```javascript
alloy("commandName", options);
```

SDK-koden anger `commandName` vad som ska göras, medan `options` det är parametrar och data som du vill skicka till ett kommando. Eftersom de tillgängliga alternativen är beroende av kommandot bör du läsa dokumentationen för mer information om varje kommando.

## Ett meddelande om löften

[Utfästelser](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) är grundläggande för hur SDK kommunicerar med koden på din webbsida. Ett löfte är en vanlig programmeringsstruktur som inte är specifik för denna SDK eller ens JavaScript. Ett löfte fungerar som en proxy för ett värde som inte är känt när löftet skapas. När värdet är känt är löftet&quot;löst&quot; med värdet. Hanterarfunktioner kan kopplas till ett löfte, så att du kan meddelas när löftet har lösts eller när ett fel har uppstått under lösningsprocessen. Om du vill veta mer om löften kan du läsa [den här självstudiekursen](https://javascript.info/promise-basics) eller andra resurser på webben.

## Hantera lyckade eller misslyckade

Varje gång ett kommando körs returneras ett löfte. Löftet representerar det slutliga slutförandet av kommandot. I exemplet nedan kan du använda `then` - och `catch` -metoder för att avgöra när kommandot har slutförts eller misslyckats.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Om det inte är viktigt för dig att veta när kommandot är klart, kan du ta bort `then` samtalet.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

På samma sätt kan du ta bort `catch` samtalet om du inte vet när kommandot misslyckas.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Utelämna fel

Om löftet avvisas och du inte har lagt till något `catch` samtal,&quot;bubblar upp&quot;-felet och loggas i webbläsarens utvecklarkonsol, oavsett om loggning är aktiverat i Adobe Experience Platform Web SDK. Om detta är något som du vill ta hänsyn till kan du ange att konfigurationsalternativet ska vara `suppressErrors` så som beskrivs i `true` Konfigurera SDK [](configuring-the-sdk.md).
