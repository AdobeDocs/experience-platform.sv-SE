---
title: Kör Adobe Experience Platform Web SDK-kommandon
description: Lär dig hur du kör Experience Platform Web SDK-kommandon
keywords: Kör kommandon;commandName;Promises;getLibraryInfo;response objects;medgivande;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ffc60e83285188bc5b0f6eb7a20fafee16d51d4d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Kör kommandon


När baskoden har implementerats på webbsidan kan du börja köra kommandon med SDK:n. Du behöver inte vänta på den externa filen (`alloy.js`) som ska läsas in från servern innan kommandon körs. Om SDK inte har lästs in helt köas och bearbetas kommandona av SDK så snart som möjligt.

Kommandon körs med följande syntax.

```javascript
alloy("commandName", options);
```

The `commandName` anger för SDK vad som ska göras, medan `options` är de parametrar och data som du vill skicka till ett kommando. Eftersom de tillgängliga alternativen är beroende av kommandot bör du läsa dokumentationen för mer information om varje kommando.

## Ett meddelande om löften

[Löften](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) är grundläggande för hur SDK kommunicerar med koden på din webbsida. Ett löfte är en vanlig programmeringsstruktur som inte är specifik för denna SDK eller ens JavaScript. Ett löfte fungerar som en proxy för ett värde som inte är känt när löftet skapas. När värdet är känt är löftet&quot;löst&quot; med värdet. Hanterarfunktioner kan kopplas till ett löfte, så att du kan meddelas när löftet har lösts eller när ett fel har uppstått under lösningsprocessen. Läs mer om löften [denna självstudiekurs](https://javascript.info/promise-basics) eller någon annan resurs på webben.

## Hantera lyckade eller misslyckade {#handling-success-or-failure}

Varje gång ett kommando körs returneras ett löfte. Löftet representerar det slutliga slutförandet av kommandot. I exemplet nedan kan du använda `then` och `catch` metoder för att avgöra när kommandot lyckades eller misslyckades.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "result" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Om det inte är viktigt för dig att veta när kommandot har utförts kan du ta bort `then` ring.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

På samma sätt kan du ta bort `catch` ring.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Svarsobjekt

Alla löften som returneras från kommandon löses med en `result` -objekt. Resultatobjektet kommer att innehålla data beroende på kommandot och användarens samtycke. Biblioteksinformation skickas till exempel som en egenskap för resultatobjektet i följande kommando.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Godkännande

Om en användare inte har gett sitt samtycke för ett visst ändamål kommer löftet fortfarande att lösas. Svarsobjektet kommer dock endast att innehålla den information som kan ges i det sammanhang som användaren har gett sitt samtycke till.
