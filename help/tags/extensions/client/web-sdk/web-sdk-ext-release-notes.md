---
title: Versionsinformation om Adobe Experience Platform Web SDK Extension
description: Adobe Experience Platform Web SDK Tag Extension
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 54c609ec995ac8e48c1c6441390b205bfb5a01cc
workflow-type: tm+mt
source-wordcount: '2812'
ht-degree: 1%

---


# Versionsinformation om SDK-tillägg

Det här dokumentet innehåller versionsinformation för taggtillägget Adobe Experience Platform Web SDK. Den senaste versionsinformationen om SDK finns i [versionsinformationen för Experience Platform Web SDK](/help/web-sdk/release-notes.md).

## Version 2.31.1 - 31 juli 2025

- Korrigerade ett problem som förhindrade att anpassade byggen kördes.
- Innehåller [version 2.28.1](../../../../web-sdk/release-notes.md#2-28-1) av Adobe Experience Platform Web SDK.

## Version 2.31.0 - 24 juli 2025

**Nya funktioner**

- Innehåller [version 2.28.0](../../../../web-sdk/release-notes.md#2-28-0) av Adobe Experience Platform Web SDK.

**Korrigeringar och förbättringar**

- Ett problem där ett fel uppstår när en datastream-åsidosättning aktiveras via ett dataelement har åtgärdats.
- Ett problem har korrigerats där tomma `idSyncContainerId` åsidosättningar skulle orsaka ett fel.
- När mediedataelement matchas inkluderas nu händelseobjektet.

**Kända fel**

- Efter utgåvan av v2.31.0 identifierades ett problem med byggprocessen för [anpassade komponenter](/help/web-sdk/install/create-custom-build.md). Medan anpassade byggen fortsätter att fungera ingår alla komponenter för närvarande i bygget, vilket resulterar i ett paket i full storlek oavsett komponentval. En fix till detta problem håller på att utvecklas. Om du förlitar dig på anpassade komponenter för att minimera byggstorleken rekommenderar vi att du väntar på en framtida version.


## Version 2.30.1 - 27 maj 2025

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där uppdateringsvariabelvyn kraschade när en organisation inte hade någon standardsandlåda angiven.

## Version 2.30.0 - 21 maj 2025

**Nya funktioner**

- Du kan nu ange ett dataelement när du aktiverar cookies från tredje part.
- Töm knappar har lagts till i kodfält.
- Innehåller [version 2.27.0](../../../../web-sdk/release-notes.md#2-27-0) av Adobe Experience Platform Web SDK.

**Korrigeringar och förbättringar**

- Validering har lagts till för att förhindra inställning av `onBeforeLinkClickSend` när händelsegruppering är aktiverad.

## Version 2.29.1 - 8 maj 2025

**Korrigeringar och förbättringar**

- Korrigerade ett problem där inställningarna inte sparades när användaren omedelbart klickade på Spara efter redigering.

## Version 2.29.0 - 5 mars 2025

**Nya funktioner**

- Nu kan du skapa anpassade Web SDK-byggen och välja de komponenter du behöver från taggtilläggets användargränssnitt. Detta kan leda till mindre byggen genom att utesluta oanvända komponenter. Mer information finns i dokumentationen om att [skapa en anpassad SDK-version](web-sdk-extension-configuration.md#custom-build) för webben.
- Innehåller [version 2.26.0](../../../../web-sdk/release-notes.md#2-26-0) av Adobe Experience Platform Web SDK.

**Korrigeringar och förbättringar**

- En smidig hantering av saknade dataelement har lagts till i [uppdateringsvariabelåtgärderna](action-types.md#update-variable). Tidigare visades ett felmeddelande när en åtgärd för uppdateringsvariabel redigerades med ett dataelement som saknas. Nu kan du välja ett annat dataelement och alla inställningar för åtgärden för att uppdatera variabel fortfarande tillämpas. Dataelement kan saknas om de tas bort eller om en taggegenskap dupliceras.
- Stöd har lagts till för att öppna en ny flik med åtgärden [omdirigering med identitet](action-types.md#redirect-with-identity). När åtgärden används används nu attributet `target` för ankartaggen när webbläsaren omdirigeras.
- Ett problem har korrigerats där Adobe Audience Manager inte kunde inaktiveras vid åsidosättning av konfiguration.

## Version 2.28.0 - 23 januari 2025

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där åsidosättningar av ID Sync Container inte kunde anges utan att Audience Manager aktiverades.
- Ett problem har korrigerats där åsidosättningar av datastream-konfiguration inaktiverades vid uppgradering till den senaste versionen.
- Ett problem har korrigerats där användare inte kunde spara inställningarna för automatisk klickning av mål.

**Nya funktioner**

- En ny funktion har lagts till för att växla mellan tekniska namn och visningsnamn i XDM-objektet.
- Innehåller [version 2.25.0](../../../../web-sdk/release-notes.md#2-25-0) av Adobe Experience Platform Web SDK.

## Version 2.27.0 - 31 oktober 2024

**Nya funktioner**

- [Datastream-åsidosättningar](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides) innehåller nu inställningar för att inaktivera Experience Cloud-lösningar och Adobe Experience Platform-tjänster.
- Du kan nu skapa [datastream-åsidosättningar](../web-sdk/web-sdk-extension-configuration.md) för mediesessioner.

Innehåller version 2.24.0 av Adobe Experience Platform Web SDK.

## Version 2.26.1 - 19 september 2024

**Korrigeringar och förbättringar**

- Korrigerade ett problem där cookies inte skrevs korrekt när Web SDK kördes lokalt.

Innehåller version 2.23.0 av Adobe Experience Platform Web SDK.

## Version 2.26.0 - 22 augusti 2024

**Nya funktioner**

- Övervakningspiken `triggered` har lagts till.
- [Guidade händelser](action-types.md#instance), [Begär standardanpassning](action-types.md#personalization), [Prenumerera regeluppsättningsobjekt](event-types.md#subscribe-ruleset-items) och [utvärdera regeluppsättningar](action-types.md#evaluate-rulesets) är nu allmänt tillgängliga.

**Korrigeringar och förbättringar**

- Korrigerade ett problem där duplicerade variabeldataelement kunde skriva över varandra.
- När du använder den guidade händelsen [Begär standardanpassning](action-types.md#personalization) aktiveras nu visuella personaliseringsbeslut automatiskt.

Innehåller version 2.2.0 av Adobe Experience Platform Web SDK.

## Version 2.25.0 - 18 juli 2024

**Nya funktioner**

- Stöd för automatisk spårning av personalisering i Adobe Journey Optimizer har lagts till.
- Nya inställningar för att hantera den förbättrade klicksamlingen introducerades.

Innehåller version 2.21.1 av Adobe Experience Platform Web SDK.

## Version 2.24.0 - 5 juni 2024

**Korrigeringar och förbättringar**

- Korrigerade ett fel som uppstod när tilläggskonfigurationen ändrades när config overrides definierades.
- Tillåt att tomma värden anges för ping-intervall för mediainsamling.
- Ett fel som uppstod när en åtgärd för uppdateringsvariabel ändrades har åtgärdats.
- Tillåt återställning av ID-synkroniseringsbehållaren i config overrides.

Innehåller version 2.20.0 av Adobe Experience Platform Web SDK.

## Version 2.23.1 - 28 maj 2024

**Nya funktioner**

- Stöd för komponenten [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) har lagts till i tilläggskonfigurationen.
- [`Send Media Event`](action-types.md#send-media-event)-åtgärden för funktionen [!DNL Streaming Media Collection] har lagts till.
- [`Media: Quality of Experience`](data-element-types.md#quality-experience)-dataelementet har lagts till för [!DNL Streaming Media Collection]-funktionen.

Innehåller version 2.20.0 av Adobe Experience Platform Web SDK.

**Korrigeringar och förbättringar**

- Ett fel som uppstod vid sökning efter dataelement i åtgärden [Uppdatera variabel](action-types.md#update-variable) har korrigerats.
- [!UICONTROL Media] händelsetyper har tagits bort från de händelsetyper som föreslås användas i åtgärden `sendEvent`.

## Version 2.2.0 - 3 maj 2024

**Nya funktioner**

- Utöka variabeldataelementet så att det stöder dataobjekt.
- Uppdateringsåtgärden för variabeln har nu stöd för att ändra genomströmningsdata för Adobe Analytics, Adobe Audience Manager och Adobe Target.

Innehåller version 2.19.2 av Adobe Experience Platform Web SDK.

## Version 2.21.4 - 10 januari 2024

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där sparande av konfigurationsåsidosättningar utan alla tre miljöerna skulle krascha tilläggets användargränssnitt.
- Ett problem har korrigerats där kryssrutan för att rensa det befintliga värdet inte fylldes i när en åtgärd för att uppdatera variabeln redigerades.

Innehåller version 2.19.2 av Adobe Experience Platform Web SDK.

## Version 2.21.3 – 10 november 2023

Innehåller version 2.19.1 av Adobe Experience Platform Web SDK.

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där den förslagsmatris som är tillgänglig i `Send event complete`-händelser alltid var tom.

## Version 2.21.2 - 1 november 2023

**Nya funktioner**

- `Request default personalization` alternativ för att skicka händelseåtgärd har lagts till.
- Stöd för sidhändelser över- och underkant har lagts till i åtgärden skicka händelse.
- `Apply propositions`-åtgärd har lagts till.
- `Evaluate rulesets`-åtgärd och `Subscribe ruleset items`-händelse har lagts till för meddelanden i appen.
- `Decision context` har lagts till för att skicka händelseåtgärd.

**Korrigeringar och förbättringar**

- Innehåller version 2.19.0 av Adobe Experience Platform Web SDK.

## Version 2.20.3-8 augusti 2023

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där dataelement inte kunde sparas i ID-synkroniseringsbehållar-ID:ts åsidosättningsfält.

## Version 2.20.1 - 3 augusti 2023

**Korrigeringar och förbättringar**

- Förbättrad validering av inställningar för åsidosättning av sparad datastam.

## Version 2.20.0 - 31 juli 2023

**Nya funktioner**

- Stöd har lagts till för [åsidosättningar av datastream-ID:t ](../../../../datastreams/overrides.md) per kommando.

**Korrigeringar och förbättringar**

- `edgeConfigId` har tagits bort till förmån för `datastreamId` i SDK-konfigurationen.
- Flera förbättringar av användarupplevelsen för datastream-konfigurationen åsidosätter användargränssnittet.

## Version 2.19.0 - 21 juni 2023

- Dataelementet **[!UICONTROL Variable]** och **[!UICONTROL Update Variable]**-åtgärderna är nu allmänt tillgängliga.

## Version 2.18.0 - 18 maj 2023

- Innehåller version 2.17.0 av Adobe Experience Platform Web SDK.

## Version 2.17.0 - 25 april 2023

**Nya funktioner**

- Innehåller version 2.16.0 av Adobe Experience Platform Web SDK.
- Stöd har lagts till för åsidosättande av [datastream-konfigurationen](/help/datastreams/overrides.md).
- Lägg till borttagningsmeddelande till alternativet `datasetId` i kommandot `sendEvent`.

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där databasbläddringen i Safari skulle stänga datastream-väljaren.

## Version 2.16.1 - 14 april 2023

- Korrigerade ett problem med XDM-objekt och variabeldataelement där du inte kunde välja ett schema från en icke-standardsandlåda.

## Version 2.16.0 - 30 mars 2023

**Nya funktioner**

- (Beta) **[!UICONTROL Update variable]**-åtgärden och **[!UICONTROL Variable]**-dataelementet har lagts till.
- Konfigurationen för callback-funktionen [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) har lagts till.

**Korrigeringar och förbättringar**

- Ett problem som orsakade att klickning på element i en ankartagg inte fungerade när åtgärden **[!UICONTROL Redirect with identity]** användes har åtgärdats.
- Korrigerade ett problem där XDM-objektdataelement inte fungerade när det bara fanns ett schema.
- Innehåller version 2.15.0 av Adobe Experience Platform Web SDK.

## Version 2.15.1 - 26 januari 2023

- Ett problem har korrigerats där användare utan åtkomst till datastreams inte kunde redigera tilläggskonfigurationen.
- Stöd för ytor har lagts till i åtgärden `sendEvent`.

Innehåller version 2.14.0 av Adobe Experience Platform Web SDK.

## Version 2.14.1 - 13 oktober 2022

- Ett problem har korrigerats där webb-SDK inte följer ID:t från Experience Cloud ID-tjänsten.

Innehåller version 2.13.1 av Adobe Experience Platform Web SDK Library.

## Version 2.14.0 - 28 september 2022

- En ny `targetMigrationEnabled`-konfiguration har lagts till som möjliggör fullständig sidmigrering.
- En tillämpad svarsåtgärd har lagts till för att aktivera hybridimplementeringar av server och klient.
- Ett kontextalternativ för användaragenttips har lagts till.

Innehåller version 2.13.0 av Adobe Experience Platform Web SDK Library.

## Version 2.13.0 - 29 juni 2022

- Sorteringsordningen för numeriska egenskaper i XDM-objektdataelementet, till exempel eVars, har korrigerats.

Innehåller version 2.12.0 av Adobe Experience Platform Web SDK Library.

## Version 2.12.0 - 13 juni 2022

- Dataelementet `identityMap` har uppdaterats för att fylla i namnområdesalternativen baserat på de sandlådor som definieras av tilläggsinställningarna.
- **[!UICONTROL Redirect with identity]**-åtgärd har lagts till för att tillåta delning av domänöverskridande identiteter.
- Lagt till dokumentationslänkar till åtgärden `sendEvent`.
- Uppgraderat bibliotek för React Spectrum.
- Flera förbättringar av användargränssnittet.

Innehåller version 2.11.0 av Adobe Experience Platform Web SDK Library.

## Version 2.11.2 - 3 maj 2022

Innehåller version 2.10.1 av Adobe Experience Platform Web SDK Library.

## Version 2.11.1 - 22 april 2022

- Korrigerat kommandofel för konfiguration från version 2.11.0.

Innehåller version 2.10.0 av Adobe Experience Platform Web SDK Library.

## Version 2.11.0 - 22 april 2022

- Förbättrade prestanda för tagggränssnitt.
- Lägg till sandlådeväljare i tilläggskonfigurationen för datastreams.

Innehåller version 2.10.0 av Adobe Experience Platform Web SDK Library.

## Version 2.10.0 - 10 mars 2022

- Uppdatera det fördolda kodutdrag som är tillgängligt för kopiering på konfigurationssidan så att det fungerar med den uppdaterade Adobe Target VEC-redigeraren.

Innehåller version 2.9.0 av Adobe Experience Platform Web SDK Library.

## Version 2.9.0 - 19 januari 2022

Innehåller version 2.8.0 av Adobe Experience Platform Web SDK Library.

## Version 2.8.0 - 26 oktober 2021

Innehåller version 2.7.0 av Adobe Experience Platform Web SDK Library.

- Ytterligare information från Edge Network finns i Send Event Complete-händelsen, inklusive `inferences` och `destinations`. Formatet på dessa egenskaper kan ändras eftersom dessa funktioner för närvarande lanseras som en del av en Beta.

## Version 2.7.3 - 7 september 2021

Innehåller version 2.6.4 av Adobe Experience Platform Web SDK Library.

- Det finns inte längre någon varning för borttagning av dubbletter för `container.buildInfo.environment.`

## Version 2.7.0 - 16 augusti 2021

Innehåller version 2.6.3 av Adobe Experience Platform Web SDK Library.

- När du använder dataelementtypen för identitetskarta tas nu identifierare vars ID:n matchar värden som inte är ifyllda strängar automatiskt bort från identitetskartan.
- Ett fel som uppstod när ett dataelement skulle sparas med datatypen XDM Object har korrigerats och inget schema har valts.
- Förbättrad typografi i användargränssnittet.

## Version 2.6.2 - 4 augusti 2021

Innehåller version 2.6.2 av Adobe Experience Platform Web SDK Library.

## Version 2.6.1 - 29 juli 2021

Innehåller version 2.6.1 av Adobe Experience Platform Web SDK Library.

## Version 2.6.0 - 27 juli 2021

Innehåller version 2.6.0 av Adobe Experience Platform Web SDK Library.

- Etiketter, beskrivningar och felmeddelanden som använder termen &quot;edge configuration&quot; har ändrats till att använda termen &quot;datastream&quot; för att passa in i den senaste Adobe Experience Platform-terminologin.
- I tilläggskonfigurationsvyn lades stöd till för hantering av ett stort antal datastreams- och datastream-miljöer.
- I XDM-objektets dataelementvy har stöd lagts till för att hantera ett stort antal scheman.
- En händelsetyp för Skicka händelse slutförd har lagts till, som kan användas för att köra en regel efter att en händelse har skickats till servern och ett svar har tagits emot. Mer dokumentation kommer snart.
- Händelsetypen för Mottagna beslut har tagits bort. Använd händelsetypen Send Event Complete i stället.
- Användargränssnittet och felhanteringen har förbättrats.

## Version 2.5.0 - 1 juni 2021

Innehåller version 2.5.0 av Adobe Experience Platform Web SDK Library.

- Ett `data`-fält har lagts till i åtgärden Skicka händelse. I kommande dokumentation beskrivs hur detta kan användas i vissa scenarier.
- I datavyn för XDM-objektet har ett problem korrigerats där ett fel uppstod om användaren hade åtkomst till Adobe Experience Platform-sandlådor men inte till den sandlåda som konfigurerats som standard för organisationen.
- I XDM-objektets dataelementvy har ett problem korrigerats där ett obligatoriskt schemafält skulle betraktas som ogiltigt även om det överordnade objektet inte innehöll några värden.

## Version 2.4.0 - 9 mars 2021

Innehåller version 2.4.0 av Adobe Experience Platform Web SDK Library.

- [&quot;Borttagning av dokument&quot;](/help/web-sdk/commands/sendevent/documentunloading.md) har lagts till i användargränssnittet för åtgärden Skicka händelse.
- Stöd för ett `out`-alternativ har lagts till när [standardmedgivande](/help/web-sdk/commands/configure/defaultconsent.md) konfigureras, vilket innebär att alla händelser utesluts tills medgivande tas (det befintliga `pending`-alternativet köar händelser och skickar dem när medgivande tas emot).
- Ett verktygstips har lagts till i standardfältet för samtycke.
- Stöd för Adobe Consent 2.0-standarden har lagts till när kommandot [`setConsent`](/help/web-sdk/commands/setconsent.md) används.
- Ett bättre fel visas nu i användargränssnittet för XDM-objektets dataelement om användarens åtkomsttoken är ogiltig eller felaktigt etablerad.
- Korsfel (som inte påverkar tilläggsprogrammets funktion) som visades på webbläsarens utvecklarkonsol när ett XDM-objektdataelement visades har åtgärdats.

## Version 2.3.0 - 4 november 2020

Innehåller version 2.3.0 av Adobe Experience Platform Web SDK Library.

- Stöd för att använda ett dataelement har lagts till när standardsamtycke konfigureras.
- Lagt till möjlighet att söka efter XDM-scheman med datatypen XDM Object.
- Kloning av XDM-data har lagts till i åtgärdstypen Skicka-händelse för att säkerställa att efterföljande ändringar av XDM-dataobjektet inte återspeglas i begäran.

## Version 2.2.0 - 1 oktober 2020

- När kunderna försökte skapa ett XDM-objekt från sandlådescheman, stötte de på autentiseringsproblem. API:t som anropar Experience Platform är nu medvetet om miljöer, så att användare bara får de scheman de har tillgång till för redigering.
- När du använder dataelementet `identityMap` är namnutrymmena nu förifyllda i en listruta så du behöver inte fylla i dessa manuellt.
- Gränssnittet för dataelementet `xdmObject` har gjorts om. I det nya användargränssnittet kan du se vilka fält som har fyllts i utan att behöva ange varje objekt i objektet.

## Version 2.1.1 - 26 augusti 2020

- Korrigerar ett problem där Adobe Experience Platform-sandlådor i XDM-objektvyn inte visas korrekt. Om en förväntad sandlåda inte visas i listan när du använder den här versionen av tillägget bör du kontakta Adobe Experience Platform-administratören för att kontrollera att åtkomstbehörigheterna är korrekt angivna.

## Version 2.1.0 - 5 augusti 2020

- Brytningsändring: Ta bort åtgärden `syncIdentity` och stöd för att skicka dessa ID:n i åtgärden `sendEvent` i stället. Inaktivera alla befintliga regler med den här åtgärden innan du uppgraderar tillägget.
- Uppdatera till allokering v. 2.1.0 ([Versionsinformation](/help/web-sdk/release-notes.md))
- Stöd för IAB 2.0-standard för samtycke i åtgärden `setConsent`.
- Stöd för åsidosättande av datauppsättnings-ID:t i åtgärden `sendEvent`.
- Lägg till ett nytt dataelement av typen `IdentityMap` som kan användas för att fylla i `identityMap`-posten i XDM-objektdataelementet som nu är aktiverat, och i åtgärden `setConsent`.
- Stöd för att skicka en identitetskarta i åtgärden `setConsent`.
- Stöd för att välja en Experience Platform-sandlåda i XDM-objektdataelementet.

## Version 1.0.0 - 26 maj 2020

- Stöd för att välja miljö från konfigurationstjänsten.

## Version 0.1.2 - 4 maj 2020

- `configId` har bytt namn till `edgeConfigId`.
- `viewStart` har bytt namn till `renderDecisions`, inställt på false som standard. Om värdet är true hämtas Personalization erbjudanden och återges automatiskt.
- Ändringar relaterade till `Get Decisions`:
   - Kommandot `getDecisions` har tagits bort.
   - Ett `scopes`-alternativ har lagts till i kommandot `sendEvent`. Besluten returneras i det `sendEvent` lösta löftet.
   - Ett inbyggt `__view__`-omfång har lagts till vilket resulterar i att erbjudanden för hela sidan/vyn returneras. (VEC erbjuder till exempel i Target.)
Dessa beslut returneras endast från kommandot `sendEvent` om `renderDecisions` är inställt på false.
   - En `Decisions Received`-händelse har lagts till som utlöses när beslut blir tillgängliga.
- Flera Personalization-aviseringar kombinerades under ett enda serversamtal.
- Ett problem i ID för händelsenammanfogning där det återställdes varje gång som dataelementet refererades till har korrigerats.
- Namnet på åtgärden `setCustomerIds` ändrades till `syncIdentity`.
- Ett `getIdentity`-kommando har lagts till. Detta kan endast användas med anpassad kod för tillfället.
- Om du aktiverar felsökning med `_satellite` aktiveras nu felsökning i Adobe Experience Platform Web SDK.
- Stöd för typvärden har lagts till i XDM-objektet: Booleans, siffror och decimaler.

## Version 0.0.10 - 16 mars 2020

- Kombinerade koncepten för anmälan och avanmälan under `Consent` och lade till ett nytt `setConsent`-kommando.
- Ett nytt dataelement av typen `XDM Object` har lagts till som tillåter mappning från JavaScript/JSON till XDM.

## Version 0.0.7 - 18 februari 2020

- IDSyncContainerId, datasetId, schemaId, urlDestinationsEnabled och cookieDestinationsEnabled har tagits bort
- Stöd för bindestreck i edgeDomain-alternativvärdet har lagts till
- Begäran som görs under ID-migrering skickas till demdex-slutpunkten för att förbättra identifieringen över domäner när ingen demdex-cookie har angetts
- Begäran som görs under ID-migrering förväntar alltid ett svar som ser till att identitets-cookie ställs in
- När ett ogiltigt kommando körs loggas en lista med giltiga kommandonamn i konsolen
- En kryssruta har lagts till för att växla stöd för cookies från tredje part till taggtillägget. Detta inaktiverar samtal till demdex.net

## Version 0.0.5 - 20 december 2019

- Lägg till konfigurationer för aktivitetsspåraren i taggtillägg
- Visa EventType och EventMergeId vid händelsekommando
- Lägg till taggtillägget onBeforeEventSend-konfiguration till
- Lägg till edgeBasePath-konfiguration i taggtillägg

## Version 0.0.3 - 25 november 2019

- Nya fält för sammanfognings-ID och typ i åtgärden Skicka händelse. Koppla ID mappar till `xdm.eventMergeID` i XDM-schemat och typen mappar till `xdm.eventType` i XDM-schemat.

## Version 0.0.2 - 18 november 2019

- Inledande version
