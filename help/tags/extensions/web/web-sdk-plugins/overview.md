---
title: Översikt över tillägg för vanliga SDK-webbplugin-program
description: Läs mer om taggtillägget Common Web SDK Plugins i Adobe Experience Platform.
source-git-commit: 4edc811f6306cd66f0ebef0a21896624f6c5e181
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Översikt över tillägg för vanliga SDK-webbplugin-program

>[!IMPORTANT]
>
>Tillägget är avsett att användas med Adobe Experience Platform Web SDK-tillägget. Mer information om vilken version som ska användas med AppMeasurement finns i översikten på sidan [Tillägget Common Analytics Plugins](../plugins/overview.md).

I det här dokumentet beskrivs hur du konfigurerar taggtillägget för Web SDK-plugin-program och använder det för att förstärka [Adobe Experience Platform Web SDK-tillägg](../sdk/overview.md).

## Konfigurera tillägget Common Web SDK Plugins

I det här avsnittet finns en referens för de alternativ som är tillgängliga när du konfigurerar tillägget för Web SDK-plugin-program.

>[!IMPORTANT]
>
>Tillägget Common Web SDK Plugins är avsett att förstärka Adobe Experience Platform Web SDK-tillägget, men du behöver inte ha det installerat för att tillägget ska fungera som förväntat.

## Lägga till plugin-program i Adobe Experience Platform Web SDK-tillägget

