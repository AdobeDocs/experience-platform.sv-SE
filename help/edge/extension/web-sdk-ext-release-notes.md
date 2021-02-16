---
title: Adobe Experience Platform Web SDK-tillägg
seo-title: Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
description: Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
seo-description: Adobe Experience Platform Web SDK-tillägg i Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 56f0b3abd859a6b27f0117fb6ec4c312ca93ba5d
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Platform Web SDK

[Läs mer: Versionsinformation för Adobe Experience Platform Web SDK](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html)

## 4 november 2020

### Adobe Experience Platform Web SDK 2.3.0

Innehåller version 2.3.0 av Adobe Experience Platform Web SDK-biblioteket.

#### Funktioner

* Stöd för att använda ett dataelement har lagts till när standardsamtycke konfigureras.
* Lagt till möjlighet att söka efter XDM-scheman med datatypen XDM Object.
* Kloning av XDM-data har lagts till i åtgärdstypen Skicka-händelse för att säkerställa att efterföljande ändringar av XDM-dataobjektet inte återspeglas i begäran.

## 1 oktober 2020

### Adobe Experience Platform Web SDK 2.2.0

#### Felkorrigeringar

* När kunderna försökte skapa ett XDM-objekt från sandlådescheman, stötte de på autentiseringsproblem. API:t som anropar AEP är nu medvetet om miljöer, så användarna presenteras bara med de scheman som de har tillgång till för redigering.

#### Funktioner

* När du använder dataelementet `identityMap` är namnutrymmena nu förifyllda i en listruta så du behöver inte fylla i dessa manuellt.
* Gränssnittet för `xdmObject`-dataelementet har gjorts om. I det nya användargränssnittet kan du se vilka fält som har fyllts i utan att behöva ange varje objekt i objektet.


## 26 augusti 2020

### Adobe Experience Platform Web SDK 2.1.1

#### Funktioner

* Korrigerar ett problem där Adobe Experience Platform-sandlådor i XDM-objektvyn visas felaktigt. Om en förväntad sandlåda inte visas i listan när du använder den här versionen av tillägget bör du kontakta Adobe Experience Platform-administratören för att kontrollera att åtkomstbehörigheterna är korrekt angivna.


## 5 augusti 2020

### Adobe Experience Platform Web SDK 2.1.0

#### Funktioner

* Brytningsändring: Ta bort åtgärden `syncIdentity` och stöd för att skicka dessa ID:n i åtgärden `sendEvent` i stället. Inaktivera alla befintliga regler med den här åtgärden innan du uppgraderar tillägget.
* Uppdatera till allokera v. 2.1.0 ([Versionsinformation](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html))
* Stöd för IAB 2.0 Consent Standard i åtgärden `setConsent`.
* Stöd för åsidosättande av datauppsättnings-ID:t i `sendEvent`-åtgärden.
* Lägg till ett nytt dataelement av typen `IdentityMap` som kan användas för att fylla i `identityMap`-posten i XDM-objektdataelementet som nu är aktiverat och i `setConsent`-åtgärden.
* Stöd för att skicka en identitetskarta i `setConsent`-åtgärden.
* Stöd för att välja en AEP-sandlåda i XDM-objektdataelementet.


## 26 maj 2020

### Adobe Experience Platform Web SDK 1.0.0

#### Funktioner

* Stöd för att välja miljö från konfigurationstjänsten.


## 4 maj 2020

### Adobe Experience Platform Web SDK 0.1.2

#### Funktioner

* Namnet på `configId` har ändrats till `edgeConfigId`.
* Namnet på `viewStart` har ändrats till `renderDecisions`, inställt på false som standard. Om värdet är true hämtas erbjudanden om personalisering och återges automatiskt.
* Ändringar som rör `Get Decisions`:
   * Kommandot `getDecisions` har tagits bort.
   * Ett `scopes`-alternativ har lagts till i kommandot `sendEvent`. Besluten returneras i det lösta löftet `sendEvent`.
   * Ett inbyggt `__view__`-omfång har lagts till som ger möjlighet att returnera erbjudanden för hela sidan/vyn. (VEC erbjuder till exempel i Target.)
Dessa beslut returneras endast från kommandot `sendEvent` om `renderDecisions` är inställt på false.
   * En `Decisions Received`-händelse som utlöses när beslut blir tillgängliga har lagts till.
