---
title: Hantera flimmer för personaliserade upplevelser med Adobe Experience Platform Web SDK
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att hantera flimmer i användarupplevelser.
keywords: mål;flimmer;prehideStyle;asynkront;asynkront;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Hantera flimmer

När SDK försöker återge personaliseringsinnehåll måste det se till att det inte blir någon flimmer. Flimmer, som även kallas FOOC (Flash i ursprungligt innehåll), är när ett ursprungligt innehåll visas kort innan alternativet visas under testning/personalisering. SDK försöker tillämpa CSS-format på element på sidan för att säkerställa att dessa element döljs tills personaliseringsinnehållet återges korrekt.

Funktionen flimmerhantering har några faser:

1. Dölj
1. Förbehandling
1. Återgivning

## Dölj

Under fördöljningsfasen använder SDK konfigurationsalternativet `prehidingStyle` för att skapa en HTML-formattagg och lägga till den i DOM för att se till att stora delar av sidan är dolda. Om du är osäker på vilka delar av sidan som ska anpassas bör du ange `prehidingStyle` till `body { opacity: 0 !important }`. På så sätt ser du till att hela sidan är dold. Detta har dock lett till sämre sidåtergivningsprestanda som rapporterats av verktyg som Lightroom, Web Page Tests osv. För att få bästa sidåtergivningsprestanda bör du ställa in `prehidingStyle` på en lista med behållarelement som innehåller de delar av sidan som ska anpassas.

Anta att du har en HTML-sida som den nedan och du vet att endast `bar` och `bazz` behållarelement någonsin kommer att personaliseras:

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

Sedan ska `prehidingStyle` ställas in på något som `#bar, #bazz { opacity: 0 !important }`.

## Förbehandling

Förbearbetningsfasen startas när SDK har tagit emot det anpassade innehållet från servern. Under den här fasen är svaret förbearbetat, så att element som måste innehålla personaliserat innehåll döljs. När dessa element är dolda tas HTML-formattaggen som har skapats baserat på konfigurationsalternativet `prehidingStyle` bort och HTML-innehållet eller de dolda behållarelementen visas.

## Återgivning

När allt personaliseringsinnehåll har renderats, eller om fel uppstår, visas alla tidigare dolda element för att säkerställa att det inte finns några dolda element på sidan som doldes av SDK:n.

## Hantera flimmer när SDK läses in asynkront

Rekommendationen är att alltid läsa in SDK asynkront för att få bästa sidåtergivningsprestanda. Detta har dock vissa konsekvenser för återgivningen av personaliserat innehåll. När SDK läses in asynkront måste du använda det föregående fragmentet. Det föregående fragmentet måste läggas till före SDK på HTML-sidan. Här är ett exempelutdrag som döljer hela brödtexten:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

För att vara säker på att HTML-texten eller behållarelementen inte döljs under en längre tid använder det förhandsdolda fragmentet en timer som som standard tar bort fragmentet efter `3000` millisekunder. `3000` millisekunder är den maximala väntetiden. Om svaret från servern har tagits emot och bearbetats tidigare tas HTML-formattaggen som döljs bort så snart som möjligt.
