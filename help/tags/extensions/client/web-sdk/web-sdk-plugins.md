---
title: Översikt över tillägg för vanliga SDK-webbplugin-program
description: Läs mer om taggtillägget Common Web SDK Plugins i Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Översikt över tillägg för vanliga SDK-webbplugin-program

>[!IMPORTANT]
>
>Tillägget är avsett att användas med Adobe Experience Platform Web SDK-tillägget. Mer information om vilken version som ska användas med AppMeasurementet finns i översikten för tillägget [Common Analytics Plugins](../plugins/overview.md).

I det här dokumentet beskrivs hur du konfigurerar taggtillägget för Web SDK-plugin-program och använder det för att förstärka [Adobe Experience Platform Web SDK-tillägget](../web-sdk/overview.md).

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
* [&quot;pFo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getAndPersistValue` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). Dataelementet `getAndPersistValue` lagrar ett värde i en cookie som kan hämtas senare under ett besök.

Dataelementet `getAndPersistValue` innehåller följande argument:

* `vtp` (obligatoriskt): Det värde som ska behållas från sida till sida
* `cn` (valfritt): Namnet på den cookie som värdet ska lagras i. Om det här argumentet inte anges får cookien namnet `"s_gapv"`
* `ex` (valfritt): Antalet dagar innan cookien upphör att gälla. Om det här argumentet är `0` eller inte är inställt upphör cookien att gälla när besöket är slut (30 minuters inaktivitet).

Om variabeln i argumentet `vtp` är inställd anger dataelementet cookien och returnerar sedan cookie-värdet. Om variabeln i argumentet `vtp` inte är inställd returnerar dataelementet bara cookie-värdet.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Det här plugin-programmet kräver platsåtkomst på klienten men genererar inget undantag om det inte får det.

Gör att du kan konfigurera och konfigurera [`getGeoCoordinates` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). Dataelementet `getGeoCoordinates` fångar latitud och longitud för besökarenheter.

Dataelementet `getGeoCoordinates` använder inga argument. Det returnerar ett av följande värden:

* `"geo coordinates not available"`: För enheter som inte har geoplatsdata tillgängliga när plugin-programmet körs. Det här värdet är vanligt vid den första besöksträffen, särskilt när besökarna först måste ge sitt samtycke till att spåra sin plats.
* `"error retrieving geo coordinates"`: När plugin-programmet påträffar fel vid försök att hämta enhetens plats
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Där [LATITUDE]/[LONGITUDE] är latituden och longituden

### `getNewRepeat`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getNewRepeat` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). Dataelementet `getNewRepeat` avgör om en besökare på webbplatsen är en ny besökare eller en återkommande besökare inom ett önskat antal dagar.

Dataelementet `getNewRepeat` använder följande argument:

* `d` (heltal, valfritt): Det minsta antal dagar som krävs mellan besök som återställer besökarna till `"New"`. Om argumentet inte är inställt är det som standard 30 dagar.

Det här dataelementet returnerar värdet `"New"` om den cookie-fil som angetts av dataelementet inte finns eller har upphört att gälla. Värdet `"Repeat"` returneras om cookien som anges av dataelementet finns och tiden sedan den aktuella träffen och tiden som anges i cookien är längre än 30 minuter. Den här metoden returnerar samma värde för ett helt besök.

### `getPageName`

Gör att du kan konfigurera och konfigurera [`getPageName` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). Dataelementet `getPageName` skapar en lättläst, användarvänlig formaterad version av den aktuella URL:en.

Dataelementet `getPageName` använder följande argument:

* `si` (valfri sträng): Ett ID infogades i början av strängen som representerar platsens ID. Värdet kan antingen vara ett numeriskt ID eller ett eget namn. Om den inte anges används den aktuella domänen som standard.
* `qv` (valfri, sträng): En kommaavgränsad lista med frågesträngsparametrar som, om de hittas i URL:en, läggs till i strängen
* `hv` (valfri, sträng): En kommaavgränsad lista med parametrar i URL-hash som, om de hittas i URL:en, läggs till i strängen
* `de` (valfri sträng): Avgränsaren för att dela upp enskilda delar av strängen. Standardvärdet är en pipe (`|`).

Dataelementet returnerar en sträng som innehåller en användarformaterad version av URL:en. Den här strängen tilldelas vanligtvis variabeln `pageName`, men kan även användas i andra variabler.

