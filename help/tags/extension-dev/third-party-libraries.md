---
title: Implementera tredjepartsbibliotek
description: Lär dig mer om de olika metoderna för att lagra bibliotek från tredje part i dina Adobe Experience Platform-taggtillägg.
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# Implementera bibliotek från tredje part

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Ett av de främsta syftena med taggtillägg i Adobe Experience Platform är att göra det möjligt att enkelt implementera befintlig marknadsföringsteknologi (bibliotek) på er webbplats. Genom att använda tillägg kan du implementera bibliotek från tredjepartsnätverk för innehållsleverans (CDN) utan att behöva redigera HTML för webbplatsen manuellt.

Det finns flera metoder för att hantera tredjepartsbibliotek (leverantörsbibliotek) inom tilläggen. I det här dokumentet finns en översikt över de olika implementeringsmetoderna, inklusive för- och nackdelarna med dem.

## Förutsättningar

Det här dokumentet kräver en fungerande förståelse för tillägg i taggar, inklusive vad de kan göra och hur de är sammansatta. Se [översikt över tilläggsutveckling](./overview.md) för mer information.

## Inläsningsprocess för baskod

Förutom taggarna är det viktigt att förstå hur marknadsföringsteknologier normalt läses in på en webbplats. Tredjepartsbiblioteksleverantörer tillhandahåller ett kodfragment (som kallas baskod) som måste bäddas in i HTML på webbplatsen för att bibliotekets funktioner ska kunna läsas in.

I allmänhet utförs en del av följande process av baskoder för marknadsföringsteknologier när de läses in på din webbplats:

1. Konfigurera en global funktion som kan användas för att interagera med leverantörsbiblioteket.
1. Läs in leverantörsbiblioteket.
1. Gör en serie inledande anrop i kö till den globala funktionen för konfigurations- och spårningsändamål.

När den globala funktionen är inställd kan du fortfarande anropa funktionen innan biblioteket har lästs in. Alla anrop du gör läggs till i baskodens kömekanism och körs sedan i sekventiell ordning när biblioteket har lästs in.

När inläsningen av biblioteket är klar ersätts den globala funktionen med en ny funktion som åsidosätter kön och i stället omedelbart bearbetar eventuella framtida anrop till funktionen.

### Exempel på baskod

Följande JavaScript är ett exempel på en ominifierad baskod för [Pinterest-konverteringstagg](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), som senare kommer att användas som referens i det här dokumentet för att visa hur baskoden kan anpassas för olika implementeringsstrategier med taggar:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

