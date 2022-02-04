---
title: Hantera flimmer för personaliserade upplevelser med Adobe Experience Platform Web SDK
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att hantera flimmer i användarupplevelser.
keywords: mål;flimmer;prehideStyle;asynkront;asynkront;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
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

Under fördöljningsfasen använder SDK `prehidingStyle` konfigurationsalternativet för att skapa en tagg av HTML-typ och lägga till den i DOM för att säkerställa att stora delar av sidan är dolda. Om du är osäker på vilka delar av sidan som ska personaliseras bör du ange `prehidingStyle` till `body { opacity: 0 !important }`. Detta säkerställer att hela sidan är dold. Detta har dock lett till sämre sidåtergivningsprestanda som rapporterats av verktyg som Lightroom, Web Page Tests osv. För att få bästa sidåtergivningsprestanda bör du ange `prehidingStyle` till en lista med behållarelement som innehåller de delar av sidan som ska personaliseras.

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

## Förbehandling

Förbearbetningsfasen startas när SDK har tagit emot det anpassade innehållet från servern. Under den här fasen är svaret förbearbetat, så att element som måste innehålla personaliserat innehåll döljs. När de här elementen är dolda, är det formatmärkord för HTML som har skapats baserat på `prehidingStyle` konfigurationsalternativet tas bort och HTML-brödtexten eller de dolda behållarelementen visas.

## Återgivning

När allt personaliseringsinnehåll har renderats, eller om fel uppstår, visas alla tidigare dolda element för att säkerställa att det inte finns några dolda element på sidan som doldes av SDK:n.

## Hantera flimmer när SDK läses in asynkront

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
