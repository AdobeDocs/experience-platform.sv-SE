---
title: Core Library Modules for Web Extensions
description: Lär dig mer om kärnbiblioteksmodulerna som du kan använda i dina webbtillägg.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Huvudbiblioteksmoduler för webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Det här dokumentet innehåller en lista med de moduler i huvudbiblioteket som du kan använda i dina webbtillägg. Du kan komma åt dessa moduler med `require('@adobe/{MODULE}')`, där `{MODULE}` är namnet på kärnmodulen som du vill använda.

## [!DNL reactor-object-assign]

`reactor-object-assign` härmar den inbyggda [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)-metoden genom att kopiera egenskaper från källobjekt till ett målobjekt.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

Objektet `reactor-cookie` är ett verktyg för att läsa och skriva cookies. Mer information finns i [js-cookie npm-paketet](https://www.npmjs.com/package/js-cookie).

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` representerar [`Document`](https://developer.mozilla.org/en-US/docs/Web/API/Document)-objektet. Detta kan vara bra när du testar modulen genom att tillåta att testerna injicerar ett `document`-modellobjekt med verktyg som [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` är ett verktyg för att analysera och serialisera [frågesträngar](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

Verktyget har följande metoder:

* `queryString.parse({STRING})`: Tolkar en frågesträng till ett objekt. Inledande `?`-, `#`- och `&`-tecken i frågesträngen ignoreras.
* `queryString.stringify({OBJECT})`: Strängar ett objekt i en frågesträng.

### [!DNL reactor-load-script]

`reactor-load-script` är en funktion som läser in ett skript när en URL anges. En skripttagg skapas och placeras i noden `head` i dokumentet. Ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) returneras, som du kan använda för att avgöra när skriptet har lästs in eller misslyckats.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` är en konstruktor som härmar det [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som är inbyggt i ECMAScript 6. Om det inbyggda Promise-API:t är tillgängligt returneras det i stället.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` representerar [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window)-objektet. Detta kan vara bra när du testar modulen genom att tillåta att testerna injicerar ett `Window`-modellobjekt med verktyg som [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