Sammanfattningsvis ger baskoden ovan en [direkt anropat funktionsuttryck (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) som skapar en global funktion som kan interagera med biblioteket (`window.pintrk`). Dessutom tilldelas en `scriptURL` varierar värdet för `https://s.pinimg.com/ct/core.js`, som är den plats där biblioteket finns. Så som förklarats ovan kommer alla funktioner som anropas innan biblioteket har lästs in att placeras i en kö (`window.pintrk.queue`) som ska köras i följd när biblioteket är tillgängligt.

Följande del av baskoden är mest relevant när det gäller att förstå hur biblioteket läses in på din plats:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

Baskoden skapar ett skriptelement, ställer in det att läsas in asynkront och ställer in `src` URL till `https://s.pinimg.com/ct/core.js`. Sedan läggs skriptelementet till i dokumentet genom att det infogas före det första skriptelementet som redan finns i dokumentet.

## Alternativ för taggimplementering

I avsnitten nedan visas olika sätt att läsa in leverantörsbibliotek i dina tillägg med hjälp av Pinterest baskod som visades tidigare som exempel. I vart och ett av dessa exempel ingår att skapa en [åtgärdstyp för ett webbtillägg](./web/action-types.md) som läser in biblioteket på din webbplats.

>[!NOTE]
>
>I exemplen nedan används åtgärdstyper för demonstrationssyften, men du kan tillämpa samma principer på alla funktioner som läser in taggbiblioteket på din webbplats.


Följande metoder ingår:

- [Implementera bibliotek från tredje part](#implementing-third-party-libraries)
   - [Förutsättningar](#prerequisites)
   - [Inläsningsprocess för baskod](#base-code-loading-process)
      - [Exempel på baskod](#base-code-example)
   - [Alternativ för taggimplementering](#tags-implementation-options)
      - [Läs in vid körning från leverantörsvärden {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Läs in vid körning från taggbiblioteksvärden](#load-at-runtime-from-the-tag-library-host)
      - [Bädda in biblioteket direkt](#embed-the-library-directly)
   - [Nästa steg](#next-steps)

### Läs in vid körning från leverantörsvärden {#vendor-host}

Den vanligaste metoden för leverantörsbibliotek är att använda leverantörens CDN.  Eftersom baskoden för de flesta leverantörsbibliotek redan har konfigurerats för att läsa in biblioteket från leverantörens CDN, kan du konfigurera tillägget så att biblioteket läses in från samma plats.

Det är oftast enklast att underhålla eftersom uppdateringar som görs i filen på CDN automatiskt läses in av tillägget.

När du använder den här metoden kan du helt enkelt klistra in hela baskoden direkt i en åtgärdstyp som så:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Om du vill kan du vidta ytterligare åtgärder för att omfaktorisera implementeringen. Sedan variablerna `scriptElement` och `firstScriptElement` är nu omfång för den exporterade funktionen, du kan ta bort ICFE eftersom dessa variabler inte riskerar att bli globala.

Dessutom innehåller taggar flera [kärnmoduler](./web/core.md) som alla tillägg kan använda. I synnerhet `@adobe/reactor-load-script` Modulen läser in ett skript från en fjärrplats genom att skapa ett skriptelement och lägga till det i dokumentet. Genom att använda den här modulen för skriptinläsningsprocessen kan du omfaktorisera åtgärdskoden ytterligare:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Läs in vid körning från taggbiblioteksvärden

Användningen av en leverantör-CDN för värdtjänster för bibliotek innebär flera risker: CDN kan misslyckas, filen kan uppdateras med ett kritiskt fel när som helst, eller filen kan komprometteras i ofarliga syften.

För att åtgärda detta kan du välja att inkludera leverantörsbiblioteket som en separat fil i tillägget. Tillägget kan sedan konfigureras så att filen ligger bredvid huvudtaggbiblioteket. Vid körning läser tillägget in leverantörsbiblioteket från samma server som levererade huvudbiblioteket till webbplatsen.

>[!IMPORTANT]
>
>I vissa fall kan leverantörsbiblioteket läsa in ytterligare kod från tredjepartsservrar, vilket är fallet med Pinterest leverantörsbibliotek. I dessa fall kanske inte alla riskrelaterade problem kan lösas helt genom att du paketerar leverantörsbiblioteket med ditt tillägg.

För att implementera detta måste du först hämta leverantörsbiblioteket till din dator. I Pinterest finns leverantörsbiblioteket på [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). När du har hämtat filen måste du placera den i tilläggsprojektet. I exemplet nedan namnges filen `pinterest.js` och finns i `vendor` i projektkatalogen.

När biblioteksfilen finns i projektet måste du uppdatera [tilläggsmanifest](./manifest.md) (`extension.json`) för att ange att leverantörsbiblioteket ska levereras tillsammans med huvudtaggbiblioteket. Det gör du genom att lägga till sökvägen till biblioteksfilen i en `hostedLibFiles` array:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Slutligen måste du konfigurera åtgärdskoden så att leverantörsbiblioteket läses in från samma server som är värd för huvudbiblioteket. I exemplet nedan används den åtgärdskod som är inbyggd i [föregående avsnitt](#vendor-host) som startpunkt. Använda [turbinobjekt](./turbine.md)måste du skicka leverantörsfilens filnamn (utan sökväg) på följande sätt:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Observera att när du använder den här metoden måste du uppdatera din hämtade leverantörsfil manuellt när biblioteket uppdateras i sitt CDN och sedan släppa ändringarna i en ny version av tillägget.

### Bädda in biblioteket direkt

Du kan kringgå behovet av att läsa in leverantörsbiblioteket helt genom att bädda in bibliotekskoden direkt i själva åtgärdskoden, vilket gör den till en del av huvudtaggbiblioteket. Om du använder den här metoden ökar huvudbibliotekets storlek, men du behöver inte göra ytterligare en HTTP-begäran för att hämta en separat fil.

Använda den inbyggda åtgärdskoden i [föregående avsnitt](#vendor-host) Som utgångspunkt kan du ersätta raden där skriptet läses in med innehållet i själva skriptet:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Nästa steg

Det här dokumentet innehåller en översikt över olika metoder för att lagra tredjepartsbibliotek i taggtilläggen. De här exemplen fokuserades på bibliotek, men de här teknikerna gäller för alla kodavsnitt som kan användas i tillägget.

Läs dokumentationen som är länkad till i den här handboken om du vill veta mer om verktygen för att konfigurera tillägg, inklusive åtgärdstyper, tilläggsmanifestet, kärnmoduler och turbinobjektet.
