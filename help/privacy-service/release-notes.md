---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Versionsinformation om Privacy Service
description: Den senaste versionsinformationen för Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Versionsinformation om [!DNL Privacy Service]

Det här dokumentet innehåller information om nya funktioner för Adobe Experience Platform [!DNL Privacy Service] samt förbättringar och viktiga felkorrigeringar.

>[!NOTE]
>
>Den senaste versionsinformationen för andra [!DNL Experience Platform]-tjänster finns [här](../release-notes/latest/latest.md).

## 9 september 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för LGPD (Brasilien) | Sekretessjobb kan nu skapas enligt Brasiliens [!DNL Lei Geral de Proteção de Dados]-regel (LGPD). Dessa jobb spåras under regelkoden `lgpd_bra`. |

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | [!DNL Privacy] begäranden kan nu skapas och spåras under Personal Data Protection Act (PDPA) i Thailand. När sekretessbegäranden görs i API:t godkänner arrayen `regulation` värdet &quot;pdpa_tha&quot;. |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i användargränssnittet för [!DNL Privacy Service]. Mer information finns i [användarhandboken](ui/user-guide.md). |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Privacy Service] omprofilering | Det tidigare namnet&quot;GDPR-tjänsten&quot; har ändrats till [!DNL Privacy Service] eftersom tjänsten har växt till att stödja andra bestämmelser förutom GDPR. |
| Nya API-slutpunkter | Bassökvägen för API:t [!DNL Privacy Service] har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Ny obligatorisk `regulation`-egenskap | När du skapar nya jobb i [!DNL Privacy Service]-API:t måste en `regulation`-egenskap anges i nyttolasten för begäran för att ange vilken regel som jobbet ska spåras under. Godkända värden är `gdpr` och `ccpa`. Mer information finns i dokumentet om [sekretessjobb](api/privacy-jobs.md) i API-handboken för [!DNL Privacy Service]. |
| Stöd för Adobe Primetime-autentisering | [!DNL Privacy Service] accepterar nu begäranden om åtkomst/borttagning från Adobe Primetime-autentisering, med `primetimeAuthentication` som produktvärde. Mer information finns i [dokumentationen för Primetime-autentisering](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Förbättringar

* [!DNL Privacy Service]-gränssnittsförbättringar:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Ny *Regeltyp*-listruta för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begärandemått | Den nya mätinstrumentpanelen i användargränssnittet [!DNL Privacy Service] ger synlighet för inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att betjäna organisationer med både tekniska och icke-tekniska användare som skickar GDPR-förfrågningar har funktionen&quot;Skapa begäran&quot; lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i användargränssnittet för [!DNL Privacy Service] för de organisationer som föredrar att fortsätta använda den. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts med hjälp av enskilda e-postmeddelanden är GDPR-händelsemeddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. [!DNL Privacy Service] gränssnittsanvändare kan prenumerera på Adobe I/O GDPR-händelser för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 april 2019

### Förbättringar

* Standardintervallet för statustabellen i användargränssnittet för [!DNL Privacy Service] har ändrats till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrade prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /`-slutpunkten i [!DNL Privacy Service]-API:t.

## 11 april 2019

### Förbättringar

* Uppdaterat användargränssnitt som stöder nya funktioner för betakunder
* Nytt metrics API som stöder UI 2.0-funktioner i beta

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
