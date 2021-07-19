---
title: Versionsinformation för huvudtillägget
description: Den senaste versionsinformationen om Core-tillägget i Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 1%

---

# Versionsinformation om Core Extension

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

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

* Lagt till dataelementsstöd för olika fält - Data Element-stöd har lagts till i följande händelser: Time on Page, Enters Viewport, Hover och Media Time Play. samt följande villkor: Time on Site och Value Comparison
* Lägger till stöd för standardbeteendet för Ctrl/Cmd + klick och mittersta musklickning när Länka fördröjning används
* **Markerad länkfördröjning för klickhändelsen som&quot;stöds inte längre&quot;.** - mer information finns i  [Data Collection ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) Blogg for Adobe Experience Platform

## 6 januari 2021

v1.9.0

* **Ny åtgärd**  som&quot;utlöser direktanrop&quot; - Core-tillägget innehåller nu en ny åtgärdstyp som kallas  `Trigger Direct Call`.  Detta kan användas när du vill aktivera en regel för direktsamtal via en åtgärd från en annan regel. Det mappas direkt till metoden `_satellite.track()`. Tusen tack till [Jan Exner](https://twitter.com/jexner) för detta bidrag.

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

* Korrigerade ett fel där anpassade HTML-entiteter i attribut för `script` och `style`-taggar inte avkodades korrekt innan de skrevs till sidan.&quot;
* Korrigerade ett fel där ett fel inträffar när en extern anpassad kodsåtgärd saknar innehåll. Extern anpassad kodsåtgärd är den åtgärd som läses in från en annan fil än biblioteket (detta inträffar när händelsen som utlöser regeln inte är libraryLoaded eller pageBottom)

## 6 juli 2020

v1.8.0

* **Löften i Anpassad kod**  - Anpassade kodvillkor och JavaScript-åtgärder som inte körs i det globala omfånget kan nu returnera löften.  Du kan använda dem om du vill att efterföljande villkor och åtgärder ska vänta på att en asynkron process i din anpassade kod slutförs innan du går vidare till nästa objekt.
* **Återanrop i HTML-anpassade kodåtgärder**  - Du kan göra samma sak med HTML-anpassade kodåtgärder med hjälp av  `onCustomCodeSuccess()` och  `onCustomCodeFailure()` återanrop.

Mer information finns i [Core Extension reference](./overview.md) i Conditions > Custom Code and Actions > Custom Code.

## 7 april 2020

v1.7.3

* **Längden på textfält ökar**  - Textinmatningsfält ändrades till en flex layout för att bättre utnyttja användarens skärmbredd och ge mer utrymme för längre textsträngar.

## 1 november 2019

v1.7.0

* **Åtkomst till  `event` variabel i anpassat koddataelement**  - Nu kan du referera till händelsen inifrån ett anpassat kodelement när den körs i en regels kontext. Objektet innehåller användbar information om händelsen som utlöste regeln. Tusen tack till [Stewart Schilling](https://twitter.com/sdi_stewart) för detta bidrag.

## 7 oktober 2019

v1.6.2

* **Ny&quot;konstant&quot; dataelementtyp**  - Core-tillägget innehåller nu en ny dataelementtyp som kallas  `Constant`.  Detta kan användas när du behöver lagra ett konstant värde som ska refereras till i olika villkor, åtgärder eller anpassad kod. Tusen tack till [Jan Exner](https://twitter.com/jexner) för detta bidrag.

## 11 september 2019

v1.6.1

* **Stöd för CSP Nonce**  - Core-tillägget har nu en valfri konfigurationsparameter. Du kan lägga till ett dataelement som refererar till en gång. Om den är konfigurerad används det nonce som du har konfigurerat för alla infogade skript som läggs till på sidan. Den här ändringen stöder användning av en skyddsprofil för innehåll med en enda gång, så att skript för Platform launch fortfarande kan läsas in i en CSP-miljö.  Du kan läsa mer om att använda Platform launch med en CSP [här](../../../ui/client-side/content-security-policy.md).

## 18 juni 2019

v1.5.0

* **Loggning**  av direktanrop - Webbläsarloggning för regler för direktanrop ger nu ytterligare information när det skickas.

## 8 maj 2019

v1.4.3

* **Indatafält**  - Indatafält är mycket längre nu!
* **Anpassad händelse**  - Anpassad händelsetyp kan nu användas med händelser som skickas utanför fönstret.
* **Felkorrigering**  - Ett fel har korrigerats där värdejämförelsevillkoret inte skulle innehålla värdet 0.
* **Fältet Felkorrigering**  - exchange\_url har uppdaterats så du kan nu se listan Core Extension i Adobe Exchange.

## 8 januari 2019

v1.4.2

* **Enters Viewport-händelse**  - Tidigare utlöstes Enters Viewport-händelsen bara en gång per sida. Det här beteendet kan nu konfigureras så att det aktiveras varje gång elementet kommer in i visningsrutan.
* **Anpassad händelse**  - Anpassade händelser kan nu innehålla kontextdata som kan användas i villkor och åtgärder.
* **Klickhändelse**  - När du anger en länkfördröjning för klickhändelsen registreras den nu korrekt för underordnade för ankaret och inte bara för själva ankaret.

## 8 november 2018

* **Alternativet**  Behåll kohort - Alternativet att behålla en kohort har lagts till i samplingsvillkoret. Detta medför att en användare hålls kvar i eller utanför exempelkohorten mellan sessionerna. Om till exempel kryssrutan &quot;beständig kohort&quot; är markerad och villkoret returnerar true första gången det körs för en viss besökare, returneras true för alla efterföljande körningar av villkoret för samma besökare. Om kryssrutan &quot;beständig kohort&quot; är markerad och villkoret returnerar false första gången det körs för en viss besökare, returneras false för alla efterföljande körningar av villkoret för samma besökare.
* **Felkorrigering**  - Ett problem har korrigerats där en regel som använder händelsen Sidnederst och en anpassad kodåtgärd på en sida där taggar lästes in synkront men inte installerades korrekt (inget anrop till  `_satellite.pageBottom()`) rensade webbplatsinnehållet.
* **Felkorrigering**  - Ett problem har korrigerats där Enters Viewport inte skulle fungera om taggbiblioteket lästes in asynkront och sedan lästes in färdigt efter att webbläsarens DOMContentLoaded-händelse utlöstes.

## 24 maj 2018

* **Funktion**  - Ett villkor för värdejämförelse har lagts till, vilket jämför två värden med någon av flera tillgängliga operatorer. Detta ersätter funktionaliteten för flera äldre förhållanden som var alldeles för specifika.
* **Funktion**  - Tillagt ett Max frekvens-villkor. Det här villkoret gör att du kan ange hur många gånger villkoret ska returnera true inom en tidsperiod eller en händelseförekomst. Exempel: 5 gånger per dag, 2 gånger per besök.

## 11 apr 2018

* **Funktion**  - Dataelement kan nu referera till andra dataelement.

## 20 mars 2018

* **Felkorrigering**  - Anpassade kodfönster genererade  `document.write` fel och kördes inte i asynkrona distributioner
* **Felkorrigering**  - Huvudmodulerna ingick inte i något bibliotek
* **Felkorrigering**  - Det uppstod problem med min- och maxvärdena för dataelementet Slumptal

## 10 januari 2018

* **Funktion**  - Slumpmässigt Number Data Element
* **Funktion**  - Dataelement för sidinformation
* **Funktion**  - Datumvillkor
* **Funktion**  - Provtagningsvillkor
