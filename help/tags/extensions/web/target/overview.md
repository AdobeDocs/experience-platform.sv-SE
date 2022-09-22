---
title: Adobe Target Extension - översikt
description: Läs om taggtillägget för Adobe Target i Adobe Experience Platform.
exl-id: b1c5e25b-42ea-4835-b2d4-913fa2536e77
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---

# Översikt över Adobe Target-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Konfigurera Adobe Target-tillägget

>[!IMPORTANT]
>
> Adobe Target-tillägget kräver at.js. Det stöder inte mbox.js.

Om Adobe Target-tillägget inte är installerat ännu öppnar du din egenskap och väljer **[!UICONTROL Extensions > Catalog]**, hovra över måltillägget och välj **[!UICONTROL Install]**.

Om du vill konfigurera tillägget öppnar du [!UICONTROL Extensions] hovra över tillägget och välj **[!UICONTROL Configure]**.

![](../../../images/ext-target-config.png)

### at.js-inställningar

Alla dina at.js-inställningar, med undantag för Timeout, hämtas automatiskt från din at.js-konfiguration i målanvändargränssnittet. Tillägget hämtar bara inställningar från målanvändargränssnittet när det läggs till första gången, så alla inställningar bör hanteras i användargränssnittet för datainsamling om ytterligare uppdateringar behövs.

Följande konfigurationsalternativ är tillgängliga:

#### Klientkod

Klientkoden är Target-kontots identifierare. Detta bör nästan alltid vara kvar som standardvärde.

Kan ändras med dataelement.

#### Organisations-ID

Detta ID kopplar implementeringen till ditt Adobe Experience Cloud-konto. Detta bör nästan alltid vara kvar som standardvärde.

Kan ändras med dataelement.

#### Namn på global mbox

Visar namnet på din globala Target-begäran. Som standard är det här namnet target-global-mbox, såvida du inte har ändrat namnet i målanvändargränssnittet innan du lägger till tillägget.

Kan ändras med dataelement.

#### Serverdomän

Domänen dit Target-begäranden skickas. Detta bör nästan alltid vara kvar som standardvärde.

#### Cross Domain

Avgör var Target anger cookies i webbläsarna.

* **Inaktiverad:** Anger endast cookies på förstahandsdomänen. Det här är den typiska inställningen.
* **Aktiverad:** Anger cookies på både den första domänen och måldomänen för tredje part (&quot;serverdomänen&quot;).

#### Timeout (ms)

Om svaret från Target inte tas emot inom den definierade perioden, går begäran ut och standardinnehållet visas. Ytterligare förfrågningar fortsätter att utföras under besökarens session. Standardvärdet är 3 000 ms, vilket kan vara ett annat värde än den timeout som konfigurerats i målanvändargränssnittet.

Mer information om hur inställningen Timeout fungerar finns i [Hjälp om Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html).

#### Andra at.js-inställningar som är tillgängliga i målanvändargränssnittet

Flera inställningar som är tillgängliga på [!UICONTROL Edit at.js settings] sidan i målgränssnittet är inte en del av måltillägget. Här är förslag på tillfälliga lösningar:

* Skapa global mbox automatiskt Den här inställningen ersätts av den globala mbox-åtgärden för Fire i tillägget Target.
* Bibliotekshuvud Den här inställningen ingår inte i måltillägget. Placera kod som ska läsas in före at.js i en Core Extension>Custom Code-åtgärd innan du använder åtgärden Load Target.
* Library Footer Den här inställningen ingår inte i måltillägget. Placera kod som ska läsas in efter at.js i en Core Extension>Custom Code-åtgärd efter att åtgärden Load Target har använts.

## Åtgärdstyper för måltillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i måltillägget.

Tillägget Mål innehåller följande åtgärder i delen Sedan i en regel:

### Läs in mål

Lägg till den här åtgärden i taggregeln där det är klokt att läsa in Target i sammanhanget för regeln. Detta läser in at.js-biblioteket till sidan. I de flesta implementeringar bör Target läsas in på alla sidor på webbplatsen.

Ingen konfiguration behövs.

### Lägg till mbox-parametrar

Lägg till parametrar i alla mbox-begäranden. Åtgärden Läs in mål måste användas tidigare.

1. Ange namn och värde för de parametrar som du vill lägga till.
1. Välj **plus (+)** om du vill lägga till fler parametrar.

### Lägg till globala mbox-parametrar

Lägg bara till parametrar i dina globala mbox-begäranden. Åtgärden Läs in mål måste användas tidigare.

1. Ange namn och värde för de parametrar som du vill lägga till.
1. Välj **plus (+)** om du vill lägga till fler parametrar.

### Fire Global Mbox

Starta den globala mbox på sidan. Åtgärden Läs in mål måste användas tidigare.

Ange om du vill aktivera dold brödtext för att förhindra flimmer och vilket format som ska användas när du döljer body-elementet.

Följande alternativ är tillgängliga:

* **Döljande av brödtext:** Du kan aktivera eller inaktivera den här inställningen. Standardvärdet är Aktiverat, vilket innebär att HTML BODY är dolt.
* **Dolt format för brödtext:** Standardvärdet är `body{opacity:0}`. Det här värdet kan ändras till något annat, som `body{display:none}`.

Mer information finns i [Ange onlinehjälpdokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).

## Grundläggande Adobe Target-driftsättning

När måltillägget har installerats måste du skapa minst en regel för att kunna distribuera det korrekt. Du måste först läsa in målbiblioteket (at.js), ange de parametrar som du vill använda med den globala mbox och sedan utlösa den globala mbox.

En målregel med denna grundläggande implementering ser ut så här:

![](../../../images/basic_target_implementation.png)

När du har sparat den här regeln måste du lägga till den i ett bibliotek och skapa/distribuera den så att du kan testa beteendet.

## Adobe Target-tillägg med asynkron distribution

Taggar kan distribueras asynkront. Om du läser in taggbiblioteket asynkront med Target inuti, läses även Target in asynkront. Detta är ett scenario som stöds fullt ut, men det finns ytterligare en fråga som måste hanteras.

I asynkrona distributioner kan sidan slutföra återgivningen av standardinnehållet innan målbiblioteket har lästs in fullständigt och har utfört innehållsbytet. Detta kan leda till det som kallas&quot;flimmer&quot;, där standardinnehållet visas kort innan det ersätts av det anpassade innehåll som anges av Target. Om du vill undvika denna flimmer rekommenderar vi att du använder ett förhandsdolt kodfragment och läser in taggpaketet asynkront för att undvika att innehåll flimrar.

Här är några saker du bör tänka på när du använder det fördolda fragmentet:

* Fragmentet måste läggas till innan taggens huvud-embed-kod läses in.
* Koden kan inte hanteras av taggar, så den måste läggas till direkt på sidan.
* Sidan visas när den tidigaste av följande händelser inträffar:
   * När det globala mbox-svaret har tagits emot
   * När den globala mbox-begäran gör timeout
   * När själva fragmentet timeout
* Åtgärden &quot;Fire Global Mbox&quot; ska användas på alla sidor med det föregående dolda fragmentet för att minimera tiden för det föregående dolda fragmentet.

Det föregående dolda kodfragmentet är följande och kan minimeras. De konfigurerbara alternativen finns i slutet:

```javascript
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
