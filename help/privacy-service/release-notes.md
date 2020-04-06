---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Versionsinformation om Integritetstjänst
topic: release notes
translation-type: tm+mt
source-git-commit: 682436b29df4696e98ef96fe5a65ab32221098ba

---


# Versionsinformation om Integritetstjänst

Det här dokumentet innehåller information om nya funktioner i Adobe Experience Platform Privacy Service, samt förbättringar och viktiga felkorrigeringar.

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i Sekretessgränssnittet. Mer information finns i [användarhandboken](ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Omprofilering av integritetstjänsten | Den tidigare benämningen&quot;GDPR-tjänsten&quot; har ändrats till Privacy Service eftersom tjänsten har utvecklats för att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Bassökvägen för sekretesstjänstens API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Ny obligatorisk `regulation` egenskap | När du skapar nya jobb i sekretesstjänstens API måste en `regulation` egenskap anges i nyttolasten för begäran för att ange vilken regel som ska spåra jobbet under. Godkända värden är `gdpr` och `ccpa`. Mer information finns i dokumentet om [sekretessjobb](api/privacy-jobs.md) i utvecklarhandboken för Integritetstjänst. |
| Stöd för Adobe Primetime-autentisering | Integritetstjänsten accepterar nu begäranden om åtkomst/borttagning från Adobe Primetime Authentication, med `primetimeAuthentication` som produktvärde. Mer information finns i dokumentationen [för](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) Primetime-autentisering. |

### Förbättringar

* Förbättringar av användargränssnittet för sekretesstjänster:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Ny _regeltypsmeny_ för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begärandemått | Den nya mätinstrumentpanelen i gränssnittet för sekretesstjänster ger synlighet för inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att betjäna organisationer med både tekniska och icke-tekniska användare som skickar GDPR-förfrågningar har funktionen&quot;Skapa begäran&quot; lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i integritetstjänstens gränssnitt för de organisationer som föredrar att fortsätta använda den. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts via individuella e-postmeddelanden, men GDPR-händelsemeddelanden är meddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. Användare av sekretessgränssnitt kan prenumerera på Adobe I/O GDPR-event för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 april 2019

### Förbättringar

* Standardintervallet för statustabellen i sekretessgränssnittet har ändrats till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrade prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /` slutpunkten i sekretesstjänstens API.

## 11 april 2019

### Förbättringar

* Uppdaterat användargränssnitt som stöder nya funktioner för betakunder
* Nytt metrics API som stöder UI 2.0-funktioner i beta

## 9 april 2019

### Förbättringar

* Uppdaterade alla GET-API-anrop (lookup) till standardvärdet för ett 30-dagars uppslagsintervall
* Begränsad API-användning med ett maximalt uppslagsintervall på 45 dagar

## 14 februari 2019

### Förbättringar

* Tvinga fältet i varje `include` POST-överföring.
* Tvinga `include` fältet när JSON överförs.

### Felkorrigeringar

* Ett problem har korrigerats där kunderna inte kunde läsa in användargränssnittet för sekretesstjänsten.