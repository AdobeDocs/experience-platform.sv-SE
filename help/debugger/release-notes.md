---
title: Versionsinformation om Adobe Experience Platform Debugger
description: Den senaste versionsinformationen om Adobe Experience Platform Debugger.
keywords: felsökning;Experience Platform Debugger extension;chrome;extension;release notes
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: f2733cca00f98e85cd1b3944c5127f5c1c89594e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Versionsinformation om Adobe Experience Platform Debugger

## Version 1.4.0 - 24 augusti 2022

* Stöd för hybridimplementering av Web SDK har lagts till.
* Ett felmeddelande har lagts till när målspårning inte kan aktiveras.
* Uppdaterade beroenden.

## Version 1.3.3 - 20 juni 2022

* Korrigerat problem som förhindrade att popup-fönster öppnades från nätverkshändelsetabeller.
* Ett problem som hindrade inläsning av tilläggsinformation på sidan har korrigerats.

## Version 1.3.2 - 9 juni 2022

* En standardavatar lades till när användaren är inloggad.
* Syntaxmarkering har lagts till för JSON-objekt i loggar.

## Version 1.3.1 - 24 maj 2022

* Uppdaterade beroenden.
* Ett analysproblem har korrigerats där efterprocessträffar inte kunde aktiveras.
* Ett problem där felsökaren skulle kopplas till inloggningsfönstret i Adobe har korrigerats.
* Ett AT.js-problem där loggmeddelanden inte kunde visas i Felsökning har korrigerats.

## Version 1.3.0 - 28 januari 2022

* Länken Om har lagts till för att visa aktuell version och information.
* Tillagd växel för att visa efterbearbetade träffar för Analytics-begäranden. Växeln är tillgänglig i avsnittet Analytics (Analyser).
* Ett problem med fjärrfelsökningssession när sessionen stängdes utanför felsökaren har åtgärdats.
* Korrigerat felmeddelande som var synligt på fliken Web SDK Edge Transactions.
* Adobe-taggar på sidborttagningsvarning har åtgärdats när felsökaren använde _satellit-objektet.
* Korrigerade vissa fall där en AppMeasurement-instans inte hittades på sidan.
* Ett problem med sidanslutningen som uppstod när felsökningsfönstret öppnades för första gången har åtgärdats.

## Version 1.2.0 - 26 oktober 2021

* Visa händelser från alla webbläsarflikar i nätverksvyn. Om du bara vill visa händelser från den aktuella fliken väljer du låsikonen i felsökarens nedre högra hörn.
* Uppdaterad branding.

## Version 1.1.0 - 5 oktober 2021

* Visualisering av fjärrfelsökning - Ordna fjärrfelsökningshändelserna i ett visuellt flödesschema i Adobe Experience Platform Web SDK > Edge Transactions.
* Kräv att den IMS-organisation för Adobe Experience Platform Web SDK som används på sidan matchar den inloggade organisationen när en ny fjärrfelsökningssession startas.
* Visa endast kanttransaktioner för den anslutna fliken. Målspårningsloggar är fortfarande tillgängliga i avsnittet Loggar > Edge.
* Tillåt att olika ID-konfigurationer för dataström åsidosätts för varje instans av Adobe Experience Platform Web SDK på sidan. Växla till Lägg till felsökning aktiverat.
* Ett problem har korrigerats där Adobe Target trace-token inte alltid skickades med fjärrfelsökningssessioner för Adobe Experience Platform Web SDK.

## Version 1.0.0 5 maj 2021

* Första huvudversionen av felsökaren för Experience Platform. Avsedd att ersätta Experience Cloud Debugger.
