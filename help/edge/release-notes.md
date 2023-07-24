---
title: Versionsinformation för Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen om webb-SDK för Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versionsinformation;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 1%

---


# Versionsinformation

Det här dokumentet innehåller versionsinformation för Adobe Experience Platform Web SDK.
Den senaste versionsinformationen om taggtillägget Web SDK finns i [Versionsinformation om tillägget för Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Version 2.16.0 - 17 maj 2023

**Korrigeringar och förbättringar**

* Web SDK kodar nu destinationsvärdena för cookie-filen i Audience Manager, ungefär som i [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en).

## Version 2.16.0 - 25 april 2023

**Nya funktioner**

* Stöd för [åsidosättningar av konfiguration av datastream](../datastreams/overrides.md).

## Version 2.15.0 - 30 mars 2023

**Nya funktioner**

* Stöd för [`onBeforeLinkClickSend`](fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) klicka på motringningen.
* Stöd för Adobe Journey Optimizer klickspårning har lagts till.

**Korrigeringar och förbättringar**

* Länksamlingen innehåller nu länknamn och besöksregion.
* Konsolfel för misslyckade URL-mål har tagits bort.

## Version 2.14.0 - 25 januari 2023

* (Beta) Stöd för Adobe Journey Optimizer-ytor och -erbjudanden har lagts till.

**Korrigeringar och förbättringar**

* Ett problem med anpassade kodåtgärder för Adobe Target VEC där koden infogades på en alternativ plats har korrigerats [!DNL at.js].
* Ett problem har korrigerats där refererhuvudet i vissa kantfall inte var korrekt inställt på begäranden till Edge-nätverket.
* Ett problem där [klienttips för användaragent](fundamentals/user-agent-client-hints.md) kan anges till en felaktig typ.
* Ett problem där `placeContext.localTime` matchade inte schemat.

## Version 2.13.1 - 13 oktober 2022

* Korrigerade ett problem där besökarmigrering inte fungerar om window.Visitor definieras efter konfiguration. Det här är ett särskilt problem när du använder Adobe-taggar.
* Ett problem där `device.screenWidth` och `device.screenHeight` har fyllts i som strängar i vissa miljöer.

## Version 2.13.0 - 28 september 2022

**Nya funktioner**

* Stöd för [Page by Page Full Migration](home.md#migrating-to-web-sdk). Adobe Target-profilen bevaras nu när en besökare förflyttar sig mellan at.js- och Web SDK-sidor.
* Utökat konfigurerbart stöd för [klienttips för hög entropi-användaragent](fundamentals/user-agent-client-hints.md#high-entropy).
* Stöd för nya `applyResponse` -kommando. Detta möjliggör hybridpersonalisering via [API för Edge Network Server](../server-api/overview.md).
* QA-lägeslänkar fungerar nu på flera sidor.

**Korrigeringar och förbättringar**

* Ett problem har korrigerats där personalisering av klickspårningsstatistik inte uppdaterades när länkspårning inaktiverades.
* Uppdaterade kommandon som genererar ett valideringsfel när okända alternativ anges.
* The `_experience.decisioning.propositionEventType` egenskapen fylls nu i när händelser för visnings- och interaktionspersonalisering skickas automatiskt.
* Dubblettvalidering av namnutrymme har lagts till för `getIdentity` -kommando.
* Dubblettvalidering av beslutsomfattning har lagts till för `sendEvent` -kommando.

## Version 2.12.0 - 29 juni 2022

* Ändra förfrågningarna till Edge Network för att använda `cluster` cookie-platstips som en del av URL:en. Detta garanterar att användare som byter plats (t.ex. genom ett VPN eller kör med mobila enheter, etc.) når samma kant och har samma personaliseringsprofil.
* Sträng konfigurerade funktioner i kommandosvaret getLibraryInfo.

## Version 2.11.0 - 13 juni 2022

**Nya funktioner**

* Ni kan nu leverera personaliserade upplevelser mer korrekt genom att dela besökar-ID:n mellan mobilappar och mobilwebbinnehåll samt mellan domäner. Se [dedikerad dokumentation](identity/id-sharing.md) om du vill veta mer.
* Nu kan du återge eller köra en array med förslag från [!DNL Adobe Target] till enkelsidiga applikationer, utan att öka analysmåtten. Detta minskar antalet rapporteringsfel och ökar noggrannheten i analysen. Se [dedikerad dokumentation](personalization/rendering-personalization-content.md#applypropositions) om du vill veta mer.
* Ytterligare information har lagts till i `getLibraryInfo` med tillgängliga kommandon och den slutliga konfigurationen för instansen.

**Korrigeringar och förbättringar**

* Uppdaterade cookie-inställningar för användning `sameSite="none"` och `secure` flagga på [!DNL HTTPS] sidor.
* Ett problem där anpassat innehåll inte tillämpades korrekt när `eq` pseudoväljare.
* Ett problem där `localTimezoneOffset` kan inte validera Experience Platform.

## Version 2.10.1 - 3 maj 2022

* Korrigerade ett problem där flera beständiga iframes skapades för ID-synkronisering och segmentmål.

## Version 2.10.0 - 22 april 2022

* Använd en beständig iframe för alla ID-synkroniseringar och segmentmål.
* Ett problem där sammanslagna mätvärden duplicerades i `sendEvent` resultat.

## Version 2.9.0 - 10 mars 2022

* Stöd för spårning har lagts till [!DNL control (default)] Adobe Target upplevelser.
* Optimerade vyändringshändelser för ensidesprogram. Visningsmeddelandet ingår nu i händelsen view-change när personaliserade upplevelser återges.
* Konsolvarning har tagits bort när ingen `eventType` är närvarande.
* Ett problem där `propositions` egenskapen returnerades endast från en `sendEvent` när upplevelser begärdes eller hämtades från cachen. The `propositions` kommer nu alltid att definieras som en array.
* Korrigerade ett problem där dolda behållare inte visades när ett fel returnerades från Adobe Experience Edge.
* Ett problem där interaktionshändelserna inte räknades i Adobe Target har korrigerats. Detta korrigerades genom att vynamnet lades till i XDM på web.webPageDetails.viewName.
* Åtgärda brutna dokumentationslänkar i konsolmeddelanden.

## Version 2.8.0 - 19 januari 2022

* Stöd för skugg-DOM-väljare för personalisering.
* Ändrade namn på händelsetyper för personalisering. (`display` och `click` bli `decisioning.propositionDisplay` och `decisioning.propositionInteract`)
* Ett problem har korrigerats där HTML erbjuder med infogade script-taggar lade till script-taggarna två gånger på sidan trots att skriptet bara kördes en gång.

## Version 2.7.0 - 26 oktober 2021

* Exponera ytterligare information från Experience Edge i det returnerade värdet från `sendEvent`, inklusive `inferences` och `destinations`. Formatet på dessa egenskaper kan ändras eftersom dessa funktioner för närvarande lanseras som en del av en betaversion. Mer information finns i [Spåra händelser.](fundamentals/tracking-events.md)

## Version 2.6.4 - 7 september 2021

* Ett problem har korrigerats där angivna HTML Adobe Target-åtgärder tillämpades på `head` -elementet ersatte hela `head` innehåll. Ange nu HTML-åtgärder för `head` -elementet ändras till HTML.

## Version 2.6.3 - 16 augusti 2021

* Ett problem där objekt som inte är avsedda för allmän användning exponerades genom det lösta löftet från `configure` -kommando.

## Version 2.6.2 - 4 augusti 2021

* Ett problem där en varning om borttagning av `result.decisions` (tillhandahålls av `sendEvent` ) loggas på konsolen även när `result.decisions` gick inte att komma åt egenskapen. Ingen varning loggas vid åtkomst till `result.decisions` men egenskapen är fortfarande föråldrad.

## Version 2.6.1 - 29 juli 2021

* Ett problem har korrigerats där återgivning av personalisering för en enkelsidig appvy som inte har något personaliseringsinnehåll skulle orsaka ett fel och orsaka löftet som returnerades från `sendEvent` som ska avvisas.

## Version 2.6.0 - 27 juli 2021

* Innehåller mer personaliseringsinnehåll i `sendEvent` lösta löften, inklusive Adobe Target svarstoken. När `sendEvent` kommandot körs, ett löfte returneras, som till slut löses med ett `result` objekt som innehåller information som tagits emot från servern. Tidigare innehöll det här resultatobjektet en egenskap med namnet `decisions`. Detta `decisions` egenskapen har tagits bort. En ny egenskap, `propositions`, har lagts till. Den nya egenskapen ger kunderna tillgång till mer personaliserat innehåll, inklusive [svarstoken](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Version 2.5.0 - juni 2021

* Stöd för omdirigeringserbjudanden om personalisering har lagts till.
* Automatiskt insamlade visningsrutebredder och -höjder som är negativa värden skickas inte längre till servern.
* När en händelse avbryts genom att returnera `false` från `onBeforeEventSend` återanrop, ett meddelande loggas nu.
* Korrigerade ett problem där specifika XDM-data avsedda för en enda händelse inkluderades för flera händelser.

## Version 2.4.0 - mars 2021

* SDK kan nu [installeras som ett npm-paket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Stöd för `out` alternativ när [konfigurera standardsamtycke](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), som släpper alla händelser tills samtycke tas emot (den befintliga `pending` Alternativet placerar händelser i kö och skickar dem när de har fått sitt samtycke).
* The [onBeforeEventSend callback](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kan nu användas för att förhindra att en händelse skickas.
* Använder nu en XDM-schemafältgrupp i stället för `meta.personalization` när du skickar händelser om personligt innehåll som återges eller klickas.
* The [getIdentity, kommando](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) returnerar nu kantområdes-ID:t bredvid identiteten.
* Varningar och fel som tagits emot från servern har förbättrats och hanteras på ett mer lämpligt sätt.
* Stöd för [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Inställningarna för samtycke, när de tas emot, hashas och lagras i lokal lagring för en optimerad integrering mellan CMP, Platform Web SDK och Platform Edge Network. Om du samlar in medgivandeinställningar får du nu gärna ringa `setConsent` på varje sida som läses in.
* Två [övervaka kopplingar](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` och `onCommandRejected`, har lagts till.
* Felkorrigering: Meddelandehändelser för anpassningsinteraktion innehåller dubblettinformation om samma aktivitet när en användare navigerade till en ny enkelsidig appvy, tillbaka till den ursprungliga vyn och klickade på ett element som är kvalificerat för konvertering.
* Felkorrigering: Om den första händelsen som skickades av SDK hade `documentUnloading` ange till `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) används för att skicka händelsen, vilket resulterar i ett fel som rör en identitet som inte har etablerats.

## Version 2.3.0 - november 2020

* Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
* Ytterligare stöd för personalisering för ensidiga applikationer.
* Förbättrad kompatibilitet med annan JavaScript-kod på sidan som kan skrivas över `window.console` API:er.
* Felkorrigering: `sendBeacon` användes inte när `documentUnloading` har angetts till `true` eller när länkklickningar spåras automatiskt.
* Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
* Felkorrigering: Vissa webbläsarfel som innehåller skrivskydd `message` -egenskapen hanterades inte på rätt sätt vilket resulterade i att ett annat fel exponerades för kunden.
* Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0 - oktober 2020

* Felkorrigering: Opt-in-objektet blockerade Alloy från att ringa anrop när `idMigrationEnabled` är `true`.
* Felkorrigering: Meddela Alloy om det finns förfrågningar om att returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0 - augusti 2020

* Ta bort `syncIdentity` och support som skickar dessa ID:n i `sendEvent` -kommando.
* Stöd för IAB 2.0 Consent Standard.
* Stöd för att skicka ytterligare ID:n i `setConsent` -kommando.
* Stöd som åsidosätter `datasetId` i `sendEvent` -kommando.
* Bildskärmar med stöd för legering ([Läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pass `environment: browser` i implementeringens kontextdata.
