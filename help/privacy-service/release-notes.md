---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Versionsinformation om Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Versionsinformation om Privacy Service

Det här dokumentet innehåller information om nya funktioner för Adobe Experience Platform Privacy Service samt förbättringar och viktiga felkorrigeringar.

>[!NOTE]
>
>Den senaste versionsinformationen för andra Experience Platform-tjänster finns [här](../release-notes/latest/latest.md).

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i Privacy Servicens användargränssnitt. Mer information finns i [användarhandboken](ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Omprofilering av Privacy Service | Den tidigare benämningen&quot;GDPR Service&quot; har ändrats till Privacy Service eftersom tjänsten har utvecklats för att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Bassökvägen för Privacy Service-API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Ny obligatorisk `regulation` egenskap | När du skapar nya jobb i Privacy Service-API:t måste en egenskap anges i nyttolasten för begäran för att ange vilken regel som jobbet ska spåras under. `regulation` Godkända värden är `gdpr` och `ccpa`. Mer information finns i dokumentet om [sekretessjobb](api/privacy-jobs.md) i Privacy Servicens utvecklarhandbok. |
| Stöd för Adobe Primetime-autentisering | Privacy Servicen godkänner nu begäranden om åtkomst/borttagning från Adobe Primetime Authentication, med `primetimeAuthentication` som produktvärde. Mer information finns i dokumentationen [för](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) Primetime-autentisering. |

### Förbättringar

* Förbättringar av användargränssnittet för Privacy Service:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Ny _regeltypsmeny_ för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begärandemått | Den nya mätinstrumentpanelen i Privacy Servicens användargränssnitt ger synlighet för inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att betjäna organisationer med både tekniska och icke-tekniska användare som skickar GDPR-förfrågningar har funktionen&quot;Skapa begäran&quot; lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i användargränssnittet för de Privacy Service som föredrar att fortsätta använda den. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts via individuella e-postmeddelanden, men GDPR-händelsemeddelanden är meddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. Privacy Servicens gränssnittsanvändare kan prenumerera på Adobe I/O GDPR-event för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 apr 2019

### Förbättringar

* Standardintervallet för statustabellen i Privacy Servicens användargränssnitt ändrat till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrade prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /` slutpunkten i Privacy Service-API:t.

## 11 apr 2019

### Förbättringar

* Uppdaterat användargränssnitt som stöder nya funktioner för betakunder
* Nytt metrics API som stöder UI 2.0-funktioner i beta

## 9 apr 2019

### Förbättringar

* Uppdaterade alla GET-API-anrop (lookup) till standardvärdet för ett 30-dagars uppslagsintervall
* Begränsad API-användning med ett maximalt uppslagsintervall på 45 dagar

## 14 februari 2019

### Förbättringar

* Tvinga fältet i varje `include` POST-överföring.
* Tvinga `include` fältet när JSON överförs.

### Felkorrigeringar

* Ett problem där Privacy Servicens användargränssnitt inte kunde läsas in har korrigerats.