---
title: Hantera flimmer för personaliserade upplevelser med Adobe Experience Platform Web SDK
description: Läs om hur du använder Adobe Experience Platform Web SDK för att hantera flimmer i användarupplevelser.
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Hantera flimmer

När man försöker återge personaliserat innehåll måste SDK se till att det inte blir någon flimmer. Flimmer, som även kallas FOOC (Flash av ursprungligt innehåll), är när ett ursprungligt innehåll visas kort innan alternativet visas under testning/personalisering. SDK försöker tillämpa CSS-format på element på sidan för att säkerställa att dessa element döljs tills personaliseringsinnehållet återges korrekt.

Hur du hanterar flimmer beror på om du distribuerar Web SDK synkront eller asynkront. Kontrollera taggen `<head>` där du distribuerar `alloy.js` eller tagginläsaren. Förekomsten av attributet `async` i taggen `<script>` avgör om Web SDK läses in asynkront.

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

Under **fördöljningsfasen** använder SDK konfigurationsegenskapen [`prehidingStyle`](../../js/commands/configure/prehidingstyle.md) för att skapa en HTML-formattagg och lägga till den i DOM för att se till att önskade avsnitt på sidan är dolda. Om du är osäker på vilka delar av sidan som ska anpassas, bör du ange `prehidingStyle` till `body { opacity: 0 !important }`. Detta säkerställer att hela sidan är dold. Detta har dock lett till sämre sidåtergivningsprestanda som rapporterats av verktyg som Lightroom, Web Page Tests osv. För att få bästa sidåtergivningsprestanda bör du ställa in `prehidingStyle` på en lista med behållarelement som innehåller de delar av sidan som ska anpassas.

Anta att du har en HTML-sida som den nedan och du vet att bara `bar` och `bazz` behållarelement någonsin kommer att personaliseras:

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

Därefter ska `prehidingStyle` anges till något som `#bar, #bazz { opacity: 0 !important }`.

När SDK har tagit emot anpassat innehåll från servern startar **förbearbetningsfasen**. Under den här fasen är svaret förbearbetat, så att element som måste innehålla personaliserat innehåll döljs. När de här elementen är dolda tas den HTML-formattagg som har skapats baserat på konfigurationsalternativet `prehidingStyle` bort och HTML body- eller dolda behållarelement visas.

När allt anpassningsinnehåll har renderats, eller om något fel uppstod, startar **återgivningsfasen**. Alla tidigare dolda element visas för att säkerställa att det inte finns några dolda element på sidan som är dolda av SDK.

## Hantera flimmer för asynkrona distributioner

Rekommendationen är att alltid läsa in SDK asynkront för att få bästa sidåtergivningsprestanda. Detta har dock vissa konsekvenser för återgivningen av personaliserat innehåll. När SDK läses in asynkront måste det fördolda fragmentet användas. Det föregående fragmentet måste läggas till före SDK på HTML-sidan. Här är ett exempelutdrag som döljer hela brödtexten:

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

För att vara säker på att HTML-texten eller behållarelementen inte är dolda under en längre tidsperiod använder det föregående dolda fragmentet en timer som som standard tar bort fragmentet efter `3000` millisekunder. `3000` millisekunder är den maximala väntetiden. Om svaret från servern har tagits emot och bearbetats tidigare tas den tidigare HTML-stiltaggen bort så snart som möjligt.
