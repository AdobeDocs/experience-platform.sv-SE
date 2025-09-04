---
title: Versionsinformation om Adobe Experience Platform Web SDK
description: Den senaste versionsinformationen om webb-SDK för Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Experience Platform Web SDK;Web SDK;versionsinformation;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 05b9893e17db0caeab1175f35f939cb6a1dd0291
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 1%

---


# Versionsinformation om SDK för webben

Det här dokumentet innehåller versionsinformation för Adobe Experience Platform Web SDK.
Den senaste versionsinformationen om SDK-taggtillägget för webben finns i [Versionsinformationen om SDK-taggtillägg för webben](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Version 2.29.0 - 4 september 2025

**Nya funktioner**

- Stöd för insamling av Adobe Advertisement-data för Adobe Journey Analytics har lagts till
- Stöd för inspelning av push-prenumerationsinformation i användarprofiler har lagts till.

**Korrigeringar och förbättringar**

- Korrigerade ett problem där avsnitt för config override sammanfogades i stället för att ersättas.
- Korrigerade ett fall där länksamlingen skickade hela dokumentinnehållet som länknamn.
- Korrigerade ett problem där vissa förslag inte kunde återges på nytt.

## Version 2.28.1 - 31 juli 2025

**Korrigeringar och förbättringar**

- Korrigerade ett problem som förhindrade att anpassade byggen kördes.

## Version 2.28.0 - 24 juli 2025

**Nya funktioner**

- Stöd för Adobe Journey Optimizer diskvalificeringsregler har lagts till.

**Korrigeringar och förbättringar**

- Korrigerade ett fel i [Media Analytics-spåraren](commands/getmediaanalyticstracker.md) där egenskapen `length` för mediaobjektet felaktigt accepterade ogiltiga datatyper.
- Förbättrad felhantering för [identitetshantering](identity/overview.md) för att kunna bearbeta löftesavvisanden korrekt när identitetssökningen misslyckas.
- Ett problem där [personaliseringsinnehåll](personalization/rendering-personalization-content.md) med HTML-innehållsobjekt inte kunde återges har åtgärdats. Felet beror på att `renderStatusHandler` saknas.
- Åtgärdade aktivitetskartan [URL-samling](commands/configure/clickcollectionenabled.md) för att hantera URL:er som inte är HTTP.

**Kända fel**

- Den [anpassade build](/help/web-sdk/install/create-custom-build.md)-processen som använder `npx @adobe/alloy` fungerar för närvarande inte som förväntat i version 2.28.0. Alla komponenter inkluderas i det genererade bygget, oavsett vilka moduler som har valts. Problemet påverkar inte JavaScript-standardfilen som finns i CDN. En korrigering pågår.

## Version 2.27.0 - 20 maj 2025

**Korrigeringar och förbättringar**

- Ett problem med meddelanden i appen där den anpassade formateringen inte tillämpades korrekt har korrigerats.
- Ändrade formatet för händelsehistorik. Detta gör att meddelanden och innehållskort visas igen när gamla historikdata tas bort.
- Korrigerade ett problem där förslag skulle återanvändas i SPA-användningsfall.
- Ett problem med klickspårning på skuggans DOM-element har korrigerats.

## Version 2.26.0 - 5 mars 2025

**Nya funktioner**

- Nu kan du använda Web SDK NPM-paketet för att skapa anpassade Web SDK-byggen och endast välja de bibliotekskomponenter som du behöver. Detta leder till mindre biblioteksstorlek och optimerade inläsningstider. Se dokumentationen om hur du [skapar en anpassad Web SDK-version med NPM-paketet](install/create-custom-build.md).
- Kommandot [`getIdentity`](commands/getidentity.md) läser nu automatiskt ECID direkt från identitetscookien `kndctr`. Om du anropar `getIdentity` med namnutrymmet `ECID` och det redan finns en identitetscookie, skickar Web SDK inte längre någon begäran till Edge Network om att hämta identiteten. Nu läser den identiteten från kakan.

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där `getIdentity`-kommandon inte returnerade identiteten efter att ett `collect`-anrop skickades.
- Ett problem där omdirigering av personalisering orsakade att innehållet flimrades innan omdirigeringen inträffade har åtgärdats.

## Version 2.25.0 - 23 januari 2025

**Korrigerade och förbättrade**

- Validering av alternativ har lagts till för kommandot `setDebug`.
- En varning lades till när en `onBeforeLinkClickSend`-funktion eller en nedladdningslänkkvalificerare konfigurerades när klicksamlingen är inaktiverad.
- Korrigerade ett problem där renderade inlägg inte inkluderades i visningsmeddelanden.

**Nya funktioner**

- Implementerade en reserv till den konfigurerade Edge-domänen när cookies från tredje part är aktiverade och förfrågningar till adobedc.demdex.net blockeras.

## Version 2.24.1 - 6 december 2024

**Korrigerade och förbättrade**

- Ett beroendeproblem relaterat till [Adobe Experience Platform Rules Engine](https://github.com/adobe/aepsdk-rulesengine-typescript/) som orsakade fel i vissa kundintegreringar har åtgärdats. Web SDK kräver nu [Adobe Experience Platform Rules Engine](https://github.com/adobe/aepsdk-rulesengine-typescript/) version 2.0.3 eller senare.

## Version 2.24.0 - 31 oktober 2024

**Nya funktioner**

- [Åsidosättningar av dataström](../datastreams/overrides.md) stöds nu när mediesessioner startas.

- Stöd för Adobe Target-svarstoken har lagts till i övervakningskiten [`onContentRendering`](monitoring-hooks.md#onContentRendering).

**Korrigeringar och förbättringar**

- När flera meddelanden i appen returneras visas endast meddelanden med den högsta prioriteten. De andra spelas in som undertryckta.
- Tomma datastream-åsidosättningar skickas inte längre till Edge Network, vilket minskar eventuella konflikter med routningskonfigurationer på serversidan.
- Följande loggningsmeddelandekomponentnamn har bytt namn så att de överensstämmer med andra Adobe SDK:er:
   - `DecisioningEngine` har bytt namn till `RulesEngine`
   - `LegacyMediaAnalytics` har bytt namn till `MediaAnalyticsBridge`
   - `Privacy` har bytt namn till `Consent`
- Korrigerade ett fel som uppstod när standardinnehållsobjekt renderades via [`applyPropositions`](../web-sdk/commands/applypropositions.md).
- Korrigerade ett CSS-fel i Adobe Target åtgärder för att flytta och ändra storlek.
- Nyckeln `machineLearning` har tagits bort från [`sendEvent`](../web-sdk/commands/sendevent/overview.md) svar.

## Version 2.23.0 - 19 september 2024

**Nya funktioner**

- Stöd har lagts till för att begära [CORE ID](identity/overview.md#tracking-coreid-web-sdk) i kommandot [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library).

**Korrigeringar och förbättringar**

- Korrigerade ett problem där cookies inte skrevs korrekt när Web SDK kördes lokalt.

## Version 2.2.0 - 22 augusti 2024

**Nya funktioner**

- Stöd för personaliseringsövervakningshooks har lagts till.

**Korrigeringar och förbättringar**

- Stöd för Internet Explorer har tagits bort, vilket minskar bibliotekets GZIP-storlek med 9 %.
- Ett problem har korrigerats där aktivitetskartans länkinformation inte initierades när övervakarkroken `onInstanceConfigured` anropades.
- Ett problem har korrigerats där cookies-mål inte hade angetts till rätt sökväg.
- Ett kundproblem med att ringa har korrigerats.
- Korrigerade ett problem där en ogiltig URL-kodning i parametern `adobe_mc` orsakade att [ sendEvent](commands/sendevent/overview.md) anrop misslyckades.

## Version 2.21.1 - 18 juli 2024

**Korrigeringar och förbättringar**

- Ett byggfel har korrigerats vid användning av NPM-bibliotek.

## Version 2.21.0 - 16 juli 2024

**Nya funktioner**

- Stöd för automatisk spårning av offertinteraktion har lagts till.
- Ett anpassat byggskript med en alloy.js-fil har lagts till.
- Förbättrad klicksamling med stöd för ActivityMap och händelsegruppering.

## Version 2.20.0 - 21 maj 2024

**Nya funktioner**

- Stöd har lagts till för [direktuppspelad mediesamling](../web-sdk/commands/configure/streamingmedia.md).

**Korrigeringar och förbättringar**

- Korrigerade ett fel som gjorde att standardinnehållet doldes av det föregående fragmentet när samtycke valdes ut.

## Version 2.19.2 - 10 januari 2024

**Korrigeringar och förbättringar**

- Ett problem där identitetsfel maskerade andra fel har korrigerats och identitetsfel har ändrats till varningar har åtgärdats.
- Ett problem har korrigerats där längst ned på sidanrop aldrig skulle skickas när det fanns ett överst på sidanropet med `renderDecisions` inställt på `false`.
- Korrigerade ett problem där Web SDK inte kunde läsa korsdomänsidentiteter när det fanns flera `adobe_mc` frågesträngsparametrar.

## Version 2.19.1 – 10 november 2023

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där förslagsmatrisen som returnerades från `sendEvent` anrop alltid var tom.

## Version 2.19.0 - 1 november 2023

**Nya funktioner**

- Stöd för återgivning av meddelanden i appen från Adobe Journey Optimizer har lagts till.
- Stöd för [övre och nedre delen av sidhändelser](use-cases/top-bottom-page-events.md) har lagts till.
- Alternativet [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) har lagts till i kommandot `sendEvent` för att styra begäran om sidomfånget och standardytan.

**Korrigeringar och förbättringar**

- Kombinerad personalisering visar händelser tillsammans vid återgivning av flera typer av personalisering.
- Ett problem där namn på en programvy på en sida var skiftlägeskänsliga har korrigerats.
- Ett problem med skugg-DOM-anpassade erbjudandeväljare har korrigerats.

## Version 2.18.0 - 31 juli 2023

**Nya funktioner**

- Stöd har lagts till för [åsidosättningar av datastream-ID:t ](../datastreams/overrides.md) per kommando.

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där avslutningslänkar inte kunde kvalificeras på grund av att domänen är en del av frågan.
- `edgeConfigId` har tagits bort till förmån för `datastreamId` i Web SDK-konfigurationen.

## Version 2.17.0 - 17 maj 2023

**Korrigeringar och förbättringar**

- SDK för webben kodar nu Audience Manager cookie-målvärden, som liknar [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html).

## Version 2.16.0 - 25 april 2023

**Nya funktioner**

- Stöd har lagts till för åsidosättande av [datastream-konfigurationen](../datastreams/overrides.md).

## Version 2.15.0 - 30 mars 2023

**Nya funktioner**

- Stöd för länkklickning på [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) har lagts till.
- Stöd för Adobe Journey Optimizer klickspårning har lagts till.

**Korrigeringar och förbättringar**

- Länksamlingen innehåller nu länknamn och besöksregion.
- Konsolfel för misslyckade URL-mål har tagits bort.

## Version 2.14.0 - 25 januari 2023

- (Beta) Stöd för Adobe Journey Optimizer ytor och erbjudanden har lagts till.

**Korrigeringar och förbättringar**

- Ett problem med anpassade kodåtgärder för Adobe Target VEC där koden matades in på en alternativ plats än med [!DNL at.js] har korrigerats.
- Ett problem har korrigerats där refererhuvudet i vissa kantfall inte var korrekt inställt på begäranden till Edge Network.
- Ett problem har korrigerats där egenskaperna för [användaragentens klienttips](/help/web-sdk/use-cases/client-hints.md) kunde anges till en felaktig typ.
- Ett problem har korrigerats där `placeContext.localTime` inte matchade schemat.

## Version 2.13.1 - 13 oktober 2022

- Korrigerade ett problem där besökarmigrering inte fungerar om window.Visitor definieras efter konfiguration. Det här är ett särskilt problem när du kör med Adobe Tags.
- Korrigerade ett problem där `device.screenWidth` och `device.screenHeight` fylldes i som strängar i vissa miljöer.

## Version 2.13.0 - 28 september 2022

**Nya funktioner**

- Stöd har lagts till för [Fullständig sidmigrering](home.md#migrating-to-web-sdk). Adobe Target-profilen bevaras nu när en besökare förflyttar sig mellan at.js och SDK webbsidor.
- Konfigurerbart stöd för [hög entropi-klienttips för användaragent ](/help/web-sdk/use-cases/client-hints.md) har lagts till.
- Stöd för kommandot [`applyResponse`](/help/web-sdk/commands/applyresponse.md) har lagts till. Detta aktiverar hybridanpassning via [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/).
- QA-lägeslänkar fungerar nu på flera sidor.

**Korrigeringar och förbättringar**

- Ett problem har korrigerats där personalisering av klickspårningsstatistik inte uppdaterades när länkspårning inaktiverades.
- Uppdaterade kommandon som genererar ett valideringsfel när okända alternativ anges.
- Egenskapen `_experience.decisioning.propositionEventType` fylls nu i när visnings- och interaktionspersonaliseringshändelser skickas automatiskt.
- Dubblerad namnområdesvalidering har lagts till för kommandot `getIdentity`.
- Dubblettvalideringen av beslutsomfånget för kommandot `sendEvent` har lagts till.

## Version 2.12.0 - 29 juni 2022

- Ändra förfrågningarna till Edge Network om att använda `cluster`-cookie-platstipset som en del av URL:en. Detta garanterar att användare som byter plats (t.ex. genom ett VPN eller kör med mobila enheter, etc.) når samma kant och har samma personaliseringsprofil.
- Sträng konfigurerade funktioner i kommandosvaret getLibraryInfo.

## Version 2.11.0 - 13 juni 2022

**Nya funktioner**

- Ni kan nu leverera personaliserade upplevelser mer korrekt genom att dela besökar-ID:n mellan mobilappar och mobilwebbinnehåll samt mellan domäner. Mer information finns i den [dedikerade dokumentationen](identity/id-sharing.md).
- Nu kan du återge eller köra en array med förslag från [!DNL Adobe Target] till ensidiga program, utan att öka analysvärdena. Detta minskar antalet rapporteringsfel och ökar noggrannheten i analysen. Mer information finns i den [dedikerade dokumentationen](personalization/rendering-personalization-content.md#applypropositions).
- Ytterligare information har lagts till för kommandot `getLibraryInfo`, inklusive tillgängliga kommandon och den slutliga konfigurationen för instansen.

**Korrigeringar och förbättringar**

- Uppdaterade cookie-inställningar för att använda `sameSite="none"` och `secure`-flaggan på [!DNL HTTPS] sidor.
- Ett problem har korrigerats där anpassat innehåll inte tillämpades korrekt när pseudoväljaren `eq` användes.
- Korrigerade ett problem där `localTimezoneOffset` kunde misslyckas med Experience Platform-validering.

## Version 2.10.1 - 3 maj 2022

- Korrigerade ett problem där flera beständiga iframes skapades för ID-synkronisering och segmentmål.

## Version 2.10.0 - 22 april 2022

- Använd en beständig iframe för alla ID-synkroniseringar och segmentmål.
- Korrigerade ett problem där sammanslagna mätvärden duplicerades i resultatet `sendEvent`.

## Version 2.9.0 - 10 mars 2022

- Stöd för att spåra [!DNL control (default)] Adobe Target-upplevelser har lagts till.
- Optimerade vyändringshändelser för ensidesprogram. Visningsmeddelandet ingår nu i händelsen view-change när personaliserade upplevelser återges.
- Konsolvarning har tagits bort när `eventType` inte finns.
- Ett problem har korrigerats där egenskapen `propositions` bara returnerades från ett `sendEvent`-kommando när upplevelser begärdes eller hämtades från cachen. Egenskapen `propositions` kommer nu alltid att definieras som en matris.
- Korrigerade ett problem där dolda behållare inte visades när ett fel returnerades från Edge Network.
- Ett problem där interaktionshändelserna inte räknades i Adobe Target har korrigerats. Detta korrigerades genom att vynamnet lades till i XDM på web.webPageDetails.viewName.
- Åtgärda brutna dokumentationslänkar i konsolmeddelanden.

## Version 2.8.0 - 19 januari 2022

- Stöd för skugg-DOM-väljare för personalisering.
- Ändrade namn på händelsetyper för personalisering. (`display` och `click` blir `decisioning.propositionDisplay` och `decisioning.propositionInteract`)
- Ett problem har korrigerats där HTML erbjuder med infogade script-taggar lade till script-taggarna två gånger på sidan trots att skriptet bara kördes en gång.

## Version 2.7.0 - 26 oktober 2021

- Visa ytterligare information från Edge Network i returvärdet från `sendEvent`, inklusive `inferences` och `destinations`. Formatet på dessa egenskaper kan ändras eftersom dessa funktioner för närvarande lanseras som en del av en Beta.

## Version 2.6.4 - 7 september 2021

- Ett problem har korrigerats där de angivna HTML Adobe Target-åtgärderna för elementet `head` ersatte hela `head`-innehållet. Ange nu att HTML-åtgärder som används för elementet `head` ska läggas till i HTML.

## Version 2.6.3 - 16 augusti 2021

- Korrigerade ett problem där objekt som inte är avsedda för allmän användning exponerades via det lösta löftet från kommandot `configure`.

## Version 2.6.2 - 4 augusti 2021

- Ett problem har korrigerats där en varning om borttagning av `result.decisions` (som tillhandahålls av kommandot `sendEvent`) skulle loggas på konsolen även när egenskapen `result.decisions` inte användes. Ingen varning loggas vid åtkomst till egenskapen `result.decisions`, men egenskapen är fortfarande föråldrad.

## Version 2.6.1 - 29 juli 2021

- Ett problem har korrigerats där återgivningspersonalisering för en enkelsidig appvy som inte har något personaliseringsinnehåll skulle orsaka ett fel och få löftet som returnerades från `sendEvent`-kommandot att avvisas.

## Version 2.6.0 - 27 juli 2021

- Tillhandahåller mer personaliseringsinnehåll i det `sendEvent` lösta löftet, inklusive Adobe Target svarstoken. När kommandot `sendEvent` körs returneras ett löfte, som till slut löses med ett `result`-objekt som innehåller information som tagits emot från servern. Tidigare innehöll det här resultatobjektet egenskapen `decisions`. Den här `decisions`-egenskapen har tagits bort. En ny egenskap, `propositions`, har lagts till. Den här nya egenskapen ger kunderna åtkomst till mer personaliserat innehåll, inklusive [svarstoken](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Version 2.5.0 - juni 2021

- Stöd för omdirigeringserbjudanden om personalisering har lagts till.
- Automatiskt insamlade visningsrutebredder och -höjder som är negativa värden skickas inte längre till servern.
- När en händelse avbryts genom att `false` returneras från ett `onBeforeEventSend`-återanrop loggas nu ett meddelande.
- Korrigerade ett problem där specifika XDM-data avsedda för en enda händelse inkluderades för flera händelser.

## Version 2.4.0 - mars 2021

- SDK kan nu installeras som ett [NPM-paket](/help/web-sdk/install/npm.md).
- Stöd för ett `out`-alternativ har lagts till när [standardmedgivande](/help/web-sdk/commands/configure/defaultconsent.md) konfigureras, vilket innebär att alla händelser utesluts tills medgivande tas (det befintliga `pending`-alternativet placerar händelser i kö och skickar dem när medgivande tas emot).
- Återanropet [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) kan nu användas för att förhindra att en händelse skickas.
- Använder nu en XDM-schemafältgrupp i stället för `meta.personalization` när händelser skickas om anpassat innehåll som återges eller klickas.
- Kommandot [`getIdentity`](/help/web-sdk/commands/getidentity.md) returnerar nu kantområdes-ID:t bredvid identiteten.
- Varningar och fel som tagits emot från servern har förbättrats och hanteras på ett mer lämpligt sätt.
- Stöd har lagts till för Adobe Consent 2.0-standarden för kommandot [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Inställningarna för godkännande, när de tas emot, hashas och lagras i ett lokalt lager för en optimerad integrering mellan CMP, Experience Platform Web SDK och Experience Platform Edge Network. Om du samlar in medgivandeinställningar får du nu gärna ringa `setConsent` vid varje sidinläsning.
- Två [övervakningskopplingar ](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` och `onCommandRejected` har lagts till.
- Felkorrigering: Meddelandehändelser för interaktion i Personalization innehåller dubblettinformation om samma aktivitet när en användare navigerade till en ny enkelsidig programvy, tillbaka till den ursprungliga vyn och klickade på ett element som är kvalificerat för konvertering.
- Felkorrigering: Om den första händelsen som skickades av SDK hade `documentUnloading` inställt på `true`, skulle [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) användas för att skicka händelsen, vilket resulterar i ett fel om att en identitet inte har etablerats.

## Version 2.3.0 - november 2020

- Stöd för nonce har lagts till för att möjliggöra striktare skyddsprofiler för innehåll.
- Ytterligare stöd för personalisering för ensidiga applikationer.
- Förbättrad kompatibilitet med annan JavaScript-kod som kan skriva över `window.console` API:er.
- Felkorrigering: `sendBeacon` användes inte när `documentUnloading` var inställt på `true` eller när länkklick spårades automatiskt.
- Felkorrigering: En länk spåras inte automatiskt om ankarelementet innehåller HTML-innehåll.
- Felkorrigering: Vissa webbläsarfel som innehåller en skrivskyddad `message`-egenskap hanterades inte korrekt, vilket resulterade i att ett annat fel exponerades för kunden.
- Felkorrigering: Om du kör SDK i en iframe uppstår ett fel om iframe-fönstrets HTML-sida kommer från en annan underdomän än det överordnade fönstrets HTML-sida.

## Version 2.2.0 - oktober 2020

- Felkorrigering: Opt-in-objektet blockerade webb-SDK från att ringa anrop när `idMigrationEnabled` är `true`.
- Felkorrigering: Gör Web SDK medveten om förfrågningar som bör returnera personaliseringserbjudanden för att förhindra flimmer.

## Version 2.1.0 - augusti 2020

- Ta bort kommandot `syncIdentity` och stöd för att skicka dessa ID:n i kommandot `sendEvent`.
- Stöd för IAB 2.0 Consent Standard.
- Stöd för att skicka ytterligare ID i kommandot `setConsent`.
- Stöd för att åsidosätta `datasetId` i kommandot `sendEvent`.
- Supportövervakningshooks ([Läs mer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Skicka `environment: browser` i kontextdata för implementeringsinformation.
