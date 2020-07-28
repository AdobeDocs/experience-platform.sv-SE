---
title: Utföra kommandon
seo-title: Kör Adobe Experience Platform Web SDK-kommandon
description: Lär dig hur du kör Experience Platform Web SDK-kommandon
seo-description: Lär dig hur du kör Experience Platform Web SDK-kommandon
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Utföra kommandon

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
  .then(function(result) {
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
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

### Svarsobjekt

Alla löften som returneras från kommandon löses med ett `result` objekt. Resultatobjektet kommer att innehålla data beroende på kommandot och användarens samtycke. Biblioteksinformation skickas till exempel som en egenskap för resultatobjektet i följande kommando.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(results.libraryInfo.version);
});
```

### Godkännande

Om en användare inte har gett sitt samtycke för ett visst ändamål kommer löftet fortfarande att lösas. Svarsobjektet kommer dock endast att innehålla den information som kan anges i kontexten för det som användaren har godkänt.
