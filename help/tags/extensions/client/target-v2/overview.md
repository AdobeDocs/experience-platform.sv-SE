---
title: Adobe Target v2 Extension - översikt
description: Läs mer om taggtillägget Adobe Target v2 i Adobe Experience Platform.
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 5b88692117c984cd6331e7886d5bf0846309acee
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 3%

---

# Översikt över Adobe Target v2-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Konfigurera Adobe Target v2-tillägget

>[!IMPORTANT]
>
>Adobe Target-tillägget kräver At.js 2.x.

Om Adobe Target-tillägget ännu inte är installerat öppnar du din egenskap, väljer **[!UICONTROL Extensions > Catalog]**, håller pekaren över måltillägget och väljer **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du fliken Tillägg, håller pekaren över tillägget och väljer **[!UICONTROL Configure]**.

![](../../../images/targetv2config.png)

### at.js-inställningar

Alla dina at.js-inställningar, med undantag för Timeout, hämtas automatiskt från din at.js-konfiguration i målgränssnittet. Tillägget hämtar bara inställningar från målgränssnittet när det läggs till första gången, så alla inställningar bör hanteras i användargränssnittet om ytterligare uppdateringar behövs.

Följande konfigurationsalternativ är tillgängliga:

#### Klientkod

Klientkoden är Target-kontots identifierare. Detta bör nästan alltid vara kvar som standardvärde. Den kan ändras med dataelement.

#### Organisations-ID

Detta ID kopplar implementeringen till ditt Adobe Experience Cloud-konto. Detta bör nästan alltid vara kvar som standardvärde. Den kan ändras med dataelement.

#### Serverdomän

Serverdomänen refererar till den domän som Target-begäranden skickas till. Detta bör nästan alltid vara kvar som standardvärde.

#### GDPR-deltagande

