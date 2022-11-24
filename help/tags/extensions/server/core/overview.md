---
title: Översikt över tillägget för vidarebefordring av kärnhändelser
description: Läs mer om Core-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# Översikt över tillägg för vidarebefordring av viktiga händelser

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Tillägget Core Event-Forwarding innehåller standardhändelser, standardvillkor och datatyper för händelsevidarebefordran i Adobe Experience Platform.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Villkorstyper för kärntillägg

I det här avsnittet beskrivs de villkorstyper som finns i Core-tillägget.  Dessa villkorstyper kan användas med antingen den vanliga typen eller undantagstypen av logik.

### Egen kod

Ange eventuell anpassad kod som måste finnas som villkor för händelsen. Använd den inbyggda kodredigeraren för att ange den anpassade koden. Vidarebefordran av händelser i Adobe Experience Platform har stöd för ES6.

1. Välj **[!UICONTROL Open Editor]**.
1. Skriv den anpassade koden.
1. Välj **[!UICONTROL Save]**.

Om du vill komma åt ett dataelement i anpassad kod använder du `getDataElementValue` -metod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName`skriver du följande: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash-objekt

I din egen kod kan du även använda `ruleStash` -objekt.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` är ett objekt som samlar in alla resultat från åtgärdsmoduler.

Varje tillägg har ett eget namnutrymme. Om tillägget till exempel har namnet `send-beacon`, alla resultat från `send-beacon` åtgärder lagras på `ruleStash['send-beacon']` namnutrymme.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

Namnutrymmet är unikt för varje tillägg och har värdet `undefined` i början.

Namnutrymmet åsidosätts med det returnerade resultatet från varje åtgärd. Det händer ingen namnrymdsmagi. Om du till exempel har en `transform` tillägg som innehåller två åtgärder: `generate-fullname` och `generate-fulladdress`lägger sedan till de två åtgärderna i en regel.

Om resultatet av `generate-fullname` åtgärden är `Firstname Lastname`visas regelstrecket på följande sätt när åtgärden har slutförts:

```js
{
  transform: 'Firstname Lastname`
}
```

Om resultatet av `generate-address` åtgärden är `3900 Adobe Way`visas regelstrecket på följande sätt när åtgärden har slutförts:

```js
{
  transform: '3900 Adobe Way`
}
```

Observera att `Firstname Lastname` finns inte längre i regelstrecket. Det beror på att `generate-address` åtgärden åsidosätter den med adressen.

Om du vill lagra resultaten från båda åtgärderna i `transform` namnutrymme i `ruleStash`kan du skriva en åtgärdsmodul som i följande exempel:

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

Första gången som den här åtgärden utförs är `ruleStash` är `undefined` och initieras med ett tomt objekt. Nästa gång åtgärden körs, `ruleStash` returneras av åtgärden när den anropades tidigare. Använda ett objekt som `ruleStash` Med kan du lägga till nya data utan att förlora data som tidigare angetts av andra åtgärder från tillägget.

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

**Lika med:** Villkoret returnerar true om de två värdena är lika med en icke-strikt jämförelse (i JavaScript == -operatorn). Värdena kan vara av alla typer. När du skriver ett ord som _true_, _false_, _null_, eller _undefined_ till ett värdefält jämförs ordet som en sträng och konverteras inte till JavaScript-motsvarigheten.

**Är inte lika med:** Villkoret returnerar true om de två värdena inte är lika med en icke-strikt jämförelse (i JavaScript är != operator). Värdena kan vara av alla typer. När du skriver ett ord som _true_, _false_, _null_, eller _undefined_ till ett värdefält jämförs ordet som en sträng och konverteras inte till JavaScript-motsvarigheten.

**Innehåller:** Villkoret returnerar true om det första värdet innehåller det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Innehåller inte:** Villkoret returnerar true om det första värdet inte innehåller det andra värdet. Tal konverteras till strängar. Alla värden förutom tal och strängar resulterar i att villkoret returnerar true.

**Börjar med:** Villkoret returnerar true om det första värdet börjar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Börjar inte med:** Villkoret returnerar true om det första värdet inte börjar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Slutar med:** Villkoret returnerar true om det första värdet slutar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Slutar inte med:** Villkoret returnerar true om det första värdet inte slutar med det andra värdet. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Matchar Regex:** Villkoret returnerar true om det första värdet matchar det reguljära uttrycket. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar false.

**Matchar inte Regex:** Villkoret returnerar true om det första värdet inte matchar det reguljära uttrycket. Tal konverteras till strängar. Alla värden utom ett tal eller en sträng resulterar i att villkoret returnerar true.

**Är mindre än:** Villkoret returnerar true om det första värdet är mindre än det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**är mindre än eller lika med:** Villkoret returnerar true om det första värdet är mindre än eller lika med det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är större än:** Villkoret returnerar true om det första värdet är större än det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**är större än eller lika med:** Villkoret returnerar true om det första värdet är större än eller lika med det andra värdet. Strängar som representerar tal konverteras till tal. Alla värden utom ett tal eller en konvertibel sträng resulterar i att villkoret returnerar false.

**Är sant:** Villkoret returnerar true om värdet är booleskt med värdet true. Värdet som du anger konverteras inte till ett booleskt värde om det är någon annan typ. Alla värden utom ett booleskt värde med värdet true returnerar villkoret false.

**Är sann:** Villkoret returnerar true om värdet är true efter att ha konverterats till ett booleskt värde. Se [MDN:s sanna dokumentation](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) för exempel på sanna värden.

**Är falskt:** Villkoret returnerar true om värdet är ett booleskt värde med värdet false. Värdet som du anger konverteras inte till ett booleskt värde om det är någon annan typ. Alla värden utom ett booleskt värde med värdet false resulterar i att villkoret returnerar false.

**Är falskt:** Villkoret returnerar true om värdet är false efter att det har konverterats till ett booleskt värde. Se [MDN:s Falsy-dokumentation](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) för exempel på falska värden.



## Åtgärdstyper för kärntillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Core-tillägget.

### Egen kod

Ange koden som körs efter att händelsen har utlösts och villkoren har utvärderats. Vidarebefordran av händelser i Adobe Experience Platform har stöd för ES6.

1. Namnge åtgärdskoden.
1. Välj **[!UICONTROL Open Editor]**.
1. Redigera koden och välj **[!UICONTROL Save]**.

Om du vill komma åt ett dataelement i anpassad kod använder du `getDataElementValue` -metod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName`skriver du följande: 

```javascript
getDataElementValue('productName') 
```

Vidarebefordrande åtgärder utförs sekventiellt. Det går också att returnera ett värde som kan användas i en efterföljande åtgärd för anpassad kod i en åtgärd. Det returnerade värdet kan komma från kod i den åtgärden eller från svarstexten för ett anrop till en extern källa. Om du vill referera till data från en tidigare utförd åtgärd i en enda regel där Core-tillägget används, skapar du ett dataelement av typen `Path` och använd följande sökväg för att referera till värdet för en variabel som anropas `productCategory` definieras i anpassad kod i Core-tillägget:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Dataelementtyper för kärntillägg

Dataelementtyperna bestäms av tillägget. Det finns ingen begränsning för de typer som kan skapas.

I följande avsnitt beskrivs de typer av dataelement som finns i Core-tillägget. Andra tillägg använder andra typer av dataelement.

### Egen kod

Du kan ange egen JavaScript i användargränssnittet genom att välja  **[!UICONTROL Open Editor]** och infoga kod i redigeringsfönstret.

En return-programsats krävs i redigeringsfönstret för att ange vilket värde som ska användas som dataelementvärde. Om en retursats inte ingår eller om värdet `null` eller `undefined` returneras, dataelementets standardvärde återspeglar `null` eller `undefined`.

Om du vill komma åt ett dataelement i anpassad kod använder du `getDataElementValue` -metod. Om du till exempel vill hämta värdet för ett dataelement med namnet `productName`skriver du följande: 

```javascript
getDataElementValue('productName') 
```

**Exempel:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Bana

En sökväg till ett nyckelvärdepar för en händelse som skickas till Adobe Experience Platform Edge Network kan refereras med hjälp av datatypen Path.

Om du vill referera till hela objektet för en händelse anger du `arc` som banan. Akronymen `arc` står för Adobe Resource Context och är den översta sökvägen för en händelse som skickas till Adobe Experience Platform Edge Network.

Med `interact` anrop från klienten till Edge Network har följande begäran från webbläsarkonsolen:

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

Ange en sökväg som refererar `pageName`anger du följande i sökvägsfältet:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>The `interact` anrop från klienten har `events`, men för vidarebefordran av händelser behöver du `event`. Detta beror på att vidarebefordran av händelser undersöker varje händelse individuellt och inte som en grupp med flera händelser som visas på klienten.
