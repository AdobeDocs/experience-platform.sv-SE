---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Versionsinformation för sekretesstjänsten
description: De senaste versionsinformationen för Adobe Experience Platforms sekretesstjänst.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Versionsinformation om [!DNL Privacy Service]

Det här dokumentet innehåller information om nya funktioner för Adobe Experience Platform [!DNL Privacy Service]samt förbättringar och viktiga buggfixar.

>[!NOTE]
>
>Den senaste versionsinformationen för andra [!DNL Experience Platform]-tjänster finns [här](../release-notes/latest/latest.md).

## 9 september 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för LGPD (Brasilien) | Sekretessjobb kan nu skapas enligt Brasiliens [!DNL Lei Geral de Proteção de Dados] (LGPD)-reglering. Dessa jobb registreras under regelkoden `lgpd_bra`. |

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | [!DNL Privacy] förfrågningar kan nu skapas och spåras enligt PDPA (Personal Data Protection Act) i Thailand. När du gör sekretessförfrågningar i API:et accepterar `regulation`-matrisen värdet ”pdpa_tha”. |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnrymdstyper i Request Builder i användargränssnittet för [!DNL Privacy Service]. Mer information finns i [användarhandboken](ui/user-guide.md). |
| Borttagning av gammal slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Privacy Service] omprofilering | Det tidigare namnet ”GDPR-tjänsten” har ändrats till [!DNL Privacy Service] eftersom tjänsten har växt till att stödja andra bestämmelser förutom GDPR. |
| Nya API-slutpunkter | Bassökvägen för API:et [!DNL Privacy Service] har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Ny obligatorisk `regulation`-egenskap | När du skapar nya jobb i [!DNL Privacy Service]-API:et måste en `regulation`-egenskap anges i nyttolasten för förfrågan för att ange vilken regel som jobbet ska spåras under. Godkända värden är `gdpr` och `ccpa`. Mer information finns i dokumentet om [sekretessjobb](api/privacy-jobs.md) i API-handboken för [!DNL Privacy Service]. |
| Stöd för Adobe Primetime-autentisering | [!DNL Privacy Service] accepterar nu begäranden om åtkomst/borttagning från Adobe Primetime-autentisering, med `primetimeAuthentication` som produktvärde. Se [Primetime Authentication-dokumentationen](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) för mer information. |

### Förbättringar

* [!DNL Privacy Service]-gränssnittsförbättringar:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Ny rullgardinsmeny för *Regeltyp* för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begäran om mätvärden | Den nya mätinstrumentpanelen i användargränssnittet [!DNL Privacy Service] ger synlighet för inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att hjälpa organisationer med både tekniska och icke-tekniska användare som skickar in GDPR-begäranden har en ”Skapa begäran”-funktion lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i användargränssnittet för [!DNL Privacy Service] för de organisationer som föredrar att fortsätta använda den. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts med hjälp av enskilda e-postmeddelanden är GDPR-händelsemeddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. [!DNL Privacy Service] gränssnittsanvändare kan prenumerera på Adobe I/O GDPR-händelser för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 april 2019

### Förbättringar

* Standardintervallet för statustabellen i användargränssnittet för [!DNL Privacy Service] har ändrats till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrad prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /`-slutpunkten i [!DNL Privacy Service]-API:et.

## 11 april 2019

### Förbättringar

* Uppdaterat användargränssnitt som stöder nya funktioner för betakunder
* Nytt API för mätvärden med stöd för UI 2.0-funktioner i betaversion

## 9 april 2019

### Förbättringar

* Uppdaterade alla API-anrop för sökning (GET) till standardvärdet för ett 30-dagars uppslagsintervall
* Begränsad API-användning med ett maximalt uppslagsintervall på 45 dagar

## 14 februari 2019

### Förbättringar

* Tvinga fältet `include` vid varje POST som skickas.
* Tvinga fältet `include` när JSON överförs.

### Felkorrigeringar

* Ett problem där kunder inte kunde läsa in användargränssnittet för [!DNL Privacy Service] har korrigerats.
