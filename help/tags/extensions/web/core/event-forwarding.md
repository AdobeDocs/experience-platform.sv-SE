---
title: Översikt över tillägget för vidarebefordring av kärnhändelser
description: Läs mer om Core-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 0%

---

# Översikt över tillägg för vidarebefordring av viktiga händelser

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Tillägget Core Event-Forwarding innehåller standardhändelser, standardvillkor och datatyper för händelsevidarebefordran i Adobe Experience Platform.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Villkorstyper för kärntillägg

I det här avsnittet beskrivs de villkorstyper som finns i Core-tillägget.  Dessa villkorstyper kan användas med antingen den vanliga typen eller undantagstypen av logik.

### Egen kod

Ange eventuell anpassad kod som måste finnas som villkor för händelsen. Använd den inbyggda kodredigeraren för att ange den anpassade koden. Vidarebefordran av händelser i Adobe Experience Platform har stöd för ES6.

1. Välj **[!UICONTROL Open Editor]**.
1. Skriv den anpassade koden.
1. Välj **[!UICONTROL Save]**.

Använd metoden `getDataElementValue` om du vill komma åt värdet för ett dataelement i anpassad kod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName` skriver du följande: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash-objekt

I din egen kod kan du även använda objektet `ruleStash`.

```javascript
arc.ruleStash: Object<string, *>`
```

```javascript
logger.log(context.arc.ruleStash);
```

`ruleStash` är ett objekt som samlar in alla resultat från åtgärdsmoduler.

Varje tillägg har ett eget namnutrymme. Om tillägget till exempel har namnet `send-beacon`, lagras alla resultat från `send-beacon`-åtgärderna i namnutrymmet `ruleStash['send-beacon']`.

Namnutrymmet är unikt för varje tillägg och har värdet `undefined` i början.

Namnutrymmet åsidosätts med det returnerade resultatet från varje åtgärd. Det händer ingen namnrymdsmagi. Om du till exempel har ett `transform`-tillägg som innehåller två åtgärder: `generate-fullname` och `generate-fulladdress` och lägg sedan till de två åtgärderna i en regel.

Om resultatet av `generate-fullname`-åtgärden är `Firstname Lastname` visas regelstrecket så här när åtgärden har slutförts:

```js
{
  transform: 'Firstname Lastname`
}
```

Om resultatet av `generate-address`-åtgärden är `3900 Adobe Way` visas regelstrecket så här när åtgärden har slutförts:

```js
{
  transform: '3900 Adobe Way`
}
```

Observera att `Firstname Lastname` inte längre finns i regelstrecket. Detta beror på att åtgärden `generate-address` åsidosatte den med adressen.

Om du vill lagra resultaten från båda åtgärderna i namnutrymmet `transform` i `ruleStash` kan du skriva åtgärdsmodulen på samma sätt som i följande exempel:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

Första gången den här åtgärden körs är `ruleStash` `undefined` och den initieras med ett tomt objekt. Nästa gång åtgärden körs returneras `ruleStash` av åtgärden när den anropades tidigare. Om du använder ett objekt som `ruleStash` kan du lägga till nya data utan att data som tidigare angetts av andra åtgärder från tillägget går förlorade.

Du måste vara noga med att alltid returnera det fullständiga tillägget för regelstreck i det här fallet. Om du bara returnerar ett värde (till exempel 5) ser regelstrecket ut så här:

```js
{
  transform: 5
}
```

### Värdejämförelse {#value-comparison}

Jämför två värden för att avgöra om villkoret returnerar true.

Om du har en regel med flera villkor är det möjligt att det här villkoret returnerar true, men regeln utlöses inte eftersom de andra villkoren utvärderas som false eller ett av undantagen utvärderas som sant.

1. Ange ett värde.
1. Markera operatorn. Mer information finns i listan över operatorer för värdejämförelse nedan.
1. Ange ett annat värde för jämförelsen.

Följande värdejämförelseoperatorer är tillgängliga:

**Lika:** Villkoret returnerar true om de två värdena är lika med en icke-strikt jämförelse (i JavaScript returnerar operatorn ==). Värdena kan vara av alla typer. När du skriver ett ord som _true_, _false_, _null_ eller _undefined_ till ett värdefält jämförs ordet som en sträng och konverteras inte till JavaScript-motsvarigheten.

**Är inte lika:** Villkoret returnerar true om de två värdena inte är lika med en icke-strikt jämförelse (i JavaScript returneras != operator). Värdena kan vara av alla typer. När du skriver ett ord som _true_, _false_, _null_ eller _undefined_ till ett värdefält jämförs ordet som en sträng och konverteras inte till JavaScript-motsvarigheten.

**Innehåller:** Villkoret returnerar true om det första värdet innehåller det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Innehåller inte:** Villkoret returnerar true om det första värdet inte innehåller det andra värdet. Tal konverteras till strängar. Alla värden förutom tal och strängar resulterar i att villkoret returnerar true.

**Börjar med:** Villkoret returnerar true om det första värdet börjar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Börjar inte med:** Villkoret returnerar true om det första värdet inte börjar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Slutar med:** Villkoret returnerar true om det första värdet slutar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Slutar inte med:** Villkoret returnerar true om det första värdet inte slutar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Matchar Regex:** Villkoret returnerar true om det första värdet matchar det reguljära uttrycket. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Matchar inte Regex:** Villkoret returnerar true om det första värdet inte matchar det reguljära uttrycket. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Är mindre än:** Villkoret returnerar true om det första värdet är mindre än det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är mindre än eller lika med:** Villkoret returnerar true om det första värdet är mindre än eller lika med det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är större än:** Villkoret returnerar true om det första värdet är större än det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är större än eller lika med:** Villkoret returnerar true om det första värdet är större än eller lika med det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är true:** Villkoret returnerar true om värdet är booleskt med värdet true. Värdet som du anger konverteras inte till ett booleskt värde om det är någon annan typ. Alla värden utom ett booleskt värde med värdet true returnerar villkoret false.

**Är sann:** Villkoret returnerar true om värdet är true efter att ha konverterats till ett booleskt värde. Se [MDN:s sanna dokumentation](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) för exempel på sanna värden.

**Är falskt:** Villkoret returnerar true om värdet är ett booleskt värde med värdet false. Värdet som du anger konverteras inte till ett booleskt värde om det är någon annan typ. Alla värden utom ett booleskt värde med värdet false resulterar i att villkoret returnerar false.

**Är falskt:** Villkoret returnerar true om värdet är false efter att ha konverterats till ett booleskt värde. Se [MDN:s Falsy-dokumentation](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) för exempel på felaktiga värden.



## Åtgärdstyper för kärntillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Core-tillägget.

### Egen kod

Ange koden som körs efter att händelsen har utlösts och villkoren har utvärderats. Vidarebefordran av händelser i Adobe Experience Platform har stöd för ES6.

1. Namnge åtgärdskoden.
1. Välj **[!UICONTROL Open Editor]**.
1. Redigera koden och välj sedan **[!UICONTROL Save]**.

Använd metoden `getDataElementValue` om du vill komma åt värdet för ett dataelement i anpassad kod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName` skriver du följande: 

