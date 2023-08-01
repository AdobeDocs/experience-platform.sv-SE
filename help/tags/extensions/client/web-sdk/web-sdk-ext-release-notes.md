---
title: Versionsinformation om Adobe Experience Platform Web SDK Extension
description: Adobe Experience Platform Web SDK Tag Extension
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 27bff79c38395e2c2366f9bd89101eb03fcd5608
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---


# Versionsinformation om Adobe Experience Platform Web SDK-tillägg

Det här dokumentet innehåller versionsinformation för taggtillägget Adobe Experience Platform Web SDK. Information om den senaste versionen av SDK:n finns i [Versionsinformation för Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Version 2.20.0 - 31 juli 2023

**Nya funktioner**

* Stöd för [åsidosättningar per kommando för datastream-ID](../../../../datastreams/overrides.md).

**Korrigeringar och förbättringar**

* Föråldrat `edgeConfigId` till förmån för `datastreamId` i SDK-konfigurationen.
* Flera förbättringar av användarupplevelsen för datastream-konfigurationen åsidosätter användargränssnittet.

## Version 2.19.0 - 21 juni 2023

* The **[!UICONTROL Variable]** dataelement och **[!UICONTROL Update Variable]** åtgärder är nu allmänt tillgängliga.

## Version 2.18.0 - 18 maj 2023

* Innehåller version 2.17.0 av Adobe Experience Platform Web SDK.

## Version 2.17.0 - 25 april 2023

**Nya funktioner**

* Innehåller version 2.16.0 av Adobe Experience Platform Web SDK.
* Stöd för [åsidosättningar av konfiguration av datastream](../../../../datastreams/overrides.md).
* Lägg till borttagningsmeddelande i `datasetId` på `sendEvent` -kommando.


**Korrigeringar och förbättringar**

* Ett problem har korrigerats där databasbläddringen i Safari skulle stänga datastream-väljaren.

## Version 2.16.1 - 14 april 2023

* Korrigerade ett problem med XDM-objekt och variabeldataelement där du inte kunde välja ett schema från en icke-standardsandlåda.

## Version 2.16.0 - 30 mars 2023

**Nya funktioner**

* (Beta) Tillagd **[!UICONTROL Update variable]** åtgärd och **[!UICONTROL Variable]** dataelement.
* Tillagd konfiguration för [`onBeforeLinkClickSend`](../../../../edge/fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) callback-funktion.

**Korrigeringar och förbättringar**

* Korrigerat ett problem som medförde att klickning på element i en ankartagg inte fungerade när **[!UICONTROL Redirect with identity]** åtgärden användes.
* Korrigerade ett problem där XDM-objektdataelement inte fungerade när det bara fanns ett schema.
* Innehåller version 2.15.0 av Adobe Experience Platform Web SDK.


## Version 2.15.1 - 26 januari 2023

* Ett problem har korrigerats där användare utan åtkomst till datastreams inte kunde redigera tilläggskonfigurationen.
* Stöd för ytor i `sendEvent` åtgärd.

Innehåller version 2.14.0 av Adobe Experience Platform Web SDK.


## Version 2.14.1 - 13 oktober 2022

* Ett problem har korrigerats där Web SDK inte följer ID:t från Experience Cloud ID-tjänsten.

Innehåller version 2.13.1 av Adobe Experience Platform Web SDK Library.

## Version 2.14.0 - 28 september 2022

* Lagt till ny `targetMigrationEnabled` konfiguration som möjliggör sidvis fullständig migrering.
* En tillämpad svarsåtgärd har lagts till för att aktivera hybridimplementeringar av server och klient.
* Ett kontextalternativ för användaragenttips har lagts till.

Innehåller version 2.13.0 av Adobe Experience Platform Web SDK Library.

## Version 2.13.0 - 29 juni 2022

* Sorteringsordningen för numeriska egenskaper i XDM-objektdataelementet, till exempel eVars, har korrigerats.

Innehåller version 2.12.0 av Adobe Experience Platform Web SDK Library.

## Version 2.12.0 - 13 juni 2022

* Uppdaterade `identityMap` dataelement för att fylla i namnutrymmesalternativ baserat på de sandlådor som definieras av tilläggsinställningarna.
* Tillagd **[!UICONTROL Redirect with identity]** åtgärd för att tillåta delning av domänöverskridande identiteter.
* Lagt till dokumentationslänkar till `sendEvent` åtgärd.
* Uppgraderat bibliotek för React Spectrum.
* Flera förbättringar av användargränssnittet.

Innehåller version 2.11.0 av Adobe Experience Platform Web SDK Library.

## Version 2.11.2 - 3 maj 2022

Innehåller version 2.10.1 av Adobe Experience Platform Web SDK Library.

## Version 2.11.1 - 22 april 2022

* Korrigerat kommandofel för konfiguration från version 2.11.0.

Innehåller version 2.10.0 av Adobe Experience Platform Web SDK Library.

## Version 2.11.0 - 22 april 2022

* Förbättrade prestanda för tagggränssnitt.
* Lägg till sandlådeväljare i tilläggskonfigurationen för datastreams.

Innehåller version 2.10.0 av Adobe Experience Platform Web SDK Library.

## Version 2.10.0 - 10 mars 2022

* Uppdatera det fördolda kodutdrag som är tillgängligt för kopiering på konfigurationssidan så att det fungerar med den uppdaterade Adobe Target VEC-redigeraren.

Innehåller version 2.9.0 av Adobe Experience Platform Web SDK Library.

## Version 2.9.0 - 19 januari 2022

Innehåller version 2.8.0 av Adobe Experience Platform Web SDK Library.

## Version 2.8.0 - 26 oktober 2021

Innehåller version 2.7.0 av Adobe Experience Platform Web SDK Library.

* Ytterligare information från Experience Edge finns i Send Event Complete-händelsen, inklusive `inferences` och `destinations`. Formatet på dessa egenskaper kan ändras eftersom dessa funktioner för närvarande lanseras som en del av en betaversion. Mer information finns i [Spåra händelser.](../../../../edge/fundamentals/tracking-events.md)

## Version 2.7.3 - 7 september 2021

Innehåller version 2.6.4 av Adobe Experience Platform Web SDK Library.

* Det finns inte längre någon varning för borttagning av dubbletter `container.buildInfo.environment.`

## Version 2.7.0 - 16 augusti 2021

Innehåller version 2.6.3 av Adobe Experience Platform Web SDK Library.

* När du använder dataelementtypen för identitetskarta tas nu identifierare vars ID:n matchar värden som inte är ifyllda strängar automatiskt bort från identitetskartan.
* Ett fel som uppstod när ett dataelement skulle sparas med datatypen XDM Object har korrigerats och inget schema har valts.
* Förbättrad typografi i användargränssnittet.

## Version 2.6.2 - 4 augusti 2021

Innehåller version 2.6.2 av Adobe Experience Platform Web SDK Library.

## Version 2.6.1 - 29 juli 2021

Innehåller version 2.6.1 av Adobe Experience Platform Web SDK Library.

## Version 2.6.0 - 27 juli 2021

Innehåller version 2.6.0 av Adobe Experience Platform Web SDK Library.

* Etiketter, beskrivningar och felmeddelanden som använder termen &quot;edge configuration&quot; har ändrats till att använda termen &quot;datastream&quot; för att passa in i den senaste Adobe Experience Platform-terminologin.
* I tilläggskonfigurationsvyn lades stöd till för hantering av ett stort antal datastreams- och datastream-miljöer.
* I XDM-objektets dataelementvy har stöd lagts till för att hantera ett stort antal scheman.
* En händelsetyp för Skicka händelse slutförd har lagts till, som kan användas för att köra en regel efter att en händelse har skickats till servern och ett svar har tagits emot. Mer dokumentation kommer snart.
* Händelsetypen för Mottagna beslut har tagits bort. Använd händelsetypen Send Event Complete i stället.
* Användargränssnittet och felhanteringen har förbättrats.

## Version 2.5.0 - 1 juni 2021

Innehåller version 2.5.0 av Adobe Experience Platform Web SDK Library.

* Lagt till en `data` till åtgärden Skicka händelse. I kommande dokumentation beskrivs hur detta kan användas i vissa scenarier.
* I datavyn för XDM-objektet har ett problem korrigerats där ett fel uppstod om användaren hade åtkomst till Adobe Experience Platform-sandlådor men inte till den sandlåda som konfigurerats som standard för organisationen.
* I XDM-objektets dataelementvy har ett problem korrigerats där ett obligatoriskt schemafält skulle betraktas som ogiltigt även om det överordnade objektet inte innehöll några värden.

## Version 2.4.0 - 9 mars 2021

Innehåller version 2.4.0 av Adobe Experience Platform Web SDK Library.

* Tillagd [&quot;dokument tas bort&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) kryssruta för att skicka händelseåtgärdsgränssnitt.
* Stöd för `out` alternativ när [konfigurera standardsamtycke](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) som släpper alla händelser tills samtycke tas emot (den befintliga `pending` Alternativet placerar händelser i kö och skickar dem när de har fått sitt samtycke).
* Ett verktygstips har lagts till i standardfältet för samtycke.
* Stöd för [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Ett bättre fel visas nu i användargränssnittet för XDM-objektets dataelement om användarens åtkomsttoken är ogiltig eller felaktigt etablerad.
* Korsfel (som inte påverkar tilläggsprogrammets funktion) som visades på webbläsarens utvecklarkonsol när ett XDM-objektdataelement visades har åtgärdats.

## Version 2.3.0 - 4 november 2020

Innehåller version 2.3.0 av Adobe Experience Platform Web SDK Library.

* Stöd för att använda ett dataelement har lagts till när standardsamtycke konfigureras.
* Lagt till möjlighet att söka efter XDM-scheman med datatypen XDM Object.
* Kloning av XDM-data har lagts till i åtgärdstypen Skicka-händelse för att säkerställa att efterföljande ändringar av XDM-dataobjektet inte återspeglas i begäran.

## Version 2.2.0 - 1 oktober 2020

* När kunderna försökte skapa ett XDM-objekt från sandlådescheman, stötte de på autentiseringsproblem. API:t som anropar Platform är nu medvetet om miljöer, så användarna presenteras bara med de scheman de har tillgång till för redigering.
* När du använder `identityMap` namnutrymmen är nu ifyllda i en listruta så du behöver inte fylla i dessa manuellt.
* Gränssnittet för `xdmObject` dataelement. I det nya användargränssnittet kan du se vilka fält som har fyllts i utan att behöva ange varje objekt i objektet.

## Version 2.1.1 - 26 augusti 2020

* Korrigerar ett problem där Adobe Experience Platform-sandlådor i XDM-objektvyn inte visas korrekt. Om en förväntad sandlåda inte visas i listan när du använder den här versionen av tillägget bör du kontakta Adobe Experience Platform-administratören för att kontrollera att åtkomstbehörigheterna är korrekt angivna.

## Version 2.1.0 - 5 augusti 2020

* Brytningsändring: Ta bort `syncIdentity` åtgärd och support som skickar dessa ID:n i `sendEvent` i stället. Inaktivera alla befintliga regler med den här åtgärden innan du uppgraderar tillägget.
* Uppdatera till allokering v. 2.1.0 ([Versionsinformation](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Stöd för IAB 2.0-standard för samtycke i `setConsent` åtgärd.
* Stöd för att åsidosätta datauppsättnings-ID i `sendEvent` åtgärd.
* Lägg till ett nytt dataelement av typen `IdentityMap` som kan användas för att fylla i `identityMap` i XDM-objektdataelementet som nu är aktiverat, och i `setConsent` åtgärd.
* Stöd för att skicka en identitetskarta i `setConsent` åtgärd.
* Stöd för att välja en plattformssandlåda i XDM-objektdataelementet.

## Version 1.0.0 - 26 maj 2020

* Stöd för att välja miljö från konfigurationstjänsten.

## Version 0.1.2 - 4 maj 2020

* Bytt namn `configId` till `edgeConfigId`.
* Bytt namn `viewStart` till `renderDecisions`, inställt på false som standard. Om värdet är true hämtas erbjudanden om personalisering och återges automatiskt.
* Ändringar relaterade till `Get Decisions`:
   * Borttagen `getDecisions` -kommando.
   * Lagt till en `scopes` till `sendEvent` -kommando. Besluten returneras i `sendEvent` löst löfte.
   * Lagt till en inbyggd `__view__` omfång som resulterar i att sidans/vyns breda erbjudanden returneras. (VEC erbjuder till exempel i Target.)
Dessa beslut kommer från `sendEvent` kommando endast om `renderDecisions` är inställt på false.
   * Lagt till en `Decisions Received` som utlöses när beslut blir tillgängliga.
* Flera personaliseringsaviseringar kombinerades under ett enda serversamtal.
* Ett problem i ID för händelsenammanfogning där det återställdes varje gång som dataelementet refererades till har korrigerats.
* Bytt namn på `setCustomerIds` åtgärd till `syncIdentity`.
* Lagt till en `getIdentity` -kommando. Detta kan endast användas med anpassad kod för tillfället.
* Aktivera felsökning med `_satellite` aktiverar nu felsökning i Adobe Experience Platform Web SDK.
* Stöd för typvärden har lagts till i XDM-objektet: Booleans, siffror och decimaler.

## Version 0.0.10 - 16 mars 2020

* Kombinerade koncepten för anmälan och avanmälan enligt `Consent`och lade till en ny `setConsent` -kommando.
* Ett nytt dataelement av typen har lagts till `XDM Object` som tillåter mappning från JavaScript/JSON till XDM.

## Version 0.0.7 - 18 februari 2020

* IDSyncContainerId, datasetId, schemaId, urlDestinationsEnabled och cookieDestinationsEnabled har tagits bort
* Stöd för bindestreck i edgeDomain-alternativvärdet har lagts till
* Begäran som görs under ID-migrering skickas till demdex-slutpunkten för att förbättra identifieringen över domäner när ingen demdex-cookie har angetts
* Begäran som görs under ID-migrering förväntar alltid ett svar som ser till att identitets-cookie ställs in
* När ett ogiltigt kommando körs loggas en lista med giltiga kommandonamn i konsolen
* En kryssruta har lagts till för att växla stöd för cookies från tredje part till taggtillägget. Detta inaktiverar samtal till demdex.net

## Version 0.0.5 - 20 december 2019

* Lägg till konfigurationer för aktivitetsspåraren i taggtillägg
* Visa EventType och EventMergeId vid händelsekommando
* Lägg till taggtillägget onBeforeEventSend-konfiguration till
* Lägg till edgeBasePath-konfiguration i taggtillägg

## Version 0.0.3 - 25 november 2019

* Nya fält för sammanfognings-ID och typ i åtgärden Skicka händelse. Koppla ID-mappningar till `xdm.eventMergeID` i XDM-schemat och Type-mappningar till `xdm.eventType` i XDM-schemat.

## Version 0.0.2 - 18 november 2019

* Inledande version
