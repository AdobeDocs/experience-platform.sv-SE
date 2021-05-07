---
title: Versionsinformation för Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen för Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versionsinformation;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Versionsinformation

## Version 2.4.0, mars 2021

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

## Version 2.3.0, november 2020

* Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
* Ytterligare stöd för personalisering för ensidiga applikationer.
* Förbättrad kompatibilitet med annan JavaScript-kod som kan skriva över `window.console` API:er.
* Felkorrigering: `sendBeacon` användes inte när `documentUnloading` var inställt på `true` eller när länkklick spårades automatiskt.
* Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
* Felkorrigering: Vissa webbläsarfel som innehåller en skrivskyddad `message`-egenskap hanterades inte korrekt, vilket resulterade i att ett annat fel exponerades för kunden.
* Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0, oktober 2020

* Felkorrigering: Opt-in-objektet blockerade Alloy från att ringa anrop när `idMigrationEnabled` är `true`.
* Felkorrigering: Meddela Alloy om det finns förfrågningar om att returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0, augusti 2020

* Ta bort kommandot `syncIdentity` och stöd för att skicka dessa ID:n i kommandot `sendEvent`.
* Stöd för IAB 2.0 Consent Standard.
* Stöd för att skicka ytterligare ID:n i kommandot `setConsent`.
* Stöd för att åsidosätta `datasetId` i kommandot `sendEvent`.
* Bildskärmar för supportallokering ([Läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Skicka `environment: browser` i kontextdata för implementeringsinformation.