```javascript
getDataElementValue('productName') 
```

Åtgärder på serversidan för platform launch utförs sekventiellt. Det går också att returnera ett värde som kan användas i en efterföljande åtgärd för anpassad kod i en åtgärd. Det returnerade värdet kan komma från kod i den åtgärden eller från svarstexten för ett anrop till en extern källa. Om du vill referera till data från en tidigare utförd åtgärd i en enskild regel där Core-tillägget används, skapar du ett dataelement av typen `Path` och använder följande sökväg för att referera till värdet för variabeln `productCategory` som definierats i anpassad kod i Core-tillägget:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Dataelementtyper för kärntillägg

Dataelementtyperna bestäms av tillägget. Det finns ingen begränsning för de typer som kan skapas.

I följande avsnitt beskrivs de typer av dataelement som finns i Core-tillägget. Andra tillägg använder andra typer av dataelement.

### Egen kod

Du kan ange egen JavaScript i användargränssnittet genom att markera **[!UICONTROL Open Editor]** och infoga kod i redigeringsfönstret.

En return-programsats krävs i redigeringsfönstret för att ange vilket värde som ska användas som dataelementvärde. Om en return-programsats inte ingår eller om värdet `null` eller `undefined` returneras, återspeglas dataelementets standardvärde `null` eller `undefined`.

Använd metoden `getDataElementValue` om du vill komma åt värdet för ett dataelement i anpassad kod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName` skriver du följande: 

```javascript
getDataElementValue('productName') 
```

**Exempel:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Bana

En sökväg till ett nyckelvärdepar för en händelse som skickas till Adobe Experience Platform Edge Network kan refereras med hjälp av datatypen Path.

Om du vill referera till hela objektet för en händelse anger du `arc` som sökväg. Akronymen `arc` står för Adobe Resource Context och är den översta sökvägen för en händelse som skickas till Adobe Experience Platform Edge Network.

Med tanke på `interact`-anropet från klienten till Edge Network har till exempel följande begäran från webbläsarkonsolen:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Om du vill ange en sökväg som refererar till `pageName` anger du följande i sökvägsfältet:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>`interact`-anropet från klienten har `events`, men för händelsevidarebefordran behöver du `event`. Detta beror på att vidarebefordran av händelser undersöker varje händelse individuellt och inte som en grupp med flera händelser som visas på klienten.
