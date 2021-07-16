---
title: Versionsinformation om Adobe Analytics Extension
description: Den senaste versionsinformationen om taggtillägget Adobe Analytics i Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 3%

---

# Versionsinformation om Adobe Analytics-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

## 6 augusti 2020

### Adobe Analytics Extension 1.8.5

#### Felkorrigeringar

* Det felaktiga cookie-namnet i inställningarna för AAM-modulen angavs när fältet lämnades tomt. Detta har nu rättats till.

#### Funktioner

* Uppdaterat [AppMeasurement till 2.2.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* Det lilla användargränssnittet ändras så att de extra inställningarna nu visas komprimerade i ett dragspel i stället för i en kryssruta.

## 2 juni 2020

### Adobe Analytics Extension 1.8.4

#### Felkorrigeringar

* Korrigerade ett fel där kundvagnens händelser (prodView, scAdd, scView osv.) inte visades i listrutan med händelser. Alla dessa bör nu kunna markeras i listrutan.

#### Funktioner

* Du kan nu inaktivera aktivitetskartan i tillägget utan att behöva använda anpassad kod. Aktivitetskartan läses in som en separat modul (ungefär som AAM) och du kan stänga av den om du vill.
* Rensade användargränssnittet genom att minimera hierarkivariabler och andra alternativ.
* Ett fält har lagts till för att ange inköps-ID:n från gränssnittet för tilläggskonfigurationen.

## 10 mars 2020

### Adobe Analytics Extension 1.8.3

#### Felkorrigeringar

* Korrigerade ett fel som påverkade regelkonfigurationen som skulle orsaka ett fel när du försökte ange variabler om du använde ett anpassat bibliotek och rapportsviterna inte var konfigurerade i Analytics.
* När du skapade en eVar fanns det ett fel som inte visade dig möjligheten att &quot;duplicera från&quot; ett uttryck eller vice versa. Detta har nu korrigerats för att spegla beteendet i tidigare versioner.

#### Funktioner

* Uppdaterat [AppMeasurement till 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## 2 mars 2020

### Adobe Analytics Extension 1.8.2

#### Felkorrigeringar

* Ett problem där felaktig syntax användes för numeriska händelser och serialiserad valuta har korrigerats

#### Funktioner

* Uppdaterat [AppMeasurement till 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
* DIL-biblioteket i modulen Audience Manager har uppdaterats till 9.4
* Ökade längden på indatafält i tillägget
* eVars och props i tilläggs- och åtgärdskonfigurationerna visar nu det egna namnet från Analytics
* En kryssruta har lagts till i avsnittet Cookies i tilläggskonfigurationen där du kan skriva säkra cookies
* Tre nya konfigurationer har lagts till i modulen Audience Manager. En inställning för aktivering av loggning, aktivering av URL-mål och aktivering av cookie-mål har lagts till

## 13 november 2019

### Adobe Analytics Extension 1.8.1

#### Felkorrigeringar

* Korrigerade ett fel där premiumartiklar och props inte kunde sparas.

## 1 november 2019

### Adobe Analytics Extension 1.8.0

#### Felkorrigeringar

* Korrigerade ett fel där ett litet antal kunder inte kunde se rapportalternativen i listrutan
* Korrigerade ett fel där vissa variabler inte ställdes in korrekt när ECID användes

#### Funktioner

* Sorterar variabler, avtryck och händelser numeriskt i tilläggsvyn
* Har gjort ändringar i backend-schemat för att stödja kontextdata i Magento

## 6 september 2019

### Adobe Analytics Extension 1.7.8

#### Felkorrigeringar

* Korrigerade ett fel där vissa användare inte såg alternativ för rapportsviten i listrutan
* Korrigerade ett fel där händelser inte utlöstes korrekt

## 5 september 2019

### Adobe Analytics Extension 1.7.7

#### Funktioner

* Uppdaterat AppMeasurement till 2.17
* Uppdaterad målgruppshanteringsmodul som stöder DIL 9.3
* Uppdaterade fältbredder som ger mer utrymme

#### Felkorrigeringar

* Ett fel för att ange anmälan/avanmälan har korrigerats
* Korrigerade ett fel där variabler inte angavs korrekt när ECID användes

## 18 juli 2019

### Adobe Analytics Extension 1.7.6

#### Funktioner

* Uppdaterat Adobe Analytics-tillägget med stöd för DIL 9.2 för Audience Manager

* Tillägget med stöd för [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0) har uppdaterats
* Följande kryssruta har tagits bort eftersom den inte längre stöds: &quot;Koppla inte målpubliceringen IFRAME till DOM- eller branddestinationerna&quot;

## 4 juni 2019

### Adobe Analytics Extension 1.7.5

#### Funktioner

* Uppdaterade Adobe Analytics-tillägget till [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=en#version-2.14.0) som innehåller en korrigering av ett känt clearVars-problem
* En Exchange-länk har lagts till i tillägget. Du når Exchange-listan genom att markera listrutan och välja &quot;tilläggsinformation&quot;

#### Felkorrigeringar

* Korrigerade ett fel i användargränssnittet som visade att fel var togs bort från en lista
* Korrigerade ett fel som krävde en SSL-spårningsserver när flera rapportsviter skulle läggas till. När du lägger till flera rapportsviter krävs en spårningsserver, men SSL-spårningsserverfältet är valfritt.

## 15 apr 2019

### Adobe Analytics Extension 1.7.4

#### Felkorrigeringar

* Återrullade tillägget efter att ett fel påträffades i appMeasurement 2.13.0. appMeasurement 2.13.0 orsakade ett fel som inte skickade ECID, så om du installerade 1.7.3 rekommenderar vi att du uppgraderar till 1.7.4 för att undvika det här problemet. Observera att clearVars fortsätter tills en uppdaterad version av appMeasurement släpps

## 12 apr 2019

### Adobe Analytics Extension 1.7.3

#### Felkorrigeringar

* Uppdaterade Adobe Analytics Extension to appMeasurement 2.13.0 som innehåller en korrigering av ett känt clearVars-problem.

## 21 mars 2019

### Adobe Analytics Extension 1.7.2

#### Funktioner

* Uppdaterade Adobe Analytics-tillägget till DIL 9.1.
* Uppdaterade Adobe Analytics-tillägget till appMeasurement 2.12.
* Uppgraderade Adobe Analytics tilläggsvy till React-Spectrum.
* När du konfigurerar dina rapportsviter på konfigurationssidan visas nu en listruta med alla rapportsviter i ditt företag, vilket gör det enklare för dig att välja rätt rapportserie.

## 7 mars 2019

### Adobe Analytics Extension 1.7.1

#### Felkorrigeringar

* Återställer tillägget till version 1.6 efter att ett fel påträffades i 1.7.

## 11 februari 2019

### Adobe Analytics Extension 1.6

#### Funktioner

* Uppdaterade Adobe Analytics-tillägget till DIL 9.0, som kommer att stödja deltagande.
* Adobe Analytics-tillägget för AppMeasurement 2.11 har uppdaterats med stöd för deltagande.

#### Felkorrigeringar

* Korrigerade en konflikt med Prototype JS. Analystillägget har nu stöd för standardbiblioteken prototype.js.

## 9 november 2018

### Adobe Analytics Extension 1.5.1

#### **Felkorrigeringar**

* Modul DIL har nedgraderats till 7.0 för att åtgärda ett problem som orsakade problem med analysfyrar som inte aktiverades

## 5 november 2018

### Adobe Analytics Extension 1.5

#### **Funktioner**

* Adobe Analytics-tillägget för stöd för DIL 8.0 i Audience Manager har uppdaterats
* Avdelade fältet Serialisera från värde i två, Event ID och Event Value. Detta åtgärdar problemet som tilldelade ett värde i stället för att serialisera en händelse
   * Observera: om du använder det aktuella fältet för att lägga till ett ID med hjälp av en sträng (t.ex. Event7=3:abc123) du måste uppdatera dina indata så att de återspeglar ID:t i fältet Händelse-ID

#### **Felkorrigeringar**

* Ett fel som inte gjorde att valutakoden fylldes i korrekt har korrigerats

## 11 oktober 2018

### Adobe Analytics Extension 1.4

#### **Funktioner**

* Spårningscookie-namnet migrerades till tilläggskonfigurationen.

#### **Felkorrigeringar**

* Korrigerade ett fel så att angivna variabler inte kraschar när inget trackerProperties-objekt är tillgängligt.

## 5 juni 2018

### Adobe Analytics Extension 1.3

#### **Funktioner**

* Uppdaterat Adobe Analytics-tillägg som stöd för AppMeasurement 2.9.
* En funktion för att göra spåraren globalt tillgänglig har lagts till i Adobe Analytics-tillägget, vilket gör att spåraren kan användas globalt under `windows.s`.

#### **Felkorrigeringar**

* Korrigerade ett fel som gjorde att listvyn återställdes vid återgång från detaljvyn
* Korrigerade några fel för att förbättra inläsningen av resurser i revideringsväljaren
* Korrigerade ett fel där flera regler skrev över s.events i Adobe Analytics-tillägget

## 20 mars 2018

### Adobe Analytics Extension 1.2

#### **Funktioner**

* Uppdaterar AppMeasurement.js till 2.8.0
* Lägger till stöd för vidarebefordran på serversidan

## 8 februari 2018

### Adobe Analytics Extension 1.1

#### **Funktioner**

* AppMeasurement har uppdaterats till version 2.6
* Den initierade Analytics-spåraren visas nu via en delad modul i Adobe Experience Platform-taggtillägget, så att andra tillägg kan innehålla kod som interagerar med den.

#### **Felkorrigeringar**

* Korrigerade ett fel i Adobe Analytics Extension som gjorde att &quot;Error, missing Report Suite ID in AppMeasurement initialization&quot; visades i webbläsarkonsolen.
