---
title: Versionsinformation för Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versionsinformation;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 7d7a9357f17b941a8f7800be86f211bb1276698d
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Versionsinformation

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
