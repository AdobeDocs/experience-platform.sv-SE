---
title: Versionsinformation om Adobe Target v2-tillägget
description: Den senaste versionsinformationen om taggtillägget Adobe Target v2 i Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: a062305e3ed0eb4d127f93ff37efe15e41eaa601
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Versionsinformation om Adobe Target v2-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

## v0.20.3 (23 januari 2024)

- Uppdaterat till stöd för `at.js` 2.11.4
- Korrigerade ett fel för att förhindra att ogiltiga geodata skickas till leverans-API.

## v0.20.2 (29 november 2023)

- Uppdaterat till stöd för `at.js` 2.11.3
- Korrigerade ett fel som förhindrade att svarstoken skickades på händelser som inte kunde återges vid innehållsrendering.

## v0.20.1 (3 november 2023)

- Uppdaterat för stöd av `at.js` 2.11.2.
- Korrigerade ett fel som orsakade inkonsekvenser i de svarstoken som skickades för anpassade händelser.

## v0.20.0 (9 oktober 2023)

- Uppdaterat för stöd av `at.js` 2.11.0.
- Stöd har lagts till för att ställa in anpassade Adobe Experience Platform sandboxId och sandboxName i targetGlobalSettings, som skickas till Delivery API för getOffer-/getOffers-anrop.
- Korrigering av skugg-DOM för kedja:eq() i väljaren.

## v0.19.3 (18 september 2023)

- Uppdaterat för stöd av `at.js` v2.10.3.
- Korrigerade ett problem som felaktigt utlöste den anpassade händelsen vid innehållsåtergivning när inga erbjudanden renderades. Den rätta händelsen, at-content-rendering-no-offers, aktiveras nu.
- EventToken och responseTokens har lagts till i felobjektet för den anpassade händelsen at-content-rendering-failed.

## v0.19.2 (14 februari 2023)

- Ett problem med att tillåta timeout för ett dataelement har korrigerats.

## v0.19.1 (3 februari 2023)

- Uppdaterat för stöd av `at.js` v2.10.1
- Klientens anpassade Mbox-parametrar har nu korrekt stöd för punktnotation
- Leveranssamtal som inte längre görs i VEC

## v0.19.0 (19 september 2022)

- Uppdaterat för stöd för `at.js` v2.10.0
- Stöd för domänövergripande spårning har lagts till.

## v0.18.0 (1 juni 2022)

- Uppdaterat till stöd för `at.js` v2.9.0
- Stöd för klienttips för användaragent har lagts till.

## v0.17.1 (28 januari 2022)

- Uppdaterat till stöd för `at.js` v2.8.1
- Korrigerad `pageLoad` mappas inte till `target-global-mbox` i ODD-hybridkörningsläge
- Ett problem med analysinformation för `mbox`-begäran har korrigerats
- Uppgraderade utvecklarberoenden för att åtgärda säkerhetsproblem

## v0.17.0 (7 januari 2022)

- Uppdaterat för stöd för `at.js` v2.8.0, som nu samlar in data om funktionsanvändning och telemetri för prestanda.  Personuppgifter samlas inte in. Om du vill avanmäla dig från den här funktionen anger du `telemetryEnabled` till `false` i `targetGlobalSettings`.

## v0.16.0 (28 oktober 2021)

- Uppdaterat för stöd för `at.js` v2.7.0, som nu kan hämtas från Adobe Target.

## v0.15.2 (16 augusti 2021)

- Uppdaterat för stöd av `at.js` 2.6.1.
- Initiera On-Device-beslut vid start oberoende av sidinläsningshändelsen.
- Enhetsbeslut kan nu användas vid första besök efter att artefakten har hämtats.

## v0.15.1 (20 juli 2021)

- Korrigerade ett problem med ett `stringify`-funktionsnamn som orsakade att felaktiga UUID-värden genererades för `sessionId`, `requestId` och så vidare.

## v0.15.0 (16 juli 2021)

- Lägg till ett säkert attribut till cookies när `at.js`-inställningarna secureOnly är inställda på true
- Svarstoken är nu tillgängliga när `triggerView()` används
- Ett fel som är relaterat till `CONTENT_RENDERING_NO_OFFERS`-händelsen har korrigerats. Nu aktiveras det korrekt när inget innehåll returneras från Target
- A4T-klickmätningsdetaljer returneras korrekt när förhämtningsbegäranden används
- UUID-generering använder inte längre `Math.random()`, men är beroende av `window.crypto`
- `sessionId`-cookie-förfallodatum har utökats korrekt för varje nätverksanrop
- Initieringen av SPA-vycachen hanteras nu korrekt och inställningarna för `viewsEnable` följs

## v0.14.2 (2 juni 2021)

- Åtgärda ett fel där det slutliga paketet innehåller två `at.js` versioner, en med On-Device Decisioning och en utan.

## v0.14.1 (19 maj 2021)

- Korrigera regression som introducerades i version 0.14 där Load Target-åtgärden utlöste globala mbox-anrop

## v0.14 (14 maj 2021)

- Lagt till ett nytt Load Target-funktionsmakro med [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning), som läser in `at.js` 2.5 med beslutsfunktioner på enheten
- Uppdaterat `at.js` till 2.5


## v0.13.7 (25 mars 2021)

- Ett problem med att `targetPageParams` togs med i mbox-begäranden har korrigerats. `targetPageParams` ska endast inkluderas i `pageLoad`-begäranden.
- Korrigerade ett problem med globala dokument- och fönsterobjekt i taggtillägget genom att ersätta globala objektberoenden med direkta referenser till dem.
- Uppdaterade `at.js` till 2.4.1.

## v0.13.6 (25 januari 2021)

- Lägger till stöd för en enhetlig profil/plattform-ID för leverans-API customerIds
- Korrigerar ogiltig formattaggsinmatning
- Uppdaterat kl. 2.4.0
- Ett problem där odefinierade parametrar kan leda till felaktiga leveransbegäranden har åtgärdats

## v0.13.4 (25 november 2020)

- Korrigerade ett fel där mbox-parametrar inte visades i användargränssnittet
- Varumärkesuppdateringar
- Uppdaterat version `at.js` till 2.3.3

## v0.13.3 (24 juli 2020)

- Korrigerade ett fel som orsakade att QA-lägeslänkar inte fungerade för inaktiva aktiviteter
- Korrigerade ett fel när tillägget misslyckas om ett skript eller en kod lägger till egenskapen `default` i `window` eller `document`

## v0.13.2 (15 juni 2020)

- Ett problem har korrigerats när CNAME och kantåsidosättning användes, där `at.js` 1.x felaktigt kunde skapa serverdomänen, vilket resulterade i att Target-begäran misslyckades
- Ett problem har korrigerats där Target fördröjde anropet från Analytics sendBeacon när v2-taggtillägget för Target och Adobe Analytics användes
- Inställningen `deviceIdLifetime` har förbättrats genom att den kan åsidosättas via `targetGlobalSettings`

## v0.13.0 (25 mars 2020)

- Uppdaterade `at.js` till v2.3.
- Stöd för global Mbox-målmapp har lagts till i API:t adobe.target.getOffer
- Ett problem har korrigerats där parametrar och sidinläsningsparametrar inte bearbetades korrekt

## v0.12.0 (10 oktober 2019)

- Uppdaterade `at.js` till v2.2.
- Förbättrade prestanda för integrering mellan Experience Cloud ID-bibliotek (ECID) v4.4 och `at.js` 2.2.
- Tidigare gjorde ECID-biblioteket två blockerande anrop innan `at.js` kunde hämta upplevelser. Detta har reducerats till ett enda samtal, vilket avsevärt förbättrar prestandan.

>[!NOTE]
>Uppgradera ditt ECID-taggtillägg till v4.4.1 om du vill utnyttja den här prestandaförbättringen.

## v0.11.1 (31 juli 2019)

- Tilläggsversionen har uppdaterats så att `at.js` 2.1.1 används
- En korrigering för hantering av parametrar har lagts till

## v0.11.0 (3 juni 2019)

- Nytt taggtillägg som stöder `at.js` 2.1
