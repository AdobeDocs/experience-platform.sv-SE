---
title: Satellitobjektreferens
description: Lär dig mer om objektet _satellit på klientsidan och de olika funktioner du kan utföra med det i taggar.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 309f3cce82c5d6c7f10c08b05da6d9c6c44631b6
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Satellitobjektreferens

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Det här dokumentet fungerar som referens för klientsidesobjektet `_satellite` och de olika funktioner du kan utföra med det.

## `track`

**Kod**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Exempel**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` utlöser alla regler med händelsetypen för direktanrop som har konfigurerats med den angivna identifieraren från Core-taggtillägget. Exemplet ovan utlöser alla regler med en Direct Call-händelsetyp där den konfigurerade identifieraren är `contact_submit`. Ett valfritt objekt som innehåller relaterad information skickas också. Du kommer åt detaljobjektet genom att ange `%event.detail%` i ett textfält i ett villkor eller en åtgärd eller `event.detail` i kodredigeraren i ett villkor eller en åtgärd för anpassad kod.

## `getVar`

**Kod**

```javascript
_satellite.getVar(name: string) => *
```

**Exempel**

```javascript
var product = _satellite.getVar('product');
```

I det angivna exemplet returneras dataelementets värde om det finns ett dataelement med ett matchande namn. Om det inte finns något matchande dataelement kommer det att kontrollera om en anpassad variabel med ett matchande namn tidigare har angetts med `_satellite.setVar()`. Om en matchande anpassad variabel hittas returneras dess värde.

>[!NOTE]
>
>Du kan använda syntax i procent (`%`) för att referera till variabler för många formulärfält i taggimplementeringen, vilket minskar behovet av att anropa `_satellite.getVar()`. Om du till exempel använder `%product%` kommer du åt värdet för produktdataelementet eller den anpassade variabeln.

När en händelse utlöser en regel kan du skicka regelns motsvarande `event`-objekt till `_satellite.getVar()` på följande sätt:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

>[!NOTE]
>
>Koden `setVar` är helt separat från ett dataelement som anges i Taggar.

**Kod**

```javascript
_satellite.setVar(name: string, value: *)
```

**Exempel**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` anger en anpassad variabel med ett angivet namn och värde. Värdet för variabeln kan sedan nås med `_satellite.getVar()`.

Du kan också ange flera variabler samtidigt genom att skicka ett objekt där nycklarna är variabelnamn och värdena är respektive variabelvärde.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Kod**

```javascript
_satellite.getVisitorId() => Object
```

**Exempel**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Om tillägget [!DNL Adobe Experience Cloud ID] är installerat på egenskapen returnerar den här metoden instansen av Visitor-ID. Mer information finns i [Experience Cloud ID-tjänstdokumentationen](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=sv-SE).

## `logger`

**Kod**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Exempel**

```javascript
_satellite.logger.error('No product ID found.');
```

Objektet `logger` tillåter att ett meddelande loggas till webbläsarkonsolen. Meddelandet visas bara om taggfelsfunktionen är aktiverad av användaren (genom att anropa `_satellite.setDebug(true)` eller använda ett lämpligt webbläsartillägg).

### Varningar om borttagning av loggning

```javascript
_satellite.logger.deprecation(message: string)
```

**Exempel**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Detta loggar en varning till webbläsarkonsolen. Meddelandet visas oavsett om taggfelsfunktionen är aktiverad av användaren eller inte.

## `cookie` {#cookie}

