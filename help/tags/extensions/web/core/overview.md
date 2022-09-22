---
title: Core Extension Overview
description: Läs mer om Core-taggtillägget i Adobe Experience Platform.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '5482'
ht-degree: 0%

---

# Översikt över Core Extension

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Core-taggtillägget är standardtillägget som släpps med Adobe Experience Platform.

Det här dokumentet innehåller information om de alternativ som är tillgängliga när du använder Core-tillägget för att skapa en regel.

## Huvudtilläggshändelsetyper {#core-extension-event-types}

I det här avsnittet beskrivs de händelsetyper som finns i Core-tillägget. Mer information om alternativen som kan anges för flera olika händelsetyper finns i [Alternativ](#options) -avsnitt.

### Webbläsarbaserade händelser

#### Tabboskärpa

Händelsen tab-blur utlöser åtgärden när en flik förlorar fokus. Det finns inga inställningar för den här händelsetypen.

#### Flikfokus

Händelsen tab-focus utlöser åtgärden när en flik får fokus. Det finns inga inställningar för den här händelsetypen.

### Formulär

#### Oskärpa

Oskärpehändelsen utlöser åtgärden när ett formulär förlorar fokus. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Fokus

Fokushändelsen utlöser åtgärden när ett formulär får fokus. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Skicka

Skicka-händelsen utlöser åtgärden när ett formulär skickas. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

### Tangentbordskontrollerade händelser

#### Tryck på tangenten

Händelsen utlöses när en tangent trycks ned. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

### Mediebaserade händelser

#### Media avslutad

Händelsen utlöses när mediet avslutas. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Medieladdade data

Händelsen utlöses när mediet läser in data. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Pausa media

Händelsen utlöses när mediet pausas. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Media Play

Händelsen utlöses när mediet spelas upp. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Media är installerade

Händelsen utlöses om mediet stannar. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Media-Time Play

Händelsen utlöses om mediet spelas upp under en viss tid. Du måste ange hur länge mediet måste spelas upp för att händelsen ska kunna utlösas. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.


#### Media-Volume har ändrats

Händelsen utlöses om volymen höjs eller sänks. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

### Mobilorienterade händelser

#### Orienteringsändring

Händelsen utlöses om enhetens orientering ändras. Du måste ange hur länge orienteringen måste ändras för att händelsen ska kunna utlösas. Det finns inga inställningar för den här händelsetypen.

#### Zoomändring

Händelsen utlöses om användaren zoomar in eller ut. Det finns inga inställningar för den här händelsetypen.

### Musstyrda händelser

#### Klicka på

Händelsen utlöses om det angivna elementet är markerat (klickat). Du kan också ange egenskapsvärden som måste vara true för elementet innan händelsen aktiveras.

Om elementet är en ankartagg (`<a>`) för länkat innehåll kan du även ange om navigeringen ska fördröjas under en viss tidsperiod. Detta kan vara användbart om regeln kräver extra tid för att köras och vanligtvis inte skulle slutföras innan sidnavigeringen utförs.

>[!WARNING]
>
>Detta alternativ bör användas med extrem försiktighet på grund av de potentiella negativa konsekvenser det kan få för användarupplevelsen om det används felaktigt.

När du använder fördröjning av länkar förhindrar Platform faktiskt webbläsaren från att navigera utanför sidan. Sedan utförs en JavaScript-omdirigering till det ursprungliga målet efter den angivna tidsgränsen. Detta är särskilt farligt när sidmarkeringen har `<a>` -taggar där den tänkta funktionen egentligen inte navigerar användaren bort från sidan. Om du inte kan lösa problemet på något annat sätt bör du vara mycket exakt med väljardefinitionen så att den här händelsen utlöses exakt där du behöver den och inte någon annanstans.

Standardvärdet för fördröjning av länkar är 100 millisekunder. Observera att taggar alltid väntar på den angivna tiden och inte är kopplade till körningen av regelns åtgärder på något sätt. Det är möjligt att fördröjningen tvingar användaren att vänta längre än nödvändigt och även att fördröjningen inte är tillräckligt lång för att alla regelåtgärder ska kunna slutföras. Längre fördröjningar ger mer tid för regelkörning men försämrar även användarupplevelsen.

För att aktivera fördröjningen måste du ange både det valda elementet som utlöser händelsen och den specifika tiden innan händelsen utlöses.

Avancerade alternativ finns i [Alternativ](#options) för mer information.

#### Hovra

Händelsen utlöses om användaren hovrar över ett angivet element. Du måste också konfigurera om regeln aktiveras omedelbart eller efter ett visst antal millisekunder. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

### Andra händelser

#### Egen händelse

Händelsen utlöses om en anpassad händelsetyp inträffar. Namngivna JavaScript-funktioner som definieras någon annanstans i kodbasen kan användas som en anpassad händelsetyp. Du måste ange namnet på den anpassade händelsetypen och konfigurera andra inställningar enligt beskrivningen i [Alternativ](#options) nedan.

#### Dataelementet har ändrats

Händelsen utlöses om ett angivet dataelement ändras. Du måste ange ett namn för dataelementet. Du kan markera dataelementet genom att antingen skriva dess namn i textfältet eller genom att markera dataelementsikonen till höger om textfältet och välja i en lista som finns i dialogrutan som visas.

#### Direktsamtal {#direct-call-event}

En direktanropshändelse kringgår system för händelsidentifiering och sökning. Regler för direktsamtal är idealiska för situationer där du vill tala om för systemet exakt vad som händer. De är också idealiska när systemet inte kan identifiera någon händelse i DOM.

När du definierar en direktanropshändelse måste du ange en sträng som ska fungera som den här händelsens identifierare. Om en [aktivera direktanrop](#direct-call-action) som innehåller samma identifierare utlöses, kommer alla regler för direktanropshändelser som lyssnar efter den identifieraren att köras.

![Skärmbild av en direktanropshändelse i användargränssnittet för datainsamling](../../../images/extensions/core/direct-call-event.png)

#### Elementet finns

Händelsen utlöses om ett angivet element finns. Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Enters Viewport

Händelsen utlöses om användaren anger en angiven visningsruta. Du måste ange en CSS-väljare som ett villkor för att kunna ange matchande element som mål. Du måste också konfigurera om regeln aktiveras omedelbart eller efter ett visst antal millisekunder, och om händelsen ska utlösas varje gång händelsen inträffar eller endast första gången.

Se [Alternativ](#options) för mer information om anpassningsbara händelseinställningar.

#### Historikändring

Händelsen utlöses om en pushState- eller hashchange-händelse inträffar. Det finns inga inställningar för den här händelsetypen.

#### Tidsåtgång på sidan

Händelsen utlöses om användaren finns kvar på sidan under ett visst antal sekunder. Du måste ange hur många sekunder som måste skickas innan händelsen aktiveras.

### Sidladdningshändelser

#### DOM-klart

Händelsen utlöses när DOM är klar och användaren kan interagera med sidan. Det finns inga inställningar för den här händelsetypen.

#### Bibliotek inläst (sidan ovanpå) {#library-loaded-page-top}

Händelsen utlöses så snart som taggbiblioteket har lästs in. Det finns inga inställningar för den här händelsetypen.

#### Sidan nederst {#page-bottom}

Händelsen utlöses en gång `_satellite.pageBottom();` har anropats. När du läser in taggbiblioteket asynkront bör den här händelsetypen inte användas. Det finns inga inställningar för den här händelsetypen.

#### Fönster inläst

Händelsen utlöses när onLoad anropas av webbläsaren och sidan har lästs in. Det finns inga inställningar för den här händelsetypen.

### Alternativ {#options}

Var och en av formulärhändelsetyperna använder följande inställningar:

#### Specifika element \| Alla element

* Om du väljer **[!UICONTROL Specific Elements]** visas alternativen för att välja element och egenskapsvärden.
* Om du väljer **[!UICONTROL Any Element]**, det finns inga fler alternativ som behöver göras för att begränsa elementen.

#### Element som matchar CSS-väljaren

Ange CSS-väljaren som identifierar elementen som utlöser händelsen.

#### Och har vissa egenskapsvärden

Om du väljer det här alternativet blir följande parametrar tillgängliga:

* `property=value`

   Ange värdet för egenskapen

* Regex

   Aktivera om `property=value` är ett reguljärt uttryck.

* Lägg till

   Lägg till ytterligare `property=value` par.

#### Avancerade alternativ (Bubbling)

* Kör den här regeln även när händelsen kommer från ett underordnat element
* Tillåt att den här regeln körs även om händelsen redan har utlöst en regel som riktar sig till ett underordnat element
* När regeln har körts kan du förhindra att händelsen utlöser regler för överordnade element

## Villkorstyper för kärntillägg

I det här avsnittet beskrivs de villkorstyper som finns i Core-tillägget. Dessa villkorstyper kan användas med antingen den vanliga typen eller undantagstypen av logik.

### Data

#### Cookie

Ange det cookie-namn och värde som måste finnas för att en händelse ska kunna utlösa en åtgärd.

1. Ange ett cookie-namn.
1. Ange det värde som måste finnas i cookien om händelsen ska utlösa en åtgärd.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

#### Egen kod

Ange eventuell anpassad kod som måste finnas som villkor för händelsen.

>[!NOTE]
>
>ES6+ JavaScript stöds nu i anpassad kod. Observera att vissa äldre webbläsare inte stöder ES6+. Om du vill förstå hur funktionerna i ES6+ påverkas testar du mot alla webbläsare som bör stödjas.

Använd den inbyggda kodredigeraren för att ange egen kod:

1. Välj **[!UICONTROL Open Editor]**.
1. Skriv den anpassade koden.
1. Välj **[!UICONTROL Save]**.

En variabel med namnet `event` kommer automatiskt att vara tillgängligt, vilket du kan referera till inifrån din anpassade kod. The `event` -objektet innehåller användbar information om händelsen som utlöste regeln. Det enklaste sättet att avgöra vilka händelsedata som är tillgängliga är att logga `event` till konsolen inifrån din egen kod:

```javascript
console.log(event);
return true;
```

Kör regeln i en webbläsare och inspektera det loggade händelseobjektet i webbläsarens konsol. När du förstår vilken information som är tillgänglig kan du använda den för programmatisk beslutsfattande i din anpassade kod.

*Villkorssekvenser*

När alternativet Kör regelkomponenter i sekvens från egenskapsinställningarna är aktiverat kan efterföljande regelkomponenter vänta medan villkoret utför en asynkron åtgärd.

När villkoret returnerar [Lova](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)kommer nästa villkor i regeln inte att köras förrän det returnerade löftet är löst. Om löftet avvisas anser taggarna att villkoret är misslyckat och inga ytterligare villkor eller åtgärder från den regeln kommer att utföras.

Ett exempel på ett villkor som returnerar ett löfte:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Värdejämförelse {#value-comparison}

Jämför två värden för att avgöra om villkoret returnerar true.

Om du har en regel med flera villkor är det möjligt att det här villkoret returnerar true, men regeln utlöses inte eftersom de andra villkoren utvärderas som false eller ett av undantagen utvärderas som sant.

1. Ange ett värde.
1. Markera operatorn. Mer information finns i listan över operatorer för värdejämförelse nedan.
1. (Om det behövs) Välj om jämförelsen ska vara skiftlägeskänslig.
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

#### Variabel

Ange JavaScript-variabelns namn och värde som måste finnas för att en händelse ska kunna utlösa en åtgärd.

1. Ange JavaScript-variabelnamnet.
1. Ange det variabelvärde som måste finnas som villkor för händelsen.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

### Engagemang

#### Landningssida

Ange den sida som användaren måste logga in på för att utlösa händelsen.

1. Ange landningssidan.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

#### Ny/återkommande besökare

Ange om besökaren ska vara en ny besökare eller en återkommande besökare för en händelse som ska utlösa en åtgärd.

Välj något av följande:

* Ny besökare
* Returnerar besökare

#### Sidvisningar

Konfigurera det antal gånger besökaren måste visa sidan innan åtgärden aktiveras.

1. Välj om antalet sidvyer måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet sidvisningar som avgör om villkoret är uppfyllt eller inte.
1. Konfigurera när sidvyerna ska räknas genom att välja något av följande:
   * Livstid
   * Aktuell session

#### Sessioner

Utlös åtgärden om användarens antal sessioner uppfyller de angivna villkoren.

1. Välj om antalet sessioner måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet sessioner som avgör om villkoret är uppfyllt.

#### Tid på plats

Utlös åtgärden om användarens antal sessioner uppfyller de angivna villkoren.

Konfigurera hur länge besökaren måste vara på platsen innan åtgärden aktiveras.

1. Ange om antalet minuter som besökaren finns på platsen måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet minuter som avgör om villkoret är uppfyllt.

#### Trafikkälla

Utlös åtgärden om användarens antal sessioner uppfyller de angivna villkoren.

Ange källan för besökarens trafik som måste vara true för att åtgärden ska aktiveras.

1. Ange trafikkällan.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

### Teknik

#### Webbläsare

Välj den webbläsare som besökaren måste använda för att åtgärden ska aktiveras.

Välj en eller flera av följande webbläsare:

* Krom
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Enhetstyp

Välj den enhetstyp som besökaren måste använda för att åtgärden ska aktiveras.

Välj en eller flera av följande enhetstyper:

* Android
* Blackberry
* Skrivbord
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operativsystem

Välj det operativsystem som besökaren måste använda för att åtgärden ska aktiveras.

Välj ett eller flera av följande operativsystem:

* Android
* Blackberry
* iOS
* Linux
* macOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Skärmupplösning

Välj den skärmupplösning besökarna måste använda på sina enheter för att åtgärden ska aktiveras.

1. Välj om skärmupplösningsbredden för besökarens enhet måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet pixlar som krävs för skärmupplösningens bredd.
1. Välj om skärmupplösningshöjden för besökarens enhet måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet pixlar som krävs för skärmupplösningshöjden.

#### Fönsterstorlek

Välj den fönsterstorlek besökarna måste använda på sina enheter för att åtgärden ska aktiveras.

1. Välj om fönsterstorleksbredden för besökarens enhet måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet pixlar som krävs för fönstrets storleksbredd.
1. Välj om fönsterstorlekshöjden för besökarens enhet måste vara större än, lika med eller mindre än det angivna värdet.
1. Ange antalet pixlar som krävs för fönstrets storlekshöjd.

### URL

#### Domän

Ange besökarens domän.

#### Hash

Ange ett eller flera hash-mönster som måste finnas i URL:en.

>[!NOTE]
>
>Flera hash-mönster förenas med en OR.

1. Ange hash-mönstret.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.
1. Lägg till andra hash-mönster.

#### Sökväg och frågesträng

Ange en eller flera sökvägar som måste finnas i URL:en.  Detta inkluderar sökvägen och frågesträngen.

>[!NOTE]
>
>Flera banor förenas med en OR.

1. Ange sökvägen.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.
1. Lägg till andra sökvägar.

#### Sökväg utan frågesträng

Ange en eller flera sökvägar som måste finnas i URL:en.  Detta inkluderar sökvägen, men inkluderar inte frågesträngen.

>[!NOTE]
>
>Flera banor förenas med en OR.

1. Ange sökvägen.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.
1. Lägg till andra sökvägar.

#### Protokoll

Ange det protokoll som används i URL:en.

Välj något av följande:

* HTTP
* HTTPS

#### Frågesträngsparameter

Ange URL-parametern som används i URL:en.

1. Ange ett URL-parameternamn.
1. Ange det värde som används för URL-parametern.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.

#### Underdomän

Ange en eller flera underdomäner som måste finnas i URL:en.

>[!NOTE]
>
>Flera underdomäner förenas med en OR.

1. Ange underdomänen.
1. (Valfritt) Aktivera Regex om det här är ett reguljärt uttryck.
1. Lägg till andra underdomäner.

### Övriga

#### Datumintervall

Ange ett datumintervall. Välj det datum och den tidpunkt som händelsen inträffar efter, det datum den inträffar före och tidszonen.

#### Maximal frekvens

Ange det maximala antalet gånger som villkoret returnerar true. Du kan välja mellan följande alternativ:

* Sidvy
* Sessioner
* Besökare
* Sekunder
* Minuter
* Dagar
* Veckor
* Månader

För villkorets maximala frekvens 1 per session är dessa två `localStorage` objekten jämförs. Om `visitorTracking.sessionCount` är större än `maxFrequency.session` antal, samplingsvillkoret är sant. Om de är lika är villkoret false.

`sessionCount` är en `visitorTracking` så du måste aktivera besökar-API:t för att samplingsvillkoret ska fungera.

#### Provtagning

Ange hur många procent av tiden som villkoret returnerar true.

## Åtgärdstyper för kärntillägg

I det här avsnittet beskrivs de åtgärdstyper som finns i Core-tillägget.

### Egen kod

>[!NOTE]
>
>ES6+ JavaScript stöds nu i anpassad kod. Observera att vissa äldre webbläsare inte stöder ES6+. Om du vill förstå hur funktionerna i ES6+ påverkas testar du mot alla webbläsare som bör stödjas.

Ange koden som körs efter att händelsen har utlösts och villkoren har utvärderats.

1. Namnge åtgärdskoden.
1. Välj det språk som ska användas för att definiera åtgärden:
   * JavaScript
   * HTML
1. Välj om åtgärdskoden ska köras globalt.
1. Välj **[!UICONTROL Open Editor]**.
1. Redigera koden och välj **[!UICONTROL Save]**.

När JavaScript är valt som språk, en variabel med namnet `event` kommer automatiskt att vara tillgängligt, vilket du kan referera till inifrån din anpassade kod. The `event` -objektet innehåller användbar information om händelsen som utlöste regeln. Det enklaste sättet att avgöra vilka händelsedata som är tillgängliga är att logga `event` till konsolen inifrån din egen kod:

```javascript
console.log(event);
```

Kör regeln i en webbläsare och inspektera det loggade händelseobjektet i webbläsarens konsol. När du har förstått vilken information som är tillgänglig kan du använda den för programmatiskt beslutsfattande i din anpassade kod och skicka en del av `event` till en server och så vidare.

### Bearbetning av anpassad kodåtgärd

Tillägget Core, som är tillgängligt för alla Adobe Experience Platform-användare, innehåller en anpassad kodsåtgärd för att köra JavaScript eller HTML som tillhandahålls av användaren. Det är ofta användbart för användare att förstå hur regler med anpassade kodåtgärder behandlas.

#### Regler som använder händelserna top eller page bottom

Kod från anpassade åtgärder bäddas in i huvudtaggbiblioteket. Koden skrivs till dokumentet med document.write. Om en regel har flera åtgärder för anpassad kod, skrivs koden i den ordning som konfigurerats i regeln.

#### Regler som använder någon annan händelse än sidans överkant eller sidans nederkant

Kod från anpassade åtgärder läses in från servern och skrivs till dokumentet med [Postscribe](https://github.com/krux/postscribe). Om en regel har flera åtgärder för anpassad kod läses koden in parallellt från servern, men skrivs i den ordning som konfigurerats i regeln.

När du använder document.write efter att en sida har lästs in uppstår vanligtvis problem, men det här är inte något problem för kod som tillhandahålls via anpassade kodåtgärder. Du kan använda åtgärderna document.write i Custom Code oavsett när koden kommer att köras.

#### Anpassad kodvalidering

Valideraren som används i kodredigeraren är utformad för att identifiera problem med kod som skrivits av utvecklare. Kod som har genomgått en miniatyrprocess, t.ex. den AppMeasurement.js-kod som hämtats från kodhanteraren, kan felaktigt flaggas som att valideraren har problem, vilket vanligtvis kan ignoreras.

#### Åtgärdssekvenser

När alternativet Kör regelkomponenter i sekvens från egenskapsinställningarna är aktiverat kan efterföljande regelkomponenter vänta medan åtgärden utför en asynkron åtgärd.  Detta fungerar annorlunda för JavaScript och HTML.

*JavaScript*

När du skapar en anpassad JavaScript-kodsåtgärd kan du returnera en [Lova](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) från ditt agerande. Nästa åtgärd i regeln kommer endast att utföras när det returnerade löftet är löst. Om löftet avvisas kommer nästa åtgärd från regeln inte att utföras.

>[!NOTE]
>
>Detta fungerar bara när ditt JavaScript inte är inställt på att köras globalt. Om du kör din anpassade kodsåtgärd i det globala omfånget behandlas löftet som omedelbart löst och nästa objekt i bearbetningskön flyttas.

Ett exempel på en anpassad JavaScript-kodsåtgärd som returnerar ett löfte:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

När du skapar en anpassad kodsåtgärd för HTML, en funktion med namnet `onCustomCodeSuccess()` kan användas i din egen kod. Du kan anropa den här funktionen för att ange att din egen kod har slutförts och att taggarna kan fortsätta att köra efterföljande åtgärder. Å andra sidan kan du anropa `onCustomCodeFailure()`. Detta informerar taggar om att inte köra efterföljande åtgärder från den regeln.

Ett exempel på en anpassad kodåtgärd för HTML som använder de nya återanropen:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### Utlös direktanrop {#direct-call-action}

Den här åtgärden aktiverar alla regler som använder en specifik [direktanrop](#direct-call-event). När du konfigurerar åtgärden måste du ange identifierarsträngen för den direktanropshändelse som du vill utlösa. Du kan också skicka data till direktsamtalshändelsen via en `detail` -objekt, som kan innehålla en anpassad uppsättning nyckelvärdepar.

![Skärmbild av en direktanropsåtgärd för utlösare i användargränssnittet för datainsamling](../../../images/extensions/core/direct-call-action.png)

Åtgärden mappar direkt till [`track` method](../../../ui/client-side/satellite-object.md?lang=en#track) i `satellite` -objekt, som kan nås av kod på klientsidan.

## Dataelementtyper för kärntillägg

Dataelementtyperna bestäms av tillägget. Det finns ingen begränsning för de typer som kan skapas.

I följande avsnitt beskrivs de typer av dataelement som finns i Core-tillägget. Andra tillägg använder andra typer av dataelement.

### Cookie

Alla tillgängliga domäncookies kan refereras i fältet för cookie-namn.

#### Exempel:

`cookieName`

### Konstant

Alla konstanta strängvärden som sedan kan refereras i åtgärder eller villkor.

#### Exempel:

`string`

### Egen kod

>[!NOTE]
>
>ES6+ JavaScript stöds nu i anpassad kod. Observera att vissa äldre webbläsare inte stöder ES6+. Om du vill förstå hur funktionerna i ES6+ påverkas testar du mot alla webbläsare som bör stödjas.

Du kan ange egen JavaScript i användargränssnittet genom att välja Öppna redigerare och infoga kod i redigeringsfönstret.

En return-programsats krävs i redigeringsfönstret för att ange vilket värde som ska användas som dataelementvärde. Om en retursats inte ingår eller om värdet `null` eller `undefined` returneras kommer dataelementets standardvärde att användas som dataelementvärde.

**Exempel:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Om det anpassade kodelementet hämtas som en del av en regelkörning, är det en variabel med namnet `event` blir automatiskt tillgängligt, som du kan referera till inifrån din anpassade kod. The `event` -objektet innehåller användbar information om händelsen som utlöste regeln. Det enklaste sättet att avgöra vilka händelsedata som är tillgängliga är att logga `event` till konsolen inifrån din egen kod:

```javascript
console.log(event);
return true;
```

Kör regeln i en webbläsare och inspektera det loggade händelseobjektet i webbläsarens konsol. När du förstår vilken information som är tillgänglig enligt de olika regler som kan använda ditt dataelement, kan du använda den för programmatisk beslutsfattande inom din anpassade kod eller returnera en del av `event` -objektet som dataelementets värde.

### DOM-attribut

Alla elementvärden kan hämtas, till exempel en div- eller H1-tagg.

#### Exempel:

CSS-väljarkedja:

`id#dc logo img`

Hämta värdet för:

`src`

### JavaScript-variabel

Alla tillgängliga JavaScript-objekt eller -variabler kan refereras med sökvägsfältet.

Element i taggdata kan användas för att hämta JavaScript-variabler eller objektegenskaper för kod. Dessa värden kan sedan användas i tilläggen eller anpassade regler genom att referera till taggdataelementen. Om datakällan ändras är det bara nödvändigt att uppdatera referensen till källan i användargränssnittet för datainsamling.

I exemplet nedan innehåller koden en JavaScript-variabel som kallas `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

När du skapar dataelementet i användargränssnittet för datainsamling anger du bara sökvägen till variabeln.

Om du använder ett datainsamlarobjekt som en del av datalagret använder du punktnotation i sökvägen för att referera till det objekt och den egenskap som du vill hämta till dataelementet, som `_myData.pageName`, eller `digitalData.pageName`och så vidare.

#### Exempel:

`window.document.title`

### Lokal lagring

Ange namnet på det lokala lagringsobjektet i fältet Namn på lokal lagringsobjekt.

Med lokal lagring kan webbläsare lagra information från sida till sida ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Lokal lagring fungerar ungefär som cookies, men är mycket större och mer flexibel.

Använd det angivna fältet för att ange värdet som du skapade för ett lokalt lagringsobjekt, till exempel `lastProductViewed.`

### Sammanfogade objekt

Markera flera dataelement som vart och ett ska ge ett objekt. Objekten sammanfogas i hög grad (rekursivt) för att skapa ett nytt objekt. Källobjekten ändras inte. Om en egenskap hittas på samma plats på flera källobjekt används värdet från det senare objektet. Om ett källegenskapsvärde är `undefined`, åsidosätter det inte ett värde från ett tidigare källobjekt. Om arrayer finns på samma plats på flera källobjekt sammanfogas arrayerna.

Anta till exempel att du väljer ett dataelement som innehåller följande objekt:

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Anta också att du väljer ett annat dataelement som innehåller följande objekt:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

Resultatet av dataelementet för sammanfogade objekt blir följande objekt:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Sidinformation

Använd dessa datapunkter för att samla in sidinformation som kan användas i regellogiken eller för att skicka information till Analytics eller externa spårningssystem.

Du kan välja något av följande sidattribut som ska användas i dataelementet:

* URL
* Värdnamn
* Bannamn
* Protokoll
* Referent
* Titel

### Frågesträngsparameter

Ange en enda URL-parameter i fältet URL-parameter.

Endast namnavsnittet är nödvändigt och alla specialdesigners som &quot;?&quot; eller &quot;=&quot;bör utelämnas

#### Exempel:

`contentType`

### Slumpmässigt tal

Använd det här dataelementet för att generera ett slumpmässigt tal. Det används ofta för att ta prov på data eller skapa ID:n, till exempel ett träff-ID. Det slumpmässiga talet kan användas till att dölja eller salta känsliga data. Några exempel kan vara:

* Generera ett träff-ID
* Sammanfoga numret till en användartoken eller tidsstämpel för att säkerställa unikhet
* Gör en enkelriktad hash av PII-data
* Bestäm slumpmässigt när en undersökningsförfrågan ska visas på webbplatsen

Ange minimi- och maximivärden för det slumpmässiga talet.

**Standardvärden:**

Minimum: 0

Maximum: 1000000000

### Sessionslagring

Ange namnet på sessionslagringsobjektet i fältet Namn på sessionslagringsobjekt.

Sessionslagring liknar lokal lagring, förutom att data tas bort efter att sessionen har avslutats, medan lokala lager eller en cookie kan behålla data.

### Beteende för besökare

På liknande sätt som i Sidinformation använder det här dataelementet vanliga beteendetyper för att utöka logiken i regler och andra plattformslösningar.

Välj ett av följande attribut för besökarbeteende:

* Landningssida
* Trafikkälla
* Minuter på plats
* Antal sessioner
* Antal sessionssidesvisningar
* Antal sidvisningar under livstid
* Är ny besökare

Några vanliga användningsområden:

* Visa en enkät när en besökare har varit på webbplatsen i fem minuter
* Om det här är landningssidan för besöket fyller du i en analysmätning
* Visa ett nytt erbjudande till besökaren efter X antal sessioner
* Visa ett nyhetsbrev om detta är en första besökare

### Villkorligt värde

En wrapper för [Värdejämförelse](#value-comparison-value-comparison) villkor. Baserat på resultatet av jämförelsen returnerar ett av de två tillgängliga värdena i formuläret. Kan på så sätt hantera &quot;If... Sedan.. Annars..&quot; utan extra regler.

### Körningsmiljö

Gör att du kan välja en av följande variabler:

* Miljöfas - Returer `_satellite.environment.stage` för att skilja mellan utvecklings-, staging- och produktionsmiljöer.
* Bygge bibliotek - returnerar `turbine.buildInfo.buildDate` som innehåller samma värde som `_satellite.buildInfo.buildDate`.
* Egenskapsnamn - returnerar `_satellite.property.name` för att hämta namnet på Launch-egenskapen.
* Egenskaps-ID - Returnerar `_satellite.property.id` för att hämta ID:t för Launch-egenskapen
* Regelnamn - returnerar `event.$rule.name` som innehåller namnet på den körda regeln.
* Regel-ID - returnerar `event.$rule.id` som innehåller ID:t för den körda regeln.
* Händelsetyp - Returer `event.$type` som innehåller den typ av händelse som utlöste regeln.
* Nyttolast för händelseinformation - Returer `event.detail` som innehåller nyttolasten för en anpassad händelse eller regel för direktanrop.
* Identifierare för direktanrop - Returer `event.identifier` som innehåller identifieraren för en regel för direktsamtal.

### Enhetsattribut

Returnerar ett av följande attribut för besökarenhet:

* Storlek på webbläsarfönster
* Skärmstorlek

### JavaScript-verktyg

Det är en wrapper för vanliga JavaScript-åtgärder. Den tar emot ett dataelement som indata. Den returnerar resultatet av en av följande omformningar av dataelementvärdet:

* Grundläggande strängändring (ersätt, delsträng, regex-matchning, första och sista indexvärdet, dela, segment)
* Grundläggande matrisåtgärder (segment, join, pop, shift)
* Grundläggande universella åtgärder (segment, längd)