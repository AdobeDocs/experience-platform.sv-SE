---
title: Versionsinformation om Adobe Target v2-tillägget
description: Den senaste versionsinformationen om taggtillägget Adobe Target v2 i Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 42a1ceac3de2244bef858bf03eabe4910ae597f8
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Versionsinformation om Adobe Target v2 Extension

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

## 28 oktober 2021

### Adobe Target v2-tillägg 0.16.0

- Uppdaterat för support på .js v2.7.0 som nu kan laddas ned från Adobe Target.

## 20 juli 2021

### Adobe Target v2-tillägg 0.15.1

- Ett problem med ett `stringify` funktionsnamnskonflikt, vilket ledde till att felaktiga UUID-värden genererades för `sessionId`, `requestId`och så vidare.

## 16 juli 2021

### Adobe Target v2-tillägg 0.15.0

- Lägg till ett säkert attribut i cookies när secureOnly för at.js-inställningarna är true
- Svarstoken är nu tillgängliga när du använder `triggerView()`
- Korrigerat ett fel som är relaterat till `CONTENT_RENDERING_NO_OFFERS` -händelse. Nu aktiveras det korrekt när inget innehåll returneras från Target
- A4T-klickmätningsdetaljer returneras korrekt när förhämtningsbegäranden används
- UUID-generering använder inte längre `Math.random()`, men förlitar sig på `window.crypto`
- `sessionId` Utgångsdatum för cookie-filen har utökats korrekt för varje nätverksanrop
- Initieringen av SPA-vycachen hanteras nu korrekt och följs `viewsEnable` inställningar

## 2 juni 2021

### Adobe Target v2-tillägg 0.14.2

- Åtgärda ett fel där det slutliga paketet innehåller två at.js-versioner, en med On-Device Decision och en utan.

## 19 maj 2021

### Adobe Target v2-tillägg 0.14.1

- Korrigera regression som introducerades i version 0.14 där Load Target-åtgärden utlöste globala mbox-anrop

## 14 maj 2021

### Adobe Target v2-tillägg 0.14

- Lagt till ett nytt åtgärdsinläsningsmål med [Beslut på enheten](./overview.md#load-target-with-on-device-decisioning), som laddas at at.js 2.5 med beslutsfunktioner på enheter
- Uppdaterat at.js till 2.5


## 25 mars 2021

### Adobe Target v2-tillägg 0.13.7

- Ett problem med `targetPageParams` som ingår i mbox-begäranden. `targetPageParams` bör endast inkluderas i `pageLoad` förfrågningar.
- Korrigerade ett problem med globala dokument- och fönsterobjekt i taggtillägget genom att ersätta globala objektberoenden med direkta referenser till dem.
- Uppdaterat .js till 2.4.1.

## 25 januari 2021

### Adobe Target v2-tillägg 0.13.6

- Lägger till stöd för en enhetlig profil/plattform-ID för leverans-API customerIds
- Korrigerar ogiltig formattaggsinmatning
- Uppdaterat kl. 2.4.0
- Ett problem där odefinierade parametrar kan leda till felaktiga leveransbegäranden har åtgärdats

## 25 november 2020

### Adobe Target v2-tillägg 0.13.4

- Korrigerade ett fel där mbox-parametrar inte visades i användargränssnittet
- Varumärkesuppdateringar
- Version at.js har uppdaterats till 2.3.3

## 24 juli 2020

### Adobe Target v2-tillägg 0.13.3

- Korrigerade ett fel som orsakade att QA-lägeslänkar inte fungerade för inaktiva aktiviteter
- Korrigerade ett fel när tillägget misslyckas om ett skript eller en kod läggs till `default` egenskapen till `window` eller `document`

## 15 juni 2020

### Adobe Target v2-tillägg 0.13.2

- Ett problem har korrigerats när CNAME och kantåsidosättning användes, där at.js 1.x felaktigt kunde skapa serverdomänen, vilket gjorde att Target-begäran misslyckades
- Ett problem har korrigerats där Target fördröjde anropet från Analytics sendBeacon när v2-taggtillägget för Target och Adobe Analytics användes
- Förbättrade `deviceIdLifetime` genom att göra den åsidosättningsbar via `targetGlobalSettings`

## 25 mars 2020

### Adobe Target v2-tillägg 0.13.0

- Uppdaterat at.js till v2.3.
- Stöd för global Mbox-målmapp har lagts till i API:t adobe.target.getOffer
- Ett problem har korrigerats där parametrar och sidinläsningsparametrar inte bearbetades korrekt

## 10 oktober 2019

### Adobe Target v2-tillägg 0.12.0

- Uppdaterat at.js till v2.2.
- Förbättrade prestanda för integrering mellan Experience Cloud ID-bibliotek (ECID) v4.4 och at.js 2.2.
- Tidigare gjorde ECID-biblioteket två blockerande anrop innan at.js kunde hämta upplevelser. Detta har reducerats till ett enda samtal, vilket avsevärt förbättrar prestandan.

>[!NOTE]
>Uppgradera ditt ECID-taggtillägg till v4.4.1 om du vill utnyttja den här prestandaförbättringen.

## 31 juli 2019

### Adobe Target v2-tillägg 0.11.1

- Uppdaterad tilläggsversion som ska användas i .js 2.1.1
- En korrigering för hantering av parametrar har lagts till

## 3 juni 2019

### Adobe Target v2-tillägg 0.11.0

- Nytt taggtillägg som har stöd för at.js 2.1