### `getPreviousValue`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getPreviousValue` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). Dataelementet `getPreviousValue` ställer in en variabel på ett värde som angetts vid en tidigare träff.

Dataelementet `getPreviousValue` använder följande argument:

* `v` (sträng, krävs): Variabeln som har värdet som du vill skicka till nästa bildbegäran. En vanlig variabel som används är `s.pageName` för att hämta föregående sidvärde.
* `c` (sträng, valfritt): Namnet på den cookie som lagrar värdet.  Om det här argumentet inte anges är standardvärdet `"s_gpv"`.

När du anropar det här dataelementet returneras strängvärdet som finns i cookien. Plugin-programmet återställer sedan förfallotiden för cookie och tilldelar det variabelvärdet från argumentet `v`. Kakan går ut efter 30 minuters inaktivitet.

### `getQueryParam`

Gör att du kan konfigurera och konfigurera [`getQueryParam` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). Dataelementet `getQueryParam` extraherar värdet för alla frågesträngsparametrar som finns i en URL. Det är användbart för att extrahera kampanjkoder, både interna och externa, från URL:er för landningssidor. Det är också värdefullt när du extraherar söktermer eller andra frågesträngsparametrar. Det här dataelementet innehåller robusta funktioner för att analysera komplexa URL:er, inklusive hashvärden och URL:er som innehåller flera frågesträngsparametrar.

Dataelementet `getQueryParam` använder följande argument:

* `qsp` (obligatoriskt): En kommaavgränsad lista med frågesträngsparametrar som ska sökas efter i URL:en. Den är inte skiftlägeskänslig.
* `de` (valfritt): Den avgränsare som ska användas om flera frågesträngsparametrar matchar. Standardvärdet är en tom sträng.
* `url` (valfritt): En anpassad URL, sträng eller variabel som frågesträngsparametervärdena ska extraheras från. Standardvärdet är `window.location`.

Om du anropar det här dataelementet returneras ett värde beroende på argumenten ovan och URL:en:

* Om ingen matchande frågesträngsparameter hittas returnerar metoden en tom sträng.
* Om en matchande frågesträngsparameter påträffas returnerar metoden frågesträngsparameterns värde.
* Om en matchande frågesträngsparameter påträffas men värdet är tomt returnerar metoden `true`.
* Om flera matchande frågesträngsparametrar hittas returnerar metoden en sträng med varje parametervärde avgränsat med strängen i argumentet `de`.

### `getTimeParting`

Gör att du kan konfigurera och konfigurera [`getTimeParting` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). Dataelementet `getTimeParting` hämtar information om tiden när mätbara aktiviteter äger rum på din plats. Det här dataelementet är värdefullt när du vill dela upp mätvärden med en upprepningsbar uppdelning av tiden i ett visst datumintervall. Du kan till exempel jämföra konverteringsgraden mellan två olika veckodagar, till exempel alla söndagar jämfört med alla torsdagar. Du kan också jämföra tidsperioder på dagen, t.ex. alla tider jämfört med alla kvällar.

Dataelementet `getTimeParting` använder följande argument:

`t` (Valfritt men rekommenderat, sträng): Namnet på den tidszon som besökarens lokala tid ska konverteras till.  Standardvärdet är UTC/GMT-tid. En fullständig lista över giltiga värden finns i [List of TZ database time zone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) på Wikipedia.

Vanliga giltiga värden är:

* `"America/New_York"` för Eastern Time
* `"America/Chicago"` för centraltid
* `"America/Denver"` för bergstid
* `"America/Los_Angeles"` för Pacific Time

Anrop av det här dataelementet returnerar en sträng som innehåller följande avgränsade med ett pipe (`|`):

* Det aktuella året
* Den aktuella månaden
* Dag i månaden
* Veckodagen
* Aktuell tid (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getTimeSinceLastVisit` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). Dataelementet `getTimeSinceLastVisit` spårar hur lång tid det har tagit för en besökare att återvända till din webbplats efter det senaste besöket.

Dataelementet `getTimeSinceLastVisit` använder inga argument. Den returnerar den tid som gått sedan besökaren senast kom till webbplatsen och som är paketerad i följande format:

* Tid mellan 30 minuter och en timme sedan det senaste besöket är inställt på närmaste halvminuters test. Till exempel `"30.5 minutes"`, `"53 minutes"`
* Tiden mellan en timme och en dag avrundas till närmaste kvartalstimme. Till exempel `"2.25 hours"`, `"7.5 hours"`
* Tiden som är större än en dag avrundas till närmsta dagstidsinställning. Exempel: `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Om en besökare inte har besökt tidigare eller om den förflutna tiden är längre än två år, anges värdet till `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Detta dataelement anger båda cookies och tillåter lagring av användargenererade värden i cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getValOnce` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). Dataelementet `getValOnce` förhindrar att en variabel ställs in som är lika med samma värde mer än en gång.

