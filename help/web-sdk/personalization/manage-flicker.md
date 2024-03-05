---
title: Hantera flimmer för personaliserade upplevelser med Adobe Experience Platform Web SDK
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att hantera flimmer i användarupplevelser.
keywords: mål;flimmer;prehideStyle;asynkront;asynkront;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Hantera flimmer

När SDK försöker återge personaliseringsinnehåll måste det se till att det inte blir någon flimmer. Flimmer, som även kallas FOOC (Flash av ursprungligt innehåll), är när ett ursprungligt innehåll visas kort innan alternativet visas under testning/personalisering. SDK försöker tillämpa CSS-format på element på sidan för att säkerställa att dessa element döljs tills personaliseringsinnehållet återges korrekt.

Hur du hanterar flimmer beror på om du distribuerar Web SDK synkront eller asynkront. Kontrollera `<head>` tagg där du distribuerar `alloy.js` eller tagginläsaren. Förekomsten av `async` i `<script>` -taggen avgör om Web SDK läses in asynkront.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Hantera flimmer för synkrona distributioner

Synkron flimmerhantering är uppdelad i tre faser:

1. Dölj
1. Förbehandling
1. Återgivning

Under **fördöljningsfas** använder SDK [`prehidingStyle`](../commands/configure/prehidingstyle.md) konfigurationsegenskap för att skapa en tagg av typen HTML och lägga till den i DOM för att se till att önskade avsnitt på sidan är dolda. Om du är osäker på vilka delar av sidan som ska personaliseras bör du ange `prehidingStyle` till `body { opacity: 0 !important }`. Detta säkerställer att hela sidan är dold. Detta har dock lett till sämre sidåtergivningsprestanda som rapporterats av verktyg som Lightroom, Web Page Tests osv. För att få bästa sidåtergivningsprestanda bör du ange `prehidingStyle` till en lista med behållarelement som innehåller de delar av sidan som ska personaliseras.

Anta att du har en HTML-sida som den nedan och att bara `bar` och `bazz` behållarelement personaliseras någonsin:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Sedan `prehidingStyle` ska vara inställd på något som `#bar, #bazz { opacity: 0 !important }`.

När SDK har tagit emot anpassat innehåll från servern är **förbearbetningsfas** börjar. Under den här fasen är svaret förbearbetat, så att element som måste innehålla personaliserat innehåll döljs. När de här elementen är dolda, är det formatmärkord för HTML som har skapats baserat på `prehidingStyle` konfigurationsalternativet tas bort och HTML-brödtexten eller de dolda behållarelementen visas.

När allt personaliseringsinnehåll har renderats, eller om något fel uppstod, **återgivningsfas** börjar. Alla tidigare dolda element visas för att säkerställa att det inte finns några dolda element på sidan som doldes av SDK:n.

## Hantera flimmer för asynkrona distributioner

Rekommendationen är att alltid läsa in SDK asynkront för att få bästa sidåtergivningsprestanda. Detta har dock vissa konsekvenser för återgivningen av personaliserat innehåll. När SDK läses in asynkront måste du använda det föregående fragmentet. Det föregående fragmentet måste läggas till före SDK:t på HTML-sidan. Här är ett exempelutdrag som döljer hela brödtexten:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

För att vara säker på att HTML-delen eller behållarelementen inte döljs under en längre tid använder det fördolda fragmentet en timer som som standard tar bort fragmentet efter `3000` millisekunder. The `3000` millisekunder är den maximala väntetiden. Om svaret från servern har tagits emot och bearbetats tidigare tas den tidigare HTML-stiltaggen bort så snart som möjligt.