`_satellite.cookie` innehåller funktioner för att läsa och skriva cookies. Det är en exponerad kopia av tredjepartsbiblioteket js-cookie. Mer information om mer avancerad användning av det här biblioteket finns i [js-cookie-dokumentationen](https://www.npmjs.com/package/js-cookie#basic-usage).

### Ange en cookie {#cookie-set}

Använd `_satellite.cookie.set()` om du vill ange en cookie.

**Kod**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>I den gamla [`setCookie`](#setCookie)-metoden för att ange cookies var det tredje (valfria) argumentet för det här funktionsanropet ett heltal som indikerade cookie-objektets förfallotid i dagar. I den här nya metoden accepteras ett &quot;attributes&quot;-objekt som ett tredje argument. Om du vill ange en förfallotid för en cookie med den nya metoden måste du ange en `expires`-egenskap i attributobjektet och ange det till önskat värde. Detta visas i exemplet nedan.

**Exempel**

Följande funktionsanrop skriver en cookie som upphör att gälla om en vecka.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Hämta en cookie {#cookie-get}

Använd `_satellite.cookie.get()` om du vill hämta en cookie.

**Kod**

```javascript
_satellite.cookie.get(name: string) => string
```

**Exempel**

Följande funktionsanrop läser en tidigare angiven cookie.

```javascript
var product = _satellite.cookie.get('product');
```

### Ta bort en cookie {#cookie-remove}

Använd `_satellite.cookie.remove()` om du vill ta bort en cookie.

**Kod**

```javascript
_satellite.cookie.remove(name: string)
```

**Exempel**

Följande funktionsanrop tar bort en tidigare angiven cookie.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Kod**

```javascript
_satellite.buildInfo
```

Det här objektet innehåller information om bygget av det aktuella biblioteket för tagg-körning. Objektet innehåller följande egenskaper:

### `turbineVersion`

Detta innehåller den [turbinversion](https://www.npmjs.com/package/@adobe/reactor-turbine) som används i det aktuella biblioteket.

### `turbineBuildDate`

ISO 8601-datumet när versionen av [turbin](https://www.npmjs.com/package/@adobe/reactor-turbine) som används i behållaren skapades.

### `buildDate`

ISO 8601-datumet när det aktuella biblioteket skapades.

I det här exemplet visas objektvärdena:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Det här objektet innehåller information om den miljö som det aktuella taggredigeringsbiblioteket är distribuerat till.

**Kod**

```javascript
_satellite.environment
```

Objektet innehåller följande egenskaper:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för miljön. |
| `stage` | Den miljö som det här biblioteket skapades för. Möjliga värden är `development`, `staging` och `production`. |

## `notify`

>[!NOTE]
>
>Den här metoden har tagits bort. Använd `_satellite.logger.log()` i stället.

**Kod**

```javascript
_satellite.notify(message: string[, level: number])
```

**Exempel**

```javascript
_satellite.notify('Hello world!');
```

`notify` loggar ett meddelande till webbläsarkonsolen. Meddelandet visas bara om taggfelsfunktionen är aktiverad av användaren (genom att anropa `_satellite.setDebug(true)` eller använda ett lämpligt webbläsartillägg).

Du kan skicka en loggningsnivå som kan påverka formatering och filtrering av meddelandet som loggas. Följande nivåer stöds:

3 - Informationsmeddelanden.

4 - Varningsmeddelanden.

5 - Felmeddelanden.

Om du inte anger någon loggningsnivå eller skickar något annat nivåvärde loggas meddelandet som ett vanligt meddelande.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Den här metoden har tagits bort. Använd [`_satellite.cookie.set()`](#cookie-set) i stället.

**Kod**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Exempel**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Detta ställer in en cookie i användarens webbläsare. Cookien kvarstår i det angivna antalet dagar.

## `readCookie`

>[!IMPORTANT]
>
>Den här metoden har tagits bort. Använd [`_satellite.cookie.get()`](#cookie-get) i stället.

**Kod**

```javascript
_satellite.readCookie(name: string) => string
```

**Exempel**

```javascript
var product = _satellite.readCookie('product');
```

Detta läser en cookie från användarens webbläsare.

## `removeCookie`

>[!NOTE]
>
>Den här metoden har tagits bort. Använd [`_satellite.cookie.remove()`](#cookie-remove) i stället.

**Kod**

```javascript
_satellite.removeCookie(name: string)
```

**Exempel**

```javascript
_satellite.removeCookie('product');
```

Detta tar bort en cookie från användarens webbläsare.

## Felsökningsfunktioner

Följande funktioner ska inte kommas åt från produktionskoden. De är endast avsedda för felsökning och kommer att ändras med tiden efter behov.

### `container`

**Kod**

```javascript
_satellite._container
```

**Exempel**

>[!IMPORTANT]
>
>Den här funktionen ska inte nås från produktionskoden. Den är endast avsedd för felsökning och kommer att ändras med tiden efter behov.

### `monitor`

**Kod**

```javascript
_satellite._monitors
```

**Exempel**

>[!IMPORTANT]
>
>Den här funktionen ska inte nås från produktionskoden. Den är endast avsedd för felsökning och kommer att ändras med tiden efter behov.

**Exempel**

Lägg till ett kodfragment på HTML på din webbsida som kör ett taggbibliotek. Normalt infogas koden i elementet `<head>` före elementet `<script>` som läser in taggbiblioteket. På så sätt kan övervakaren fånga upp de tidigaste systemhändelserna som inträffar i taggbiblioteket. Exempel:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

I det första skriptelementet skapas det ursprungliga `_satellite`-objektet och en array på `_satellite._monitors` initieras eftersom taggbiblioteket inte har lästs in ännu. Skriptet lägger sedan till ett övervakarobjekt i den arrayen. Övervakningsobjektet kan ange följande metoder som senare anropas av taggbiblioteket:

### `ruleTriggered`

Den här funktionen anropas efter att en händelse utlöser en regel, men innan regelns villkor och åtgärder har bearbetats. Händelseobjektet som skickades till `ruleTriggered` innehåller information om regeln som utlöstes.

### `ruleCompleted`

Den här funktionen anropas efter att en regel har bearbetats fullständigt. Händelsen har med andra ord inträffat, alla villkor har skickats och alla åtgärder har utförts. Händelseobjektet som skickades till `ruleCompleted` innehåller information om regeln som slutfördes.

### `ruleConditionFailed`

Den här funktionen anropas efter att en regel har utlösts och ett av dess villkor har misslyckats. Händelseobjektet som skickades till `ruleConditionFailed` innehåller information om regeln som utlöstes och villkoret som misslyckades.

Om `ruleTriggered` anropas kommer antingen `ruleCompleted` eller `ruleConditionFailed` att anropas kort därefter.

>[!NOTE]
>
>En bildskärm behöver inte ange alla tre metoderna (`ruleTriggered`, `ruleCompleted` och `ruleConditionFailed`). Taggar i Adobe Experience Platform fungerar med de metoder som stöds av bildskärmen.

### Testa monitorn

I exemplet ovan anges alla tre metoderna i monitorn. När de anropas loggar övervakaren ut relevant information. Om du vill testa detta ställer du in två regler i taggbiblioteket:

1. En regel som har en klickningshändelse och ett webbläsarvillkor som bara godkänns om webbläsaren är [!DNL Chrome].
1. En regel som har en klickningshändelse och ett webbläsarvillkor som bara godkänns om webbläsaren är [!DNL Firefox].

Om du öppnar sidan i [!DNL Chrome], öppnar webbläsarkonsolen och väljer sidan visas följande i konsolen:

![](../../images/debug.png)

Ytterligare kopplingar eller ytterligare information kan läggas till i dessa hanterare efter behov.