Dataelementet `getValOnce` använder följande argument:

* `vtc` (obligatoriskt, sträng): Variabeln som ska kontrolleras och om den precis har ställts in på ett identiskt värde tidigare
* `cn` (valfri sträng): Namnet på den cookie som innehåller värdet som ska kontrolleras. Standardvärdet är `"s_gvo"`
* `et` (valfritt, heltal): Utgången för cookien i dagar (eller minuter, beroende på argumentet `ep`). Standardvärdet är `0`, som går ut i slutet av webbläsarsessionen
* `ep` (valfri sträng): Ange bara det här argumentet om argumentet `et` också är inställt. Ange det här argumentet som `"m"` om du vill att argumentet `et` ska upphöra att gälla om några minuter i stället för dagar. Standardvärdet är `"d"`, vilket anger argumentet `et` i dagar.

Om argumentet `vtc` och cookie-värdet matchar returnerar metoden en tom sträng. Om argumentet `vtc` och cookie-värdet inte matchar returnerar metoden argumentet `vtc` som en sträng.

### `getVisitDuration`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getVisitDuration` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). Dataelementet `getVisitDuration` håller reda på hur lång tid i minuter som besökaren har varit på webbplatsen fram till den tidpunkten.

Dataelementet `getVisitDuration` använder inga argument. Det returnerar ett av följande värden:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (där `[x]` är antalet minuter som gått sedan besökaren landade på platsen)

### `getVisitNum`

>[!IMPORTANT]
>
>Detta dataelement ställer in cookies. Mer information finns i den specifika dokumentationen för plugin-programmet.

Gör att du kan konfigurera och konfigurera [`getVisitNum` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). Dataelementet `getVisitNum` returnerar besöksnumret för alla besökare som kommer till webbplatsen inom det önskade antalet dagar.

Dataelementet `getVisitNum` använder följande argument:

* `rp` (valfritt, heltal ELLER sträng): Antalet dagar innan besöksnummerräknaren återställs.  Standardvärdet är `365` när det inte anges.
   * När det här argumentet är `"w"` återställs räknaren i slutet av veckan (den här lördagen klockan 11:59)
   * När argumentet är `"m"` återställs räknaren i slutet av månaden (den sista dagen i den här månaden)
   * När det här argumentet är `"y"` återställs räknaren i slutet av året (31 december)
* `erp` (valfritt, booleskt): När argumentet `rp` är ett tal avgör det här argumentet om giltigheten för besöksnumret ska förlängas. Om värdet är `true` återställs besöksnummerräknaren vid efterföljande träffar på din webbplats. Om värdet är `false` utökas inte efterföljande träffar på din webbplats när besöksnummerräknaren återställs. Standardvärdet är `true`. Det här argumentet är inte giltigt när argumentet `rp` är en sträng.

Besöksnummerökningen när besökaren återvänder till er webbplats efter 30 minuters inaktivitet. Om den här metoden anropas returneras ett heltal som representerar besökarens aktuella besöksnummer.

### `p_fo` (Endast sidan först)

Gör att du kan konfigurera och konfigurera [`p_fo` Analytics-plugin ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). Dataelementet `p_fo` är ett verktyg som kontrollerar om det finns ett specifikt JavaScript-objekt. Om objektet inte finns skapar plugin-programmet objektet och returnerar `true`. Om JavaScript-objektet redan finns på sidan returneras `false`. Det här dataelementet är användbart om du vill köra kod exakt en gång på en sida.

Dataelementet `p_fo` använder följande argument:

* `on` (obligatoriskt, sträng): Namnet på det JavaScript-objekt som dataelementet skapar om objektet inte finns på sidan än.

Om objektet inte finns än returnerar metoden `true` och skapar objektet. Om objektet redan finns returnerar metoden `false`.