När detta är aktiverat tillhandahåller Adobe Target anmälningsfunktioner som kan stödja er strategi för samtyckeshantering. Med avanmälningsfunktionen kan kunderna styra hur och när Target-taggen aktiveras.  Mer information om Adobe-deltagande finns i [Sekretess och allmänna dataskyddsförordningen (GDPR)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

#### Timeout (ms)

Om svaret från Target inte tas emot inom den definierade perioden, går begäran ut och standardinnehållet visas. Ytterligare förfrågningar fortsätter att utföras under besökarens session. Standardvärdet är 3 000 ms, vilket kan vara ett annat värde än den timeout som konfigurerats i målanvändargränssnittet.

Mer information om hur Timeout-inställningen fungerar finns i [Adobe Target-hjälpen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html).

## Åtgärdstyper för måltillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i måltillägget.

Tillägget Mål innehåller följande åtgärder i delen Sedan i en regel:

### Läs in mål

Lägg till den här åtgärden i taggregeln där det är klokt att läsa in Target i sammanhanget för regeln. Detta läser in at.js-biblioteket till sidan. I de flesta implementeringar bör Target läsas in på alla sidor på webbplatsen. Adobe rekommenderar att du bara använder åtgärden Läs in mål om den föregås av ett Target-anrop. Annars kan du råka ut för problem som att Analytics-anropet fördröjs.

Ingen konfiguration behövs.

### Load Target med enhetsspecifik beslutsfattande

Lägg till den här åtgärden i din taggregel där det är rimligt att läsa in Target med [enhetsbeslut](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html) aktiverat i regelsammanhanget. Detta läser in at.js-biblioteket med enhetsbeslut aktiverat på sidan. I de flesta implementeringar bör Target läsas in på alla sidor på webbplatsen. Adobe rekommenderar att du endast använder åtgärden Load Target med enhetsspecifik beslutsåtgärd om den föregås av ett Target-anrop. Annars kan du råka ut för problem som att Analytics-anropet fördröjs.

>[!IMPORTANT]
>
>Använd bara en sidinläsningsbegäran med enhetsbeslut om den redan är konfigurerad. Om du lägger till den här åtgärden i din regel ökar storleken på det slutgiltiga startpaketet eftersom det innehåller beslutsregelmotorn på enheten.

### Lägg till parametrar i alla begäranden

Den här åtgärdstypen tillåter att parametrar läggs till i alla Target-begäranden. Åtgärden Läs in mål måste användas tidigare.

1. Ange namn och värde för de parametrar som du vill lägga till.
1. Välj ikonen Lägg till om du vill lägga till fler parametrar.

### Lägg till parametrar i sidinläsningsbegäran

Den här åtgärdstypen tillåter att parametrar läggs till specifikt i sidans inläsningsbegäranden. Åtgärden Läs in mål måste användas tidigare.

1. Ange namn och värde för de parametrar som du vill lägga till.
1. Välj ikonen Lägg till om du vill lägga till fler parametrar.

### Begäran om inläsning av brandsida

Den här åtgärdstypen gör att Target kan utlösa en begäran när sidan läses in. Åtgärden Läs in mål måste användas tidigare.

Du måste ange om brödtext ska kunna döljas för att undvika flimmer, och vilket format som ska användas när du döljer brödtextelementet. Följande alternativ är tillgängliga:

* **Döljning av brödtext:** Du kan aktivera eller inaktivera den här inställningen. Standardvärdet är Aktiverat, vilket innebär att HTML BODY är dolt.
* **Innehållet i dolt format:** Standardvärdet är body{opacity:0}. Värdet kan ändras till något annat, som body{display:none}.

Mer information finns i [Målets onlinehjälpdokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).

### Utlösarvy

Åtgärden Utlösarvy kan anropas när en ny sida läses in eller när en komponent på en sida återges på nytt. Utlösarvyn ska implementeras för Single Page-program.

1. Ange det vynamn som måste utlösas.
1. Ange om utlösaren för vyn ska tillskrivas ett intryck för rapportering genom att markera kryssrutan Sida. Om vyn är korrelerad till en komponent som återges på nytt och inte ger ett intryck av att rapportera, ska du inte markera kryssrutan Sida.

Mer information om hur du utlöser en vy finns i [`triggerView()` hjälpdokumentationen ](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html).

## Grundläggande Adobe Target-driftsättning

När måltillägget har installerats skapar du minst en regel som ska distribueras korrekt. Du måste först läsa in målbiblioteket (at.js), ange de parametrar som du vill använda med sidinläsningsbegäran och utlösa sidinläsningsbegäran.

En målregel med denna grundläggande implementering ser ut så här:

![](../../../images/targetv2deploy.png)

När du har sparat den här regeln måste du lägga till den i ett bibliotek och skapa/distribuera den så att du kan testa beteendet.

## Adobe Target-tillägg med asynkron distribution

Taggar kan distribueras asynkront. Om du läser in taggbiblioteket asynkront med Target inuti, läses även Target in asynkront. Detta är ett scenario som stöds fullt ut, men det finns ytterligare en fråga som måste hanteras.

I asynkrona distributioner är det möjligt för sidan att slutföra återgivningen av standardinnehållet innan målbiblioteket har lästs in fullständigt och har utfört innehållsbytet. Detta kan leda till det som kallas&quot;flimmer&quot;, där standardinnehållet visas kort innan det ersätts av det anpassade innehåll som anges av Target. Om du vill undvika denna flimmer rekommenderar vi att du använder ett förhandsdolt kodfragment och läser in taggpaketet asynkront för att undvika att innehåll flimrar.

Här är några saker du bör tänka på när du använder det fördolda fragmentet:

* Fragmentet måste läggas till innan taggens huvud-embed-kod läses in.
* Koden kan inte hanteras av taggar, så den måste läggas till direkt på sidan.
* Sidan visas när den tidigaste av följande händelser inträffar:
   * När sidinläsningssvaret har tagits emot
   * När sidans inläsningsbegäran tar slut
   * När själva fragmentet timeout
* Åtgärden &quot;Begäran om inläsning av brandsida&quot; bör användas på alla sidor med det föregående dolda fragmentet för att minimera tiden för det föregående.
* Dölj brödtext måste också vara aktiverat i åtgärden för sidinläsningsbegäran i regeln för sidinläsning som du använder för mål. Annars förblir alla sidinläsningar dolda under tidsgränsen.

Det föregående dolda kodfragmentet är följande och kan minimeras. De konfigurerbara alternativen finns i slutet:

```js
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Som standard döljs hela HTML BODY med fragmentet. I vissa fall kanske du bara vill dölja vissa element i HTML i förväg, inte hela sidan. Du kan uppnå det genom att anpassa style-parametern. Ersätt den med något som bara döljer vissa delar av sidan.

Om du till exempel har två områden som identifieras av ID:n container-1 och container-2 kan formatet ersättas med följande:

```css
#container-1, #container-2 {opacity: 0 !important}
```

I stället för standardvärdet:

```css
body {opacity: 0 !important}
```

Som standard går fragmentet ut 3 000 ms eller 3 sekunder. Det här värdet kan anpassas.
