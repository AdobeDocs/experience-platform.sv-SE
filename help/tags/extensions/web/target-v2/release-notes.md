---
title: Versionsinformation om Adobe Target v2-tillägget
description: Den senaste versionsinformationen om taggtillägget Adobe Target v2 i Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Versionsinformation om Adobe Target v2 Extension

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

## 19 maj 2021

### Adobe Target v2-tillägg 0.14.1

- Korrigera regression som introducerades i version 0.14 där Load Target-åtgärden utlöste globala mbox-anrop

## 14 maj 2021

### Adobe Target v2-tillägg 0.14

- Lagt till en ny åtgärd, Load Target med [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning), som läses in på .js 2.5 med On-Device Decisioning-funktioner
- Uppdaterat at.js till 2.5


## 25 mars 2021

### Adobe Target v2-tillägg 0.13.7

- Ett problem har korrigerats där `targetPageParams` inkluderades i mbox-begäranden. `targetPageParams` bör endast tas med i  `pageLoad` förfrågningar.
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
- Korrigerade ett fel när tillägget misslyckas om ett skript eller en kod lägger till egenskapen `default` i `window` eller `document`

## 15 juni 2020

### Adobe Target v2-tillägg 0.13.2

- Ett problem har korrigerats när CNAME och kantåsidosättning användes, där at.js 1.x felaktigt kunde skapa serverdomänen, vilket gjorde att Target-begäran misslyckades
- Ett problem har korrigerats där Target fördröjde anropet från Analytics sendBeacon när v2-taggtillägget för Target och Adobe Analytics användes
- Förbättrade `deviceIdLifetime`-inställningen genom att göra den åsidosättningsbar via `targetGlobalSettings`

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