* Flera personaliseringsaviseringar kombinerades under ett enda serversamtal.
* Ett problem i ID för händelsenammanfogning där det återställdes varje gång som dataelementet refererades till har korrigerats.
* Namnet på åtgärden `setCustomerIds` ändrades till `syncIdentity`.
* Ett `getIdentity`-kommando har lagts till. Detta kan endast användas med anpassad kod för tillfället.
* Om du aktiverar felsökning med `_satellite` aktiveras nu felsökning i AEP Web SDK.
* Stöd för typvärden i XDM-objektet har lagts till: Booleaner, siffror och decimaler.

## 16 mars 2020

### Adobe Experience Platform Web SDK 0.0.10

#### Funktioner

* Kombinerade koncepten för anmälan och avanmälan under `Consent` och lade till ett nytt `setConsent`-kommando.
* Ett nytt dataelement av typen `XDM Object` som tillåter mappning från JavaScript/JSON till XDM har lagts till.

## 18 februari 2020

### Adobe Experience Platform Web SDK 0.0.7

#### Funktioner

* Alternativen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled och cookieDestinationsEnabled har tagits bort
* Stöd för bindestreck i edgeDomain-alternativvärdet har lagts till
* Begäran som görs under ID-migrering skickas till demdex-slutpunkten för att förbättra identifieringen över domäner när ingen demdex-cookie har angetts
* Begäran som görs under ID-migrering förväntar alltid ett svar som ser till att identitets-cookie ställs in
* När ett ogiltigt kommando körs loggas en lista med giltiga kommandonamn i konsolen
* En kryssruta har lagts till för att växla stöd för cookies från tredje part till Adobe Experience Platform Launch-tillägget. Detta inaktiverar anrop till demdex.net

## 20 december 2019

### Adobe Experience Platform Web SDK 0.0.5

#### Funktioner

* Lägg till konfigurationer för aktivitetsspåraren i plattformens starttillägg
* Visa EventType och EventMergeId vid händelsekommando
* Add onBeforeEventSend config to Platform Launch Extension
* Lägg till edgeBasePath-konfiguration i plattformens starttillägg

#### Uppdatera till Alloy v. 0.0.10 som innehåller följande ändringar:

* Implementera klientlagring: Tillstånd och cookies-logik har flyttats till servern
* Visa EventType och EventMergeId vid händelsekommando
* Använd sendBeacon för annan länkspårning än slutlänkar
* Synkronisering av återställnings-ID minus kontroll av förfallodatum
* kommandot setCustomerIds kan inte hash-koda ID:n på sidor som inte är SSL (http)
* Skicka APEX-domänen till servern som ska användas när tillstånd/cookies anges
* Hämta ECID från svaret med en ny referenstyp
* Ta bort standardvärden för konfigurationer för aktivering och identitet
* Ändra namn på + flytta frågealternativ till metadata
* Äldre ECID-migrering

#### Felkorrigeringar

* Vid oväntad statuskod tolkar och formaterar du svarstexten för felmeddelande
* Körning av felsökningskommando eller användning av alloy_debug skrivs över av konfigurationen

## 25 november 2019

### Adobe Experience Platform Web SDK 0.0.3

#### Funktioner

* Nya fält för sammanfognings-ID och typ i åtgärden Skicka händelse. Sammanfognings-ID mappar till `xdm.eventMergeID` i XDM-schemat och Type mappar till `xdm.eventType` i XDM-schemat.
* Förbättrad felhantering och rapportering
* Använder nu `sendBeacon` för alla länkar

#### Felkorrigeringar

* Ett problem har korrigerats där växlingen av felsökning via en frågesträngsparameter eller kommandot `debug` inte skulle finnas kvar under sessionen.

## 18 november 2019

### Adobe Experience Platform Web SDK 0.0.2

#### Funktioner

* Tillägget har blinkat
* ECID-stöd utan ytterligare bibliotek eller nätverksanrop
* Stöd för deltagande
* Stöd för att skicka XDM till AEP
* Stöd för förstahandsdomäner
* Samla in webbläsarkontext automatiskt
* Helt öppen källkod ([tillägg](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy))
* Detaljerad loggning
* Möjlighet att dölja produktionsfel
