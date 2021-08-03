---
title: Versionsinformation för Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versionsinformation;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 165c9bce5dabce9704202ebab6b97a4a30e4ca00
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Versionsinformation

## Version 2.6.2 - 4 augusti 2021

* Ett problem har korrigerats där en varning om borttagning av `result.decisions` (tillhandahålls av kommandot `sendEvent`) skulle loggas på konsolen även när det inte gick att komma åt egenskapen `result.decisions`. Ingen varning loggas vid åtkomst till egenskapen `result.decisions`, men egenskapen är fortfarande föråldrad.

## Version 2.6.1 - 29 juli 2021

* Ett problem har korrigerats där återgivningspersonalisering för en enkelsidig appvy utan något personaliseringsinnehåll skulle orsaka ett fel och få löftet som returnerades från kommandot `sendEvent` att avvisas.

## Version 2.6.0 - 27 juli 2021

* Tillhandahåller mer personaliseringsinnehåll i det lösta löftet `sendEvent`, inklusive Adobe Target svarstoken. När kommandot `sendEvent` körs returneras ett löfte som slutligen löses med ett `result`-objekt som innehåller information som tagits emot från servern. Det här resultatobjektet innehåller egenskapen `decisions`. Den här `decisions`-egenskapen har tagits bort. En ny egenskap, `propositions`, har lagts till. Den nya egenskapen ger kunderna tillgång till mer personaliserat innehåll, inklusive svarstokens. Mer dokumentation kommer snart.

## Version 2.5.0 - juni 2021

* Stöd för omdirigeringserbjudanden om personalisering har lagts till.
* Automatiskt insamlade visningsrutebredder och -höjder som är negativa värden skickas inte längre till servern.
* När en händelse avbryts genom att `false` returneras från ett `onBeforeEventSend`-återanrop loggas nu ett meddelande.
* Korrigerade ett problem där specifika XDM-data avsedda för en enda händelse inkluderades för flera händelser.

## Version 2.4.0 - mars 2021

* SDK kan nu [installeras som ett npm-paket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Stöd för ett `out`-alternativ har lagts till när [standardgodkännande](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) konfigureras, vilket släpper alla händelser tills samtycke tas emot (det befintliga `pending`-alternativet köar händelser och skickar dem när samtycke tas emot).
* Callback-funktionen [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kan nu användas för att förhindra att en händelse skickas.
* Använder nu en XDM-schemafältgrupp i stället för `meta.personalization` när händelser skickas om anpassat innehåll som återges eller klickas.
* Kommandot [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) returnerar nu kantområdes-ID:t bredvid identiteten.
* Varningar och fel som tagits emot från servern har förbättrats och hanteras på ett mer lämpligt sätt.
* Stöd för [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard) har lagts till.
* Inställningarna för samtycke, när de tas emot, hashas och lagras i lokal lagring för en optimerad integrering mellan CMP, Platform Web SDK och Platform Edge Network. Om du samlar in medgivandeinställningar rekommenderar vi nu att du ringer `setConsent` vid varje sidinläsning.
* Två [övervakningskopplingar](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` och `onCommandRejected` har lagts till.
* Felkorrigering: Meddelandehändelser för anpassningsinteraktion innehåller dubblettinformation om samma aktivitet när en användare navigerade till en ny enkelsidig appvy, tillbaka till den ursprungliga vyn och klickade på ett element som är kvalificerat för konvertering.
* Felkorrigering: Om den första händelsen som skickades av SDK hade `documentUnloading` inställt på `true`, skulle [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) användas för att skicka händelsen, vilket resulterar i ett fel om att en identitet inte har etablerats.

## Version 2.3.0 - november 2020

* Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
* Ytterligare stöd för personalisering för ensidiga applikationer.
* Förbättrad kompatibilitet med annan JavaScript-kod som kan skriva över `window.console` API:er.
* Felkorrigering: `sendBeacon` användes inte när `documentUnloading` var inställt på `true` eller när länkklick spårades automatiskt.
* Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
* Felkorrigering: Vissa webbläsarfel som innehåller en skrivskyddad `message`-egenskap hanterades inte korrekt, vilket resulterade i att ett annat fel exponerades för kunden.
* Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0 - oktober 2020

* Felkorrigering: Opt-in-objektet blockerade Alloy från att ringa anrop när `idMigrationEnabled` är `true`.
* Felkorrigering: Meddela Alloy om det finns förfrågningar om att returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0 - augusti 2020

* Ta bort kommandot `syncIdentity` och stöd för att skicka dessa ID:n i kommandot `sendEvent`.
* Stöd för IAB 2.0 Consent Standard.
* Stöd för att skicka ytterligare ID:n i kommandot `setConsent`.
* Stöd för att åsidosätta `datasetId` i kommandot `sendEvent`.
* Bildskärmar för supportallokering ([Läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Skicka `environment: browser` i kontextdata för implementeringsinformation.
