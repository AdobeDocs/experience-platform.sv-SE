---
title: Versionsinformation om Adobe Target v2-tillägget
description: Den senaste versionsinformationen om taggtillägget Adobe Target v2 i Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: e086359916b3aeef73ba9c98e1bfa13da5a974cd
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Versionsinformation om Adobe Target v2-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

## v0.19.2 (14 februari 2023)

- Ett problem med att tillåta timeout för ett dataelement har korrigerats.

## v0.19.0 (19 september 2022)

- Uppdaterat till support `at.js` v2.10.0
- Stöd för domänövergripande spårning har lagts till.

## v0.18.0 (1 juni 2022)

- Uppdaterat till support `at.js` v2.9.0
- Stöd för klienttips för användaragent har lagts till.

## v0.17.1 (28 januari 2022)

- Uppdaterat till support `at.js` v2.8.1
- Fast `pageLoad` inte mappas till `target-global-mbox` i ODD-hybridkörningsläge
- Ett problem med analysinformation för korrigerades `mbox` förfrågan
- Uppgraderade utvecklarberoenden för att åtgärda säkerhetsluckor

## v0.17.0 (7 januari 2022)

- Uppdaterat till support `at.js` v2.8.0, som nu samlar in data om funktionsanvändning och prestanda.  Personuppgifter samlas inte in. Om du vill avanmäla dig från den här funktionen anger du `telemetryEnabled` till `false` in `targetGlobalSettings`.

## v0.16.0 (28 oktober 2021)

- Uppdaterat till support `at.js` v2.7.0, nu tillgängligt för nedladdning från Adobe Target.

## v0.15.1 (20 juli 2021)

- Ett problem med ett `stringify` funktionsnamnskonflikt, vilket ledde till att felaktiga UUID-värden genererades för `sessionId`, `requestId`och så vidare.

## v0.15.0 (16 juli 2021)

- Lägg till ett säkert attribut till cookies när `at.js` settings secureOnly is set to true
- Svarstoken är nu tillgängliga när du använder `triggerView()`
- Korrigerat ett fel som är relaterat till `CONTENT_RENDERING_NO_OFFERS` -händelse. Nu aktiveras det korrekt när inget innehåll returneras från Target
- A4T-klickmätningsdetaljer returneras korrekt när förhämtningsbegäranden används
- UUID-generering använder inte längre `Math.random()`, men förlitar sig på `window.crypto`
- `sessionId` Utgångsdatum för cookie-filen har utökats korrekt för varje nätverksanrop
- Initieringen av SPA-vycachen hanteras nu korrekt och följs `viewsEnable` inställningar

## v0.14.2 (2 juni 2021)

- Åtgärda ett fel där det slutliga paketet innehåller två `at.js` versioner, en med On-Device Decision och en utan.

## v0.14.1 (19 maj 2021)

- Korrigera regression som introducerades i version 0.14 där Load Target-åtgärden utlöste globala mbox-anrop

## v0.14 (14 maj 2021)

- Lagt till ett nytt åtgärdsinläsningsmål med [Beslut på enheten](./overview.md#load-target-with-on-device-decisioning)som läses in `at.js` 2.5 med beslutsfunktioner på enheter
- Uppdaterat `at.js` till 2.5


## v0.13.7 (25 mars 2021)

- Ett problem med `targetPageParams` som ingår i mbox-begäranden. `targetPageParams` bör endast inkluderas i `pageLoad` förfrågningar.
- Korrigerade ett problem med globala dokument- och fönsterobjekt i taggtillägget genom att ersätta globala objektberoenden med direkta referenser till dem.
- Uppdaterat `at.js` till 2.4.1.

## v0.13.6 (25 januari 2021)

- Lägger till stöd för en enhetlig profil/plattform-ID för leverans-API customerIds
- Korrigerar ogiltig formattaggsinmatning
- Uppdaterat kl. 2.4.0
- Ett problem där odefinierade parametrar kan leda till felaktiga leveransbegäranden har åtgärdats

## v0.13.4 (25 november 2020)

- Korrigerade ett fel där mbox-parametrar inte visades i användargränssnittet
- Varumärkesuppdateringar
- Uppdaterade `at.js` version till 2.3.3

## v0.13.3 (24 juli 2020)

- Korrigerade ett fel som orsakade att QA-lägeslänkar inte fungerade för inaktiva aktiviteter
- Korrigerade ett fel när tillägget misslyckas om ett skript eller en kod läggs till `default` egenskapen till `window` eller `document`

## v0.13.2 (15 juni 2020)

- Ett problem har korrigerats när CNAME och kantåsidosättning användes, där `at.js` 1.x kan felaktigt skapa serverdomänen, vilket resulterar i att Target-begäran misslyckas
- Ett problem har korrigerats där Target fördröjde anropet från Analytics sendBeacon när v2-taggtillägget för Target och Adobe Analytics användes
- Förbättrade `deviceIdLifetime` genom att göra den åsidosättningsbar via `targetGlobalSettings`

## v0.13.0 (25 mars 2020)

- Uppdaterat `at.js` till v2.3.
- Stöd för global Mbox-målmapp har lagts till i API:t adobe.target.getOffer
- Ett problem har korrigerats där parametrar och sidinläsningsparametrar inte bearbetades korrekt

## v0.12.0 (10 oktober 2019)

- Uppdaterat `at.js` till v2.2.
- Förbättrade prestanda för integrering mellan Experience Cloud ID-bibliotek (ECID) v4.4 och `at.js` 2.2.
- Tidigare gjorde ECID-biblioteket två blockerande anrop innan `at.js` kan hämta upplevelser. Detta har reducerats till ett enda samtal, vilket avsevärt förbättrar prestandan.

>[!NOTE]
>Uppgradera ditt ECID-taggtillägg till v4.4.1 om du vill utnyttja den här prestandaförbättringen.

## v0.11.1 (31 juli 2019)

- Uppdaterad tilläggsversion som ska användas `at.js` 2.1.1
- En korrigering för hantering av parametrar har lagts till

## v0.11.0 (3 juni 2019)

- Nytt taggtillägg som stöds `at.js` 2.1
