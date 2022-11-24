---
title: Versionsinformation om Adobe Target Extension
description: Den senaste versionsinformationen om taggtillägget Adobe Target i Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 3%

---

# Versionsinformation för Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

## 16 september 2021

### Adobe Target Extension 0.11.4

* Uppdaterat till at.js v1.8.3
* Tillagd `SameSite=None` och `Secure` attribut när cookies anges

## 24 juli 2020

### Adobe Target Extension 0.11.3

* Korrigerade ett fel när tillägget misslyckas om ett skript eller en kod läggs till `default` egenskapen till `window` eller `document`

## 15 juni 2020

### Adobe Target Extension 0.11.2

* Ett problem har korrigerats när CNAME och kantåsidosättning användes, där at.js 1.x felaktigt kunde skapa serverdomänen, vilket gjorde att Target-begäran misslyckades

## 25 mars 2020

### Adobe Target Extension 0.11.1

* Uppdaterat at.js till v1.8.1
* Ett problem har korrigerats där parametrar och sidinläsningsparametrar inte bearbetades korrekt

## 10 oktober 2019

### Adobe Target Extension 0.11.0

* Uppdaterat at.js till v1.8.
* Förbättrade prestanda för integrering mellan Experience Cloud ID-bibliotek (ECID) v4.4 och at.js 1.8.
* Tidigare gjorde ECID-biblioteket två blockerande anrop innan at.js kunde hämta upplevelser. Detta har reducerats till ett enda samtal, vilket avsevärt förbättrar prestandan.

>[!NOTE]
>Uppgradera ditt ECID-taggtillägg för Adobe Experience Platform till v4.4.1 om du vill utnyttja prestandaförbättringen.

## 31 juli 2019

### Adobe Target Extension 0.10.1

* Programfix för parametrar som hanterar taggtillägget för Adobe Target

## 4 maj 2019

### Adobe Target Extension 0.10.0

* Ett dataelementproblem som orsakades av de senaste Google Chrome-ändringarna har korrigerats

## 14 mars 2019

### Adobe Target Extension 0.9.3

* Uppdaterad tilläggsversion som ska användas i .js 1.7.1

## 20 februari 2019

### Adobe Target Extension 0.9.2

* Fasta konkurrensvillkor mellan Target- och Analytics-tillägg

## 12 februari 2019

### Adobe Target Extension 0.9.1

#### **Funktioner**

* Uppdaterat tillägg som ska använda at.js 1.7.0 med sekretessfunktioner som stöds via taggar för att styra hur och när Target-taggen utlöses. Läs taggdokumentationen om hur du konfigurerar din implementering av Opt-in. Möjligheten att anpassa har lagts till om en mbox-parameter som har ett tomt värde ska skickas till Target eller inte.

## 23 januari 2019

### Adobe Target Extension 0.8.4

* Uppdaterat at.js till version 1.6.4
* Gränssnittet för tillägg har migrerats till Adobe Spectrum

## 15 november 2018

### Adobe Target Extension 0.8.2

* Uppdaterat at.js till version 1.6.3

## 24 oktober 2018

### Adobe Target Extension 0.8.1

* Uppdaterat at.js till version 1.6.2

## 23 augusti 2018

### Adobe Target Extension 0.8.0

* Uppdaterat at.js till version 1.6.0

## 10 augusti 2018

### Adobe Target Extension 0.7.2

* Mindre ändringar
* Uppdaterade `exchangeUrl` -egenskapen i `extension.json` fil

## 1 augusti 2018

### Adobe Target Extension 0.7.1

* Mindre korrigeringar

## 18 juni 2018

### Adobe Target Extension 0.7.0

* Uppdaterad version av at.js till 1.5.0
* Ett problem där Media Optimizer genererade ett null-referensfel i IE 11 har korrigerats

## 15 juni 2018

### Adobe Target Extension 0.6.0

#### **Funktioner**

* Måltillägget har uppdaterats till att använda at.js v1.3.1. När du distribuerar Target med Analytics väntar vi nu tills alla Target-anrop har lösts (inklusive omdirigeringserbjudanden) innan Analytics utlöses, vilket löser det tidigare konkurrensvillkoret.

## 22 februari 2018

### Adobe Target Extension 0.4.1

#### **Funktioner**

* Adobe Exchange-listan har lagts till i extension.json
* Tillagda kontroller för att se om Target är inaktiverat och om Authoring är aktiverat

#### **Felkorrigeringar**

* Korrigerade ett fel i Adobe Target Extension som gjorde att Visual Experience Composer inte kunde visa sidan när den distribuerades via taggar.

## 8 februari 2018

### Adobe Target Extension 0.4.0

#### **Funktioner**

* Uppdaterade vyer i konfigurationsskärmar för tillägg
* at.js har uppdaterats till version 1.2.3 (har stöd för JSON-erbjudanden)