Ingen konfiguration krävs för att initiera eller lägga till ett plugin-program i biblioteket, förutom att använda följande inbyggda dataelement som finns i tillägget Common Web SDK-plugin-program:

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [`getPagename`](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [&quot;Fo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getAndPersistValue` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). The `getAndPersistValue` dataelement lagrar ett värde i en cookie som kan hämtas senare under ett besök.

The `getAndPersistValue` dataelementet innehåller följande argument:

* `vtp` (obligatoriskt): Värdet som ska behållas från sida till sida
* `cn` (valfritt): Namnet på den cookie som värdet ska lagras i. Om det här argumentet inte anges får cookien ett namn `"s_gapv"`
* `ex` (valfritt): Antalet dagar innan cookien förfaller. Om det här argumentet är `0` eller inte är inställd upphör cookien att gälla när besöket är slut (30 minuters inaktivitet).

Om variabeln i `vtp` -argumentet är inställt, anger dataelementet cookien och returnerar sedan cookie-värdet. Om variabeln i `vtp` -argumentet har inte angetts, returnerar dataelementet bara cookie-värdet.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Det här plugin-programmet kräver platsåtkomst på klienten men genererar inget undantag om det inte får det.

Gör att du kan konfigurera och konfigurera [`getGeoCoordinates` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). The `getGeoCoordinates` dataelementet fångar latituden och longituden för besökarnas enheter.

The `getGeoCoordinates` dataelementet använder inga argument. Det returnerar ett av följande värden:

* `"geo coordinates not available"`: För enheter som inte har geoplatsdata tillgängliga när plugin-programmet körs. Det här värdet är vanligt vid den första besöksträffen, särskilt när besökarna först måste ge sitt samtycke till att spåra sin plats.
* `"error retrieving geo coordinates"`: När plugin-programmet påträffar fel vid försök att hämta enhetens plats
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Plats [LATITUDE]/[LONGITUD] är latitud och longitud,

### `getNewRepeat`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getNewRepeat` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). The `getNewRepeat` dataelementet avgör om en besökare på platsen är en ny besökare eller en återkommande besökare inom ett önskat antal dagar.

The `getNewRepeat` dataelementet använder följande argument:

* `d` (heltal, valfritt): Minsta antal dagar mellan besöken som återställer besökarna till `"New"`. Om argumentet inte är inställt är det som standard 30 dagar.

Detta dataelement returnerar värdet för `"New"` om den cookie som anges av dataelementet inte finns eller har gått ut. Returnerar värdet för `"Repeat"` om den cookie som anges av dataelementet finns och tiden sedan den aktuella träffen och tiden som anges i cookien är längre än 30 minuter. Den här metoden returnerar samma värde för ett helt besök.

### `getPageName`

Gör att du kan konfigurera och konfigurera [`getPageName` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). The `getPageName` dataelement skapar en lättläst, användarvänlig formaterad version av den aktuella URL:en.

The `getPageName` dataelementet använder följande argument:

* `si` (valfri, sträng): Ett ID infogat i början av strängen som representerar platsens ID. Värdet kan antingen vara ett numeriskt ID eller ett eget namn. Om den inte anges används den aktuella domänen som standard.
* `qv` (valfri, sträng): En kommaavgränsad lista med frågesträngsparametrar som, om de finns i URL:en, läggs till i strängen
* `hv` (valfri, sträng): En kommaavgränsad lista med parametrar i URL-hash som, om de hittas i URL:en, läggs till i strängen
* `de` (valfri, sträng): Avgränsaren för att dela upp enskilda delar av strängen. Standardvärdet är ett rör (`|`).

Dataelementet returnerar en sträng som innehåller en användarformaterad version av URL:en. Strängen tilldelas vanligtvis till `pageName` men kan även användas i andra variabler.

### `getPreviousValue`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getPreviousValue` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). The `getPreviousValue` dataelementet ställer in en variabel på ett värde som ställs in vid en tidigare träff.

The `getPreviousValue` dataelementet använder följande argument:

* `v` (sträng, obligatoriskt): Variabeln som har värdet som du vill skicka till nästa bildförfrågan. En vanlig variabel som används är `s.pageName` för att hämta föregående sidvärde.
* `c` (sträng, valfritt): Namnet på den cookie som lagrar värdet.  Om det här argumentet inte anges används standardvärdet `"s_gpv"`.

När du anropar det här dataelementet returneras strängvärdet som finns i cookien. Plugin-programmet återställer sedan förfallotiden för cookie och tilldelar det variabelvärdet från `v` argument. Kakan går ut efter 30 minuters inaktivitet.

### `getQueryParam`

Gör att du kan konfigurera och konfigurera [`getQueryParam` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). The `getQueryParam` dataelement extraherar värdet för alla frågesträngsparametrar som finns i en URL. Det är användbart för att extrahera kampanjkoder, både interna och externa, från URL:er för landningssidor. Det är också värdefullt när du extraherar söktermer eller andra frågesträngsparametrar. Det här dataelementet innehåller robusta funktioner för att analysera komplexa URL:er, inklusive hashvärden och URL:er som innehåller flera frågesträngsparametrar.

The `getQueryParam` dataelementet använder följande argument:

* `qsp` (obligatoriskt): En kommaavgränsad lista med frågesträngsparametrar att söka efter i URL:en. Den är inte skiftlägeskänslig.
* `de` (valfritt): Den avgränsare som ska användas om flera frågesträngsparametrar matchar. Standardvärdet är en tom sträng.
* `url` (valfritt): En anpassad URL, sträng eller variabel som frågesträngens parametervärden ska extraheras från. Standardvärdet är `window.location`.

Om du anropar det här dataelementet returneras ett värde beroende på argumenten ovan och URL:en:

* Om ingen matchande frågesträngsparameter hittas returnerar metoden en tom sträng.
* Om en matchande frågesträngsparameter påträffas returnerar metoden frågesträngsparameterns värde.
* Om en matchande frågesträngsparameter påträffas men värdet är tomt, returnerar metoden `true`.
* Om flera matchande frågesträngsparametrar hittas returnerar metoden en sträng med varje parametervärde avgränsat med strängen i `de` argument.

### `getTimeParting`

Gör att du kan konfigurera och konfigurera [`getTimeParting` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). The `getTimeParting` dataelementet innehåller information om den tid då en mätbar aktivitet äger rum på din plats. Det här dataelementet är värdefullt när du vill dela upp mätvärden med en upprepningsbar uppdelning av tiden i ett visst datumintervall. Du kan till exempel jämföra konverteringsgraden mellan två olika veckodagar, till exempel alla söndagar jämfört med alla torsdagar. Du kan också jämföra tidsperioder på dagen, t.ex. alla tider jämfört med alla kvällar.

The `getTimeParting` dataelementet använder följande argument:

`t` (Valfritt men rekommenderas, sträng): Namnet på den tidszon som besökarens lokala tid ska konverteras till.  Standardvärdet är UTC/GMT-tid. Se [Lista över TZ-databasens tidszoner](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) på Wikipedia för en fullständig lista över giltiga värden.

Vanliga giltiga värden är:

* `"America/New_York"` för Eastern Time
* `"America/Chicago"` för centraltid
* `"America/Denver"` för Mountain Time
* `"America/Los_Angeles"` för Pacific Time

Anrop av det här dataelementet returnerar en sträng som innehåller följande avgränsade med ett rör (`|`):

* Det aktuella året
* Den aktuella månaden
* Dag i månaden
* Veckodagen
* Aktuell tid (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getTimeSinceLastVisit` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). The `getTimeSinceLastVisit` dataelementet spårar hur lång tid det har tagit för en besökare att återvända till din webbplats efter deras senaste besök.

The `getTimeSinceLastVisit` dataelementet använder inga argument. Den returnerar den tid som gått sedan besökaren senast kom till webbplatsen och som är paketerad i följande format:

* Tid mellan 30 minuter och en timme sedan det senaste besöket är inställt på närmaste halvminuters test. Exempel, `"30.5 minutes"`, `"53 minutes"`
* Tiden mellan en timme och en dag avrundas till närmaste kvartalstimme. Exempel, `"2.25 hours"`, `"7.5 hours"`
* Tiden som är större än en dag avrundas till närmsta dagstidsinställning. Exempel, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Om en besökare inte har besökt tidigare eller om den förflutna tiden är längre än två år, anges värdet till `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getValOnce` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). The `getValOnce` dataelement förhindrar att en variabel ställs in som lika med samma värde mer än en gång.

The `getValOnce` dataelementet använder följande argument:

* `vtc` (required, string): Variabeln som ska kontrolleras och se om den precis har ställts in på ett identiskt värde
* `cn` (valfri, sträng): Namnet på den cookie som innehåller värdet som ska kontrolleras. Standardvärdet är `"s_gvo"`
* `et` (valfritt, heltal): Cookie-filens utgångsdatum i dagar (eller minuter) beroende på `ep` argument). Standardvärdet är `0`som upphör i slutet av webbläsarsessionen
* `ep` (valfri, sträng): Ange bara det här argumentet om `et` -argumentet ställs också in. Ange det här argumentet som `"m"` om du vill ha `et` argument om att förfalla om några minuter i stället för dagar. Standardvärdet är `"d"`, som ställer in `et` argument i dagar.

Om `vtc` argument och cookie-värdesmatchning returnerar den här metoden en tom sträng. Om `vtc` argument och cookie-värde matchar inte, metoden returnerar `vtc` argument som en sträng.

### `getVisitDuration`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getVisitDuration` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). The `getVisitDuration` dataelementet spårar den tid i minuter som besökaren har varit på webbplatsen fram till den tidpunkten.

The `getVisitDuration` dataelementet använder inga argument. Det returnerar ett av följande värden:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (där `[x]` är antalet minuter som gått sedan besökaren landade på platsen)

### `getVisitNum`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getVisitNum` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). The `getVisitNum` dataelementet returnerar besöksnumret för alla besökare som kommer till webbplatsen inom det önskade antalet dagar.

The `getVisitNum` dataelementet använder följande argument:

* `rp` (valfritt, heltal ELLER sträng): Antalet dagar innan besöksnummerräknaren återställs.  Standardvärdet är `365` när den inte är inställd.
   * När det här argumentet är `"w"`, återställs räknaren i slutet av veckan (lördagen klockan 11:59)
   * När det här argumentet är `"m"`, återställs räknaren i slutet av månaden (den sista dagen i den här månaden)
   * När det här argumentet är `"y"`, vid årets slut (31 december)
* `erp` (valfritt, boolesk): När `rp` argument är ett tal, det här argumentet avgör om giltigheten för besöksnumret ska förlängas. Om inställt på `true`återställer efterföljande träffar på webbplatsen besöksnummerräknaren. Om inställt på `false`fortsätter inte efterföljande träffar på din webbplats när besöksräknaren återställs. Standardvärdet är `true`. Detta argument är inte giltigt om `rp` argument är en sträng.

Besöksnummerökningen när besökaren återvänder till er webbplats efter 30 minuters inaktivitet. Om den här metoden anropas returneras ett heltal som representerar besökarens aktuella besöksnummer.

### `p_fo` (Endast sida först)

Gör att du kan konfigurera och konfigurera [`p_fo` Analytics-plugin](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). The `p_fo` dataelement är ett verktyg som kontrollerar om det finns ett specifikt JavaScript-objekt. Om objektet inte finns skapar plugin-programmet objektet och returnerar `true`. Om JavaScript-objektet redan finns på sidan returneras det `false`. Det här dataelementet är användbart om du vill köra kod exakt en gång på en sida.

The `p_fo` dataelementet använder följande argument:

* `on` (required, string): Namnet på det JavaScript-objekt som dataelementet skapar om objektet inte finns på sidan än.

Om objektet inte finns än returnerar metoden `true` och skapar objektet. Om objektet redan finns returnerar metoden `false`.
