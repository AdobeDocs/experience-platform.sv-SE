---
title: Versionsinformation om Adobe Experience Platform Debugger
description: Den senaste versionsinformationen om Adobe Experience Platform Debugger.
keywords: debugger;experience Platform Debugger tillägg;chrome;tillägg;versionsinformation
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: c4048b83c916f4b3b4b5acb3cccb957b65ee25c8
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 91%

---

# Versionsinformation om Adobe Experience Platform Debugger

## Version 1.6.4 - 6 maj 2025

### Åtgärder och förbättringar

* Ett problem där inloggningen inte var tillgänglig har korrigerats.

## Version 1.6.3 - 30 april 2025

### Åtgärder och förbättringar

* Ett problem har korrigerats där felsökaren skulle förhindra DTM- och Tags-funktioner.
* Ett problem har korrigerats där Analytics Post-Procsed Hits inte skulle visas i loggarna.
* Ett problem har korrigerats där data på icke-ASCII-språk som japanska inte skulle visas korrekt i loggar.

## Version 1.6.2 - 1 oktober 2024

### Åtgärder och förbättringar

* Ett problem där felsökaren var för känslig för alla CSP-fel har korrigerats

## Version 1.6.1 – 25 juli 2024

### Åtgärder och förbättringar

* Ett problem har åtgärdats som gjorde att användare inte kunde lägga till nya inbäddningskoder för taggar på sidor utan dem.

## Version 1.6.0 – 11 juli 2024

### Nya funktioner

* Tillåt användare att välja att inte ta del av/ta del av teknisk och personlig datainsamling.

### Åtgärder och förbättringar

* Åtgärda Firefox skriptinjektion och länk till sekretesspolicy.
* Hämta saknade Analytics-förfrågningar.
* Åtgärda krascher på sidor med många komplexa konsolmeddelanden.
* Uppdatera Adobe Experience Platform Debugger till ett Manifest v3-tillägg.

## Version 1.5.4 – 19 december 2023

### Åtgärder och förbättringar

* Ett problem har åtgärdats där inställningar inte behölls.
* Ett problem har åtgärdats som orsakade att felsökaren kraschade när man visade efterbearbetade träffar i Analytics.

## Version 1.5.3 – 6 december 2023

### Nya funktioner

* Lade till ett lås på den aktiva fliken när inställningen Felsökning öppnades.

### Åtgärder och förbättringar

* Ett problem har åtgärdats där Analytics-förfrågningar saknades i privata domäner.
* Ett problem har åtgärdats där Activity Map-data saknades i tabellen för Analytics-förfrågningar.
* Ett problem har åtgärdats där visning av Target Trace skulle orsaka en krasch.
* En varning har lagts till när felsökaren inte kan konfigurera sidinfrastruktur i Firefox.

## Version 1.5.2 – 10 november 2023

(Endast Firefox)

### Åtgärder och förbättringar

* Filernas ordning har uppdaterats.

## Version 1.5.1 – 2 november 2023

### Åtgärder och förbättringar

* Ett problem har åtgärdats där Analytics-händelser skulle ignoreras eller dupliceras.
* Ett problem har åtgärdats där den maximala lagringsstorleken för tillstånd överskreds.
* Ett problem har åtgärdats där Edge Logs-sökningen inte kunde filtrera händelser.

## Version 1.5.0 – 19 oktober 2023

### Nya funktioner

* Visa länkar till egenskaper, miljö och regler i sammanfattning av taggar och loggar.

### Åtgärder och förbättringar

* Ett problem har åtgärdats där sammanfattad data för taggar inte skickades.
* Ett problem har åtgärdats där Assurance-sessioner gav ett CORS-fel
* Ett problem har åtgärdats som orsakade att Target Trace inte kunde visas.
* Åtgärdade knappen Skicka feedback.
* Åtgärdade att Datastream-ID saknades i Web SDK-sammanfattningen för version ≥2.18.0.
* Ett problem har åtgärdats där Edge-loggar inte var sökbara.
* En anteckning om ytterligare profiler för vissa kontotyper har lagts till.

## Version 1.4.1 – 1 november 2022

* Förbättrad prestanda på sidor med många Adobe Experience Platform Assurance-händelser.

## Version 1.4.0 – 3 oktober 2022

* Ytterligare stöd för AEP Assurance-felsökning för Web SDK-hybridimplementeringar.
* Stöd för flera flikar i samma AEP Assurance-session har lagts till.
* Ett problem har åtgärdats där användare inte kan växla profiler/organisationer efter inloggning.
   * För vissa konton krävs att du loggar ut och loggar in igen för att byta organisation.
* Ett felmeddelande läggs till när aktivering av Target Trace misslyckas.
* Uppdaterade beroenden.

## Version 1.3.3 – 20 juni 2022

* Ett problem har åtgärdats som förhindrade att popup-fönster öppnades från tabeller för nätverkshändelse.
* Ett problem har åtgärdats som hindrade inläsning av tilläggsinformation på sidan.

## Version 1.3.2 - 9 juni 2022

* En standardavatar lades till när användaren är inloggad.
* Syntaxmarkering har lagts till för JSON-objekt i loggar.

## Version 1.3.1 - 24 maj 2022

* Uppdaterade beroenden.
* Ett Analytics-problem har korrigerats där efterprocessträffar inte kunde aktiveras.
* Ett problem där felsökaren skulle kopplas till inloggningsfönstret i Adobe har korrigerats.
* Ett AT.js-problem där loggmeddelanden inte kunde visas i Felsökning har korrigerats.

## Version 1.3.0 - 28 januari 2022

* Länken Om har lagts till för att visa aktuell version och information.
* Växlingsknapp tillagd för att visa efterbearbetade träffar för Analytics-förfrågningar. Växlingsknappen är tillgänglig i avsnittet Analytics.
* Löste problemet med fjärrfelsökningssessionen när sessionen stängdes utanför felsökaren.
* Felmeddelande som var synligt på fliken Web SDK Edge Transactions har åtgärdats.
* Adobe Tags på sidborttagningsvarning har åtgärdats när felsökaren använde _satellit-objektet.
* Korrigerade vissa fall där det inte gick att hitta en AppMeasurement-instans på sidan.
* Ett problem med sidanslutningen som uppstod när felsökningsfönstret öppnades för första gången har åtgärdats.

## Version 1.2.0 - 26 oktober 2021

* Visa händelser från alla webbläsarflikar i nätverksvyn. Om du bara vill visa händelser från den aktuella fliken väljer du låsikonen i felsökarens nedre högra hörn.
* Uppdaterad anpassning.

## Version 1.1.0 - 5 oktober 2021

* Visualisering av felsökning på distans - Organisera felsökningshändelserna på distans i ett visuellt flödesschema i Adobe Experience Platform Web SDK > Edge Transactions-avsnittet.
* Kräv att den Adobe Experience Platform Web SDK-organisation som används på sidan matchar den inloggade organisationen när en ny fjärrfelsökningssession startas.
* Visa endast Edge-transaktioner för den anslutna fliken. Target Trace-loggar finns fortfarande i avsnittet Loggar > Edge.
* Tillåt att olika ID-konfigurationer för dataström åsidosätts för varje instans av Adobe Experience Platform Web SDK på sidan. Lägg till växlingsknapp för felsökning.
* Ett problem har korrigerats där Adobe Target Trace-token inte alltid skickades med fjärrfelsökningssessioner för Adobe Experience Platform Web SDK.

## Version 1.0.0 5 maj 2021

* Första huvudversionen av Experience Platform Debugger.  Avsedd att ersätta Experience Cloud Debugger.
