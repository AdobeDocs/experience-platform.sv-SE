---
title: Dataelement
description: Dataelement är byggstenarna för dataordlistan (eller datamappningen). Använd dataelement för att samla in, ordna och leverera data över marknadsförings- och annonseringsteknologier.
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 3%

---

# Dataelement

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Dataelement är byggstenarna för dataordlistan (eller datamappningen). Använd dataelement för att samla in, ordna och leverera data över marknadsförings- och annonseringsteknologier.

Ett enskilt dataelement är en variabel vars värde kan mappas till frågesträngar, URL:er, cookie-värden, JavaScript-variabler osv. Du kan referera till det här värdet genom dess variabelnamn i hela Adobe Experience Platform. Den här samlingen dataelement blir en ordbok med definierade data som du kan använda för att skapa regler (händelser, villkor och åtgärder). Den här dataordlistan delas mellan taggar och kan användas med alla tillägg som du har lagt till i egenskapen.

>[!IMPORTANT]
>
>Ändringarna börjar inte gälla förrän de [publiceras](../publishing/overview.md).

Använd dataelement i så stor omfattning som möjligt genom hela regelskapandet för att konsolidera definitionen av dynamiska data och förbättra effektiviteten i taggningsprocessen. Du definierar dataregler en gång och använder dem sedan på flera ställen.

Begreppet återanvändbara dataelement är mycket kraftfullt och du bör använda dem som bästa praxis.

Om det till exempel finns ett visst sätt att referera till sidnamn eller produkt-ID:n eller hämta information från frågesträngsparametrar från en filialmarknadsföringslänk eller från [!DNL AdWords] och så vidare, kan du skapa en dataordlista (dataelement) genom att hämta information från dess källa och sedan använda dessa data i olika taggregler.

Anta att du använder ett visst sidnamn som exempel genom att referera till ett datalager, `document.title`-element eller en rubriktagg på webbplatsen. Med taggar i Adobe Experience Platform kan du skapa ett dataelement som en enda referenspunkt för den aktuella datapunkten. Du kan sedan använda det här dataelementet i alla regler som behöver referera till sidnamnet. Om du av någon anledning i framtiden bestämmer dig för att ändra sättet som du refererar till sidnamnet (du har t.ex. refererat till `document.title` men nu vill referera till ett visst datalager), behöver du inte redigera många olika regler för att ändra den referensen. Du ändrar bara referensen en gång i dataelementet och alla regler som refererar till det dataelementet uppdateras automatiskt.

>[!NOTE]
>
>Om det inte finns någon referens till ett dataelement i en regel, läses det inte in på någon sida såvida det inte anropas specifikt i det anpassade skriptet

Dataelement fylls i med data när de används i regler eller när de anropas manuellt i ett skript. På en hög nivå:

