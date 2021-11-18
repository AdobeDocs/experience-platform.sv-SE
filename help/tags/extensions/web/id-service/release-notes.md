---
title: Versionsinformation för Adobe Experience Cloud Identity Service Extension
description: Den senaste versionsinformationen om taggtillägget Adobe Experience Cloud Identity Service i Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 1d3abede47c97c9a4f3b18ae25c890c309e942fd
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 4%

---

# Versionsinformation om Adobe Experience Cloud Identity Service-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Versionsinformation om själva identitetstjänsten för Experience Cloud och inte bara Adobe Experience Platform-taggtillägget finns här: [https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html)

## 3 nov 2021

### Experience Cloud ID-tillägg 5.2.1

#### **Funktioner**

* Den här korrigeringen innehåller en korrigering för att skriva cookies från en iFrame med attribut `SameSite=None` i webbläsaren Google Chrome.

## 12 jan 2021

### Experience Cloud ID Extension 5.2.0

#### **Funktioner**

* Det gick inte att uppdatera uppdateringen till VisitorJS 5.2.0 med en korrigering för ECID DataElement när du fick godkännande.

## 27 okt 2020

### Experience Cloud ID Extension 5.1.0

#### **Funktioner**

* Lägger till `sameSiteCookie` konfigurera för att ange `SameSite` attributet för `AMCV` cookie.
Denna konfiguration stöder följande värden för `SameSite` attribute:

   * `Strict`
   * `Lax`
   * `None`

Information om dessa attributvärden finns på [web.dev](https://web.dev/samesite-cookies-explained/) och [krom](https://www.chromium.org/updates/same-site)


## 13 augusti 2020

### Experience Cloud ID-tillägg 5.0.1

#### **Funktioner**

* Uppdaterar till korrigeringsfilen VisitorJS 5.0.1 med en korrigering för att lägga till d_cf-flaggan när IAB-medgivandesträngen har ändrats.

## 15 juni 2020

### Experience Cloud ID Extension 5.0.0

#### **Funktioner**

* Stöd för `IAB TCF` - Genomskinlighet och samtycke - `Version 2.0`.

## 13 april 2020

### Experience Cloud ID Extension 4.6.0

#### **Funktioner**

* Gjord `loadSSL` flagga som standard. Alla anrop till identitetstjänsten är aktiverade `https` som standard. Kunderna kan ställa in det på false om de vill anropa Identity Services på http från sina icke-ssl-sidor.
* Funktionen som används för att identifiera Internet-Explorer-versionen (IE) har uppdaterats för att åtgärda ett problem som rapporterats av ESLint.
* Felkorrigering för prestandaproblem i Internet-Explorer (IE) 11 när ECID ges optIn-förhandsgodkännande och uppdateras senare.

## 22 januari 2020

### Experience Cloud ID-tillägg 4.5.2

#### **Funktioner**

* Besökare.js har uppdaterats till 4.5.2
* Besökaren 4.5.1 innehåller en felkorrigering för IAB-plugin för Option
* Uppdaterat `setCustomerIDs` metod för att avvisa tomma ID:n som skickas.

## 7 januari 2020

### Experience Cloud ID-tillägg 4.4.2

#### **Funktioner**

* Besökare.js har uppdaterats till 4.4.2
* Förbättringar för `getVisitorValues` metod för att hämta värden snabbare


## 19 september 2019

### Experience Cloud ID-tillägg 4.4.1

#### **Funktioner**

* Besökare.js har uppdaterats till 4.4.1
* Korrigerat ett fel för hämtning av förauktoriserade indata för godkännande
* Namnet på VIDEO_ANALYTICS har ändrats till MEDIA_ANALYTICS i preOptInApprovals

   ![](../../../images/ecid-media-analytics.png)

## 17 juli 2019

### Experience Cloud ID Extension 4.4.0

#### **Funktioner**

* Besökare.js har uppdaterats till 4.4.0
* Stöd för SHA256-hashing för setCustomerID:n har lagts till

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 maj 2019

### Experience Cloud ID-tillägg 4.3.1

#### **Funktioner**

* Besökare.js har uppdaterats till 4.3
* Lagt till dataelementtyp för ECID som en del av taggtillägget

   ![](../../../images/ecid-data-element.png)

## 9 apr 2019

### Experience Cloud ID Extension 4.2.0

#### **Funktioner**

* Besökare.js har uppdaterats till 4.2, vilket inkluderade stöd för plugin-programmet Audience Manager IAB TCF

## 25 februari 2019

### Experience Cloud ID Extension 4.1.0

#### **Funktioner**

* visitor.js har uppdaterats till 4.1 som uppdaterade publishDestinations per ny API-ändring. Med den här uppdateringen kan sidans referensinformation visas under ID - synkronisera om så önskas.

## 15 februari 2019

### Experience Cloud ID Extension 4.0.0

#### **Funktioner**

* Besökare.js har uppdaterats till 4.0
* Ett konfigurationsalternativ för det nya inbyggda Opt-In-objektet har lagts till. Inställningarna kan användas för att undertrycka cookie- och beacon-anrop från Adobe Solutions för att bättre stödja bestämmelser som GDPR

   ![](../../../images/ext-mcid-opt-in.png)

## 20 mars 2018

### Experience Cloud ID-tillägg 3.1.0

#### **Funktioner**

* Besökare.js har uppdaterats till 3.1
* Lägger till två konfigurationsegenskaper: `resetBeforeVersion` och `serverState`
