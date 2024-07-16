---
title: Versionsinformation för huvudtillägget
description: Den senaste versionsinformationen om Core-tillägget i Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 0%

---

# Versionsinformation om Core Extension

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

## 29 mars 2023

v3.4.1

* Lägger till nya inbyggda delegathändelser för webben:
   * Tangent
   * KeyUp
* Lägger till möjligheten att testa mot många värden (&quot;Lägg till ett annat&quot;-alternativ) mot följande delegater:
   * Händelser
      * Ändra
   * Villkor
      * Cookie
      * Landningssida
      * Frågesträngsparameter
      * Traffic Source
      * Variabel
* Ändrar delegaten events/EntersViewport så att den använder API:t [Intersection Observer](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) i stället för att manuellt identifiera element som kommer in i visningsrutan.
* Tar bort kod som migrerade DTM-cookies till LocalStorage.
* Loggar en varning till konsolen när API:erna LocalStorage och SessionStorage inte är tillgängliga.

## 4 januari 2022

v3.3.0

* Ändrar åtgärden [Utlös direktanrop](./overview.md#direct-call-action) så att du kan ange anpassad händelseinformation som ska skickas till direktanropsregler.

## 8 oktober 2021

v3.2.2

* Åtgärda JSON-schemat för villkorsstyrda värdedataelement för alla tillgängliga operatorer.
* Korrigera https://github.com/adobe/reactor-extension-core/issues/64.

## 23 september 2021

v3.2.1

* Korrigerade ett fel där initieringen av vyn med villkorsstyrda dataelement inte fungerade korrekt när fältvärdena var 0.

## 23 september 2021

v3.2.0

Följande ändringar har införts i dataelementet Villkorsvärde:

* Lägg till en kryssruta för villkorliga värden och reservvärden som gör att användaren kan välja om odefinierade värden ska vara det returnerade värdet.
* Nummervärden visas som tal i inställningsobjektet.
* Villkorligt värde behövs inte längre så att det kan fungera på samma sätt som reservvärdet.

## 17 september 2021

v3.1.1

* Åtgärda ett JS-fel som hindrade vyn för datumintervallvillkor att läsas in.

## 16 september 2021

v3.1.0

Nya dataelement lades till:

* Sammanfogat objekt - Markera flera dataelement som ska ha ett objekt. Objekten sammanfogas i hög grad (rekursivt) för att skapa ett nytt objekt.
* Villkorsvärde - Returnera ett av två värden (conditionalValue eller fallbackValue) baserat på resultatet av jämförelsen.
* Runtime Environment - Returnera en av följande Launch-miljövariabler: miljöfas, bibliotekets build-datum, egenskapsnamn, egenskaps-ID, regelnamn, regel-ID, händelsetyp, händelseinformationens nyttolast, direktanropsidentifierare.
* JavaScript Tools - Wrapper för vanliga JavaScript-åtgärder: grundläggande strängredigering (ersätt, delsträng, regex-matchning, första och sista indexvärde, delning, segment), grundläggande arrayåtgärder (segment, join, pop, shift) och grundläggande universella åtgärder (segment, längd).
* Enhetsattribut - Returnera enhetsattribut som fönsterstorlek eller skärmstorlek.

## 11 augusti 2021

v3.0.0

* PDCL-6153: Lägger till stöd för att på ett tillförlitligt sätt hämta den fullständigt kvalificerade URL:en för cachelagrade anpassade kodåtgärder.

v3.0.0 av Core-tillägget är kopplat till ändringar i [v27.2.0 av turbinwebbmiljön](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0) som gör att användare kan läsa in sitt bibliotek bland många värdregioner som hanteras av Adobe om användarens företag stöder Premium CDN.

Den här uppgraderingen är valfri och bakåtkompatibel för användare utan Premium CDN, och obligatorisk för kunder som har Premium CDN aktiverat på företaget.

## 20 maj 2021

v2.0.7

* Korrigerar ett problem där musinteraktion på textinmatningar inte längre fungerade korrekt.
* Inaktuellt användningen av webbläsaren och operativsystemet.

## 4 maj 2021

v2.0.6

* Mindre uppdatering för att korrigera ikoner som förvrängs när skärmstorleken ändras.

## 11 mars 2021

v2.0.5

* Uppdaterad kod i körtidsutvärderingen för händelser och åtgärder som har ett fördröjningsalternativ, som nu har stöd för dataelementvärden som lagts till i version 2.0.4, för att tvinga strängar till tal på rätt sätt.

## 9 mars 2021

v2.0.4

* Data Element-stöd för olika fält har lagts till - Data Element-stöd har lagts till i följande händelser: Time on Page, Enters Viewport, Hover och Media Time Play. Dessutom följande villkor: &#39;Time on Site&#39; och &#39;Value Comparison&#39;
* Lägger till stöd för standardbeteendet för Ctrl/Cmd + klick och mittersta musklickning när Länka fördröjning används
* **Markerad länkfördröjning för klickhändelsen som &quot;stöds inte längre&quot;.** - mer information finns i [bloggen för datainsamling](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) för Adobe Experience Platform

## 6 januari 2021

v1.9.0

* **Ny åtgärd,&quot;Utlös direktanrop&quot;** - Core-tillägget innehåller nu en ny åtgärdstyp med namnet `Trigger Direct Call`.  Detta kan användas när du vill aktivera en regel för direktsamtal via en åtgärd från en annan regel. Den mappas direkt till metoden `_satellite.track()`. Tusen tack till Jan Exner för detta bidrag.

## 8 december 2020

v1.8.4

* Korrigerade ett fel där en användare inte kunde rensa eller ta bort CSP på en gång.

## 28 juli 2020

v1.8.3

* Korrigerade ett fel där CSP nonce var skrivskyddat en gång när tillägget startades, i stället för att hämtas på nytt när en anpassad kodåtgärd anropas.

## 13 juli 2020

v1.8.2

* Korrigerade ett fel där den anpassade kodåtgärden genererade ett fel för HTML-kod som innehåller tokens utan taggnamn (t.ex. kommentarer).

## 10 juli 2020

v1.8.1

* Korrigerade ett fel där anpassade HTML-entiteter i attribut för `script`- och `style`-taggar inte avkodades korrekt innan de skrevs till sidan.&quot;
* Korrigerade ett fel där ett fel inträffar när en extern anpassad kodsåtgärd inte har något innehåll. Extern anpassad kodsåtgärd är den åtgärd som läses in från en annan fil än biblioteket (detta inträffar när händelsen som utlöser regeln inte är libraryLoaded eller pageBottom)

## 6 juli 2020

v1.8.0

* **Löften i anpassad kod** - Anpassade kodvillkor och JavaScript-åtgärder som inte körs i det globala omfånget kan nu returnera löften.  Du kan använda dem om du vill att efterföljande villkor och åtgärder ska vänta på att en asynkron process i din anpassade kod slutförs innan du går vidare till nästa objekt.
* **Återanrop i anpassade kodåtgärder för HTML** - Du kan göra samma sak i anpassade kodåtgärder för HTML med hjälp av återanropen `onCustomCodeSuccess()` och `onCustomCodeFailure()`.

Mer information finns i [Core Extension reference](./overview.md) i Conditions > Custom Code and Actions > Custom Code.

## 7 april 2020

v1.7.3

* **Längden på textfält ökar** - Textinmatningsfält ändrades till en flex-layout för att bättre utnyttja användarens skärmbredd och ge mer utrymme för längre textsträngar.

## 1 november 2019

v1.7.0

* **Åtkomst till `event` Variabel inom Element för anpassade koddata** - Du kan nu referera till händelsen inifrån ett anpassat kodelement när den körs i kontexten för en regel. Objektet innehåller användbar information om händelsen som utlöste regeln. Stewart Schilling för detta bidrag.

## 7 oktober 2019

v1.6.2

* **Ny typ av konstantdataelement** - Core-tillägget innehåller nu en ny dataelementtyp med namnet `Constant`.  Detta kan användas när du behöver lagra ett konstant värde som ska refereras till i olika villkor, åtgärder eller anpassad kod. Tusen tack till Jan Exner för detta bidrag.

## 11 september 2019

v1.6.1

* **Stöd för CSP Nonce** - Core-tillägget har nu en valfri konfigurationsparameter. Du kan lägga till ett dataelement som refererar till en gång. Om den är konfigurerad används det nonce som du har konfigurerat för alla infogade skript som läggs till på sidan. Den här ändringen stöder användningen av en skyddsprofil för innehåll med ett nonce, så att taggskript fortfarande kan läsas in i en CSP-miljö. Du kan läsa mer om att använda taggar med en CSP [här](../../../ui/client-side/content-security-policy.md).

## 18 juni 2019

v1.5.0

* **Loggning av direktanrop** - Webbläsarloggning för regler för direktanrop ger nu ytterligare information när det skickas.

## 8 maj 2019

v1.4.3

* **Indatafält** - Indatafälten är mycket längre nu!
* **Anpassad händelse** - Anpassad händelsetyp kan nu användas med händelser som skickas utanför fönstret.
* **Felkorrigering** - Ett fel har korrigerats där värdejämförelsevillkoret inte innehöll ett 0-värde.
* **Felkorrigering** - Exchange\_url-fältet har uppdaterats, så du kan nu se listan Core Extension i Adobe Exchange.

## 8 januari 2019

v1.4.2

* **Enters Viewport-händelse** - Tidigare utlöstes endast en gång per sida av Enters Viewport-händelsen. Det här beteendet kan nu konfigureras så att det aktiveras varje gång elementet kommer in i visningsrutan.
* **Egen händelsehändelse** - Anpassade händelser kan nu innehålla kontextuella data som kan användas i villkor och åtgärder.
* **Klickhändelse** - När du anger en länkfördröjning för klickhändelsen registreras den nu korrekt för underordnade för ankaret och inte bara för själva ankaret.

## 8 november 2018

* **alternativet Behåll kohort** - Alternativet att behålla en kohort har lagts till i samplingsvillkoret. Detta medför att en användare hålls kvar i eller utanför exempelkohorten mellan sessionerna. Om till exempel kryssrutan &quot;beständig kohort&quot; är markerad och villkoret returnerar true första gången det körs för en viss besökare, returneras true för alla efterföljande körningar av villkoret för samma besökare. Om kryssrutan &quot;beständig kohort&quot; är markerad och villkoret returnerar false första gången det körs för en viss besökare, returneras false för alla efterföljande körningar av villkoret för samma besökare.
* **Felkorrigering** - Ett problem har korrigerats där en regel som använder händelsen Sidslut och en anpassad kod på en sida där taggar lästes in synkront men inte installerades korrekt (inget anrop till `_satellite.pageBottom()`) skulle ta bort webbplatsinnehåll.
* **Felkorrigering** - Korrigerade ett fel där visningsrutan för partners inte skulle fungera om taggbiblioteket lästes in asynkront och sedan lästes in färdigt efter att webbläsarens DOMContentLoaded-händelse utlöstes.

## 24 maj 2018

* **Funktion** - Ett villkor för värdejämförelse har lagts till, vilket jämför två värden med någon av flera tillgängliga operatorer. Detta ersätter funktionaliteten för flera äldre förhållanden som var alldeles för specifika.
* **Funktion** - Ett villkor för maximal frekvens har lagts till. Det här villkoret gör att du kan ange hur många gånger villkoret ska returnera true inom en tidsperiod eller en händelseförekomst. Exempel: 5 gånger per dag, 2 gånger per besök.

## 11 april 2018

* **Funktion** - Dataelement kan nu referera till andra dataelement.

## 20 mars 2018

* **Felkorrigering** - Anpassade kodfönster genererade `document.write` fel och kördes inte i asynkrona distributioner
* **Felkorrigering** - Huvudmodulerna ingick inte i något bibliotek
* **Felkorrigering** - Det uppstod problem med min- och maxvärden för dataelementet Slumptal

## 10 januari 2018

* **Funktion** - slumpmässigt Number-dataelement
* **Funktion** - dataelement för sidinformation
* **Funktion** - datumvillkor
* **Funktion** - Provtagningsvillkor
