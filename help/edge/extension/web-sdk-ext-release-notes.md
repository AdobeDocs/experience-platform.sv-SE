---
title: Versionsinformation om Adobe Experience Platform Web SDK Extension
description: Adobe Experience Platform Web SDK Tag Extension
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Versionsinformation om Adobe Experience Platform Web SDK-tillägg

Det här dokumentet innehåller versionsinformation för taggtillägget Adobe Experience Platform Web SDK. Information om den senaste versionen av SDK finns i [Versionsinformationen för Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Version 2.6.0 - 27 juli 2021

* Etiketter, beskrivningar och felmeddelanden som använder termen &quot;edge configuration&quot; har ändrats till att använda termen &quot;datastream&quot; för att passa in i den senaste Adobe Experience Platform-terminologin.
* I tilläggskonfigurationsvyn lades stöd till för hantering av ett stort antal datastreams- och datastream-miljöer.
* I XDM-objektets dataelementvy har stöd lagts till för att hantera ett stort antal scheman.
* En händelsetyp för Skicka händelse slutförd har lagts till, som kan användas för att köra en regel efter att en händelse har skickats till servern och ett svar har tagits emot. Mer dokumentation kommer snart.
* Händelsetypen för Mottagna beslut har tagits bort. Använd händelsetypen Send Event Complete i stället.
* Användargränssnittet och felhanteringen har i allmänhet förbättrats.

## Version 2.5.0 - 1 juni 2021

Innehåller version 2.5.0 av Adobe Experience Platform Web SDK-biblioteket.

* Ett `data`-fält har lagts till i åtgärden Skicka händelse. I kommande dokumentation beskrivs hur detta kan användas i vissa scenarier.
* I datavyn för XDM-objektet har ett problem korrigerats där ett fel uppstod om användaren hade åtkomst till Adobe Experience Platform-sandlådor men inte till den sandlåda som konfigurerats som standard för organisationen.
* I XDM-objektets dataelementvy har ett problem korrigerats där ett obligatoriskt schemafält skulle betraktas som ogiltigt även om det överordnade objektet inte innehöll några värden.

## Version 2.4.0 - 9 mars 2021

Innehåller version 2.4.0 av Adobe Experience Platform Web SDK-biblioteket.

* [&quot;dokument tas bort&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)-kryssrutan har lagts till i gränssnittet för åtgärden Skicka händelse.
* Stöd för ett `out`-alternativ har lagts till när [standardmedgivande](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) konfigureras, vilket släpper alla händelser tills medgivande tas (det befintliga `pending`-alternativet köar händelser och skickar dem när medgivande tas emot).
* Ett verktygstips har lagts till i standardfältet för samtycke.
* Stöd för [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard) har lagts till.
* Ett bättre fel visas nu i användargränssnittet för XDM-objektets dataelement om användarens åtkomsttoken är ogiltig eller felaktigt etablerad.
* Korsfel (som inte påverkar tilläggsprogrammets funktion) som visades på webbläsarens utvecklarkonsol när ett XDM-objektdataelement visades har åtgärdats.

## Version 2.3.0 - 4 november 2020

Innehåller version 2.3.0 av Adobe Experience Platform Web SDK-biblioteket.

* Stöd för att använda ett dataelement har lagts till när standardsamtycke konfigureras.
* Lagt till möjlighet att söka efter XDM-scheman med datatypen XDM Object.
* Kloning av XDM-data har lagts till i åtgärdstypen Skicka-händelse för att säkerställa att efterföljande ändringar av XDM-dataobjektet inte återspeglas i begäran.

## Version 2.2.0 - 1 oktober 2020

* När kunderna försökte skapa ett XDM-objekt från sandlådescheman, stötte de på autentiseringsproblem. API:t som anropar Platform är nu medvetet om miljöer, så användarna presenteras bara med de scheman de har tillgång till för redigering.
* När du använder dataelementet `identityMap` är namnutrymmena nu förifyllda i en listruta så du behöver inte fylla i dessa manuellt.
* Gränssnittet för `xdmObject`-dataelementet har gjorts om. I det nya användargränssnittet kan du se vilka fält som har fyllts i utan att behöva ange varje objekt i objektet.

## Version 2.1.1 - 26 augusti 2020

* Korrigerar ett problem där Adobe Experience Platform-sandlådor i XDM-objektvyn visas felaktigt. Om en förväntad sandlåda inte visas i listan när du använder den här versionen av tillägget bör du kontakta Adobe Experience Platform-administratören för att kontrollera att åtkomstbehörigheterna är korrekt angivna.

## Version 2.1.0 - 5 augusti 2020

* Brytningsändring: Ta bort åtgärden `syncIdentity` och stöd för att skicka dessa ID:n i åtgärden `sendEvent` i stället. Inaktivera alla befintliga regler med den här åtgärden innan du uppgraderar tillägget.
* Uppdatera till allokera v. 2.1.0 ([Versionsinformation](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Stöd för IAB 2.0 Consent Standard i åtgärden `setConsent`.
* Stöd för åsidosättande av datauppsättnings-ID:t i `sendEvent`-åtgärden.
* Lägg till ett nytt dataelement av typen `IdentityMap` som kan användas för att fylla i `identityMap`-posten i XDM-objektdataelementet som nu är aktiverat och i `setConsent`-åtgärden.
* Stöd för att skicka en identitetskarta i `setConsent`-åtgärden.
* Stöd för att välja en plattformssandlåda i XDM-objektdataelementet.

## Version 1.0.0 - 26 maj 2020

* Stöd för att välja miljö från konfigurationstjänsten.

## Version 0.1.2 - 4 maj 2020

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
* Om du aktiverar felsökning med `_satellite` aktiveras nu felsökning i Adobe Experience Platform Web SDK.
* Stöd för typvärden i XDM-objektet har lagts till: Booleaner, siffror och decimaler.

## Version 0.0.10 - 16 mars 2020

* Kombinerade koncepten för anmälan och avanmälan under `Consent` och lade till ett nytt `setConsent`-kommando.
* Ett nytt dataelement av typen `XDM Object` som tillåter mappning från JavaScript/JSON till XDM har lagts till.

## Version 0.0.7 - 18 februari 2020

* Alternativen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled och cookieDestinationsEnabled har tagits bort
* Stöd för bindestreck i edgeDomain-alternativvärdet har lagts till
* Begäran som görs under ID-migrering skickas till demdex-slutpunkten för att förbättra identifieringen över domäner när ingen demdex-cookie har angetts
* Begäran som görs under ID-migrering förväntar alltid ett svar som ser till att identitets-cookie ställs in
* När ett ogiltigt kommando körs loggas en lista med giltiga kommandonamn i konsolen
* En kryssruta har lagts till för att växla stöd för cookies från tredje part till taggtillägget. Detta inaktiverar anrop till demdex.net

## Version 0.0.5 - 20 december 2019

* Lägg till konfigurationer för aktivitetsspåraren i taggtillägg
* Visa EventType och EventMergeId vid händelsekommando
* Lägg till taggtillägget onBeforeEventSend-konfiguration till
* Lägg till edgeBasePath-konfiguration i taggtillägg

## Version 0.0.3 - 25 november 2019

* Nya fält för sammanfognings-ID och typ i åtgärden Skicka händelse. Sammanfognings-ID mappar till `xdm.eventMergeID` i XDM-schemat och Type mappar till `xdm.eventType` i XDM-schemat.

## Version 0.0.2 - 18 november 2019

* Inledande version