1. [Skapa ett dataelement](#create-a-data-element) om du inte redan har gjort det.
1. Använd dataelementet i en [regel](./rules.md) eller ett anpassat skript.

## Användning av dataelement

### I regler

Du kan använda dataelement i redigeringsgränssnittet för regler genom att använda sökrutan för att hitta dataelementets namn.

### I anpassat skript

Du kan använda dataelement i egna skript med objektsyntaxen `_satellite`:

`_satellite.getVar('data element name');`

## Skapa ett dataelement {#create-a-data-element}

Dataelement är byggstenarna för regler. Med dataelement kan du skapa ett datalexikon (eller datamappning) med vanliga objekt på en sida, oavsett varifrån de kommer (frågesträngar, URL:er eller cookie-värden) för alla objekt som finns på webbplatsen.

1. Öppna fliken [!UICONTROL Data Elements] på en egenskapssida och välj sedan **[!UICONTROL Create New Data Element]**.
1. Namnge dataelementet.
1. Välj ett tillägg och skriv.

   De tillgängliga elementtyperna för data bestäms av tillägget. Mer information om vilka typer som är tillgängliga med Core-taggtillägget finns i [Typer av dataelement](data-elements.md#types-of-data-elements).

1. Ange eventuell begärd information om den valda typen i fälten.
1. (Valfritt) Ange ett standardvärde.

   Om du inte markerar det här alternativet finns det inget standardvärde.  De flesta användare låter detta vara i standardläge.  Olika system hanterar en tom variabel på olika sätt.  Vissa användare väljer att ange något som &quot;none&quot; eller &quot;n/a&quot; så att de kan skapa en konsekvent rapportering när dataelementet inte returnerar något värde.

1. Välj om ett värde med gemener ska framtvingas och om radbrytningar och mellanslag ska tas bort.
1. Välj en varaktighet.

   De tillgängliga alternativen är:

   * Ingen
      * Värdet lagras inte.
   * Sidvy
      * Värdet hålls i en JavaScript-variabel tills sidan uppdateras eller en ny sida läses in.
      * Kan skapas och anges i skript med objektsyntaxen `_satellite`:

        `_satellite.setVar('data_element_name')`
   * Session
      * Värdena behålls i webbläsarens sessionslagring tills webbläsarfliken stängs.
      * Tillgängligt under hela webbplatsbesöket.
   * Besökare
      * Värdet lagras oändligt i webbläsarens lokala lager.

1. Välj **[!UICONTROL Save]**.

När du skapar eller redigerar element kan du spara och skapa i ditt [aktiva bibliotek](../publishing/libraries.md#active-library). Ändringen sparas omedelbart i biblioteket och en bygge körs. Byggets status visas. Du kan också skapa ett nytt bibliotek från listrutan [!UICONTROL Active Library].

## Typer av dataelement {#types-of-data-elements}

>[!NOTE]
>
>Dataelementtyperna bestäms av tillägget. Det finns ingen begränsning för de typer som kan skapas.

I följande avsnitt beskrivs de typer av dataelement som är tillgängliga i **Core-tillägget**. Andra tillägg använder andra typer av dataelement.

### Cookie

Alla tillgängliga domäncookies kan refereras i fältet för cookie-namn.

#### Exempel:

`cookieName`

### Egen kod

Du kan ange anpassade JavaScript-filer i användargränssnittet genom att markera [!UICONTROL Open Editor] och infoga kod i redigeringsfönstret.

En return-programsats krävs i redigeringsfönstret för att ange vilket värde som ska anges som dataelementvärde. Om ingen retursats ingår tolkas dataelementet till `undefined`.  Detta utlöser reservkontrollen för att leta efter ett lagrat värde och sedan ett standardvärde om det inte finns något lagrat värde.

**Exempel:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Anpassad kod kan acceptera objektet `event` från anropsregeln som ett argument. Detta gör att koden kan läsa värdet där.

**Exempel:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Du kan sedan använda detta i egna skript med objektsyntaxen `_satellite`:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

När du använder procentsyntax (`%`) behöver du bara ange dataelementets namn. Du behöver inte ange `event`.

```text
%data element name%
```

### DOM-attribut

Alla elementvärden kan hämtas, till exempel en div- eller H1-tagg.

#### Exempel:

CSS-väljarkedja:

`id#dc logo img`

Hämta värdet för:

`src`

### JavaScript-variabel

Alla tillgängliga JavaScript-objekt eller -variabler kan refereras med sökvägsfältet.

Om du vill samla in JavaScript-variabler eller objektegenskaper i koden och använda dem med något av dina tillägg eller regler, kan dataelement användas för att hämta dessa värden. På så sätt kan du referera till dataelementet i alla regler, och om datakällan ändras behöver du bara ändra referensen till källan (dataelementet) på ett ställe.

Anta att din kod innehåller en JavaScript-variabel som heter `Page_Name`, så här:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Du måste ange sökvägen till variabeln när du skapar dataelementet.

Om du använder ett datainsamlarobjekt som en del av datalagret använder du bara punktnotation i sökvägen för att referera till objektet och egenskapen som du vill hämta till dataelementet, till exempel `_myData.pageName` eller `digitalData.pageName`.

#### Exempel:

`window.document.title`

### Lokal lagring

Ange namnet på ditt lokala lagringsobjekt i fältet [!UICONTROL Local Storage Item Name].

Med hjälp av det lokala lagringsutrymmet kan webbläsare lagra information från sida till sida ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Lokal lagring fungerar mycket som cookies, men är mycket större och mer flexibel.

Använd det angivna fältet för att ange värdet som du skapade för ett lokalt lagringsobjekt, till exempel `lastProductViewed.`

### Sidinformation

Använd dessa datapunkter för att hämta sidinformation som kan användas i regellogiken eller för att skicka information till [!DNL Analytics] eller externa spårningssystem.

Du kan välja något av följande sidattribut som ska användas i dataelementet:

* URL
* Värdnamn
* Bannamn
* Protokoll
* Referent
* Titel

### Frågesträngsparameter

Ange en enda URL-parameter i fältet [!UICONTROL URL Parameter].

Endast namnavsnittet är nödvändigt och alla specialdesigners som &quot;?&quot; eller &quot;=&quot; ska utelämnas

#### Exempel:

`contentType`

### Slumpmässigt tal

Använd det här dataelementet för att generera ett slumpmässigt tal. Det används ofta för att ta prov på data eller skapa ID:n, till exempel ett träff-ID. Det slumpmässiga talet kan också användas för att dölja eller salta känsliga data. Exempel:

* Generera ett träff-ID
* Sammanfoga numret till en användartoken eller tidsstämpel för att säkerställa unikhet
* Gör en enkelriktad hash av PII-data
* Bestäm slumpmässigt när en undersökningsförfrågan ska visas på webbplatsen

Ange minimi- och maximivärden för det slumpmässiga talet.

**Standardvärden:**

Minst: 0

Maximum: 100000000

### Sessionslagring

Ange namnet på sessionslagringsobjektet i fältet [!UICONTROL Session Storage Item Name].

Sessionslagring liknar lokal lagring, förutom att data tas bort efter att sessionen har avslutats, medan lokala lager eller en cookie kan behålla data.

### Beteende för besökare

På liknande sätt som Sidinformation använder det här dataelementet vanliga beteendetyper för att utöka logiken i regler eller andra Experience Platform-lösningar.

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
* Om det här är startsidan för besöket fyller du i ett [!DNL Analytics]-mått
* Visa ett nytt erbjudande till besökaren efter X antal sessioner
* Visa ett nyhetsbrev om detta är en förstagångsbesökare

## Inbyggda dataelement

Du måste skapa ytterligare anpassade dataelement om du tidigare har använt något av följande dataelement:

* URI
* Protokoll
* Värdnamn
