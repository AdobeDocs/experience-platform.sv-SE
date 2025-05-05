---
title: Åtkomst till svarstoken med Adobe Experience Platform Web SDK
description: Lär dig hur du får åtkomst till svarstoken med Adobe Experience Platform Web SDK.
keywords: personalisering;mål;adobe target;renderDecision;sendEvent;DecisionScopes;result.Decision,response tokens;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Åtkomst till svarstoken

Personalization-innehåll som returneras från Adobe Target innehåller [svarstoken](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=sv-SE), som är information om aktivitet, erbjudande, upplevelse, användarprofil, geoinformation med mera. Dessa uppgifter kan delas med verktyg från tredje part eller användas för felsökning. Svarstoken kan konfigureras i Adobe Target användargränssnitt.

Om du vill få åtkomst till innehåll för personalisering måste du tillhandahålla en callback-funktion när du skickar en händelse. Det här återanropet anropas efter att SDK har fått ett svar från servern. Återanropet kommer att tillhandahållas som ett `result`-objekt, som kan innehålla en `propositions`-egenskap som innehåller returnerat personaliseringsinnehåll. Nedan visas ett exempel på hur du kan tillhandahålla en callback-funktion.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

I det här exemplet är `result.propositions`, om det finns, en matris som innehåller personaliseringsförslag som är relaterade till händelsen. Mer information om innehållet i `result.propositions` finns i [Återge anpassat innehåll](../rendering-personalization-content.md).

Anta att du vill samla in alla aktivitetsnamn från alla utkast som automatiskt renderades av web SDK och överföra dem till en enda array. Du kan sedan skicka den enskilda arrayen till en tredje part. I detta fall:

1. Extrahera utdrag från objektet `result`.
1. Slinga igenom varje förslag.
1. Avgör om SDK återgav förslaget.
1. I så fall gör du en slinga genom varje objekt i förslaget.
1. Hämta aktivitetsnamnet från egenskapen `meta`, som är ett objekt som innehåller svarstoken.
1. Placera aktivitetsnamnet i en array.
1. Skicka aktivitetsnamnen till en tredje part.

Koden ser ut så här:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
