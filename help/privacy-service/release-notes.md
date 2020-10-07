---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Versionsinformation om Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%

---


# [!DNL Privacy Service] versionsinformation

Det här dokumentet innehåller information om nya funktioner för Adobe Experience Platform [!DNL Privacy Service]samt förbättringar och viktiga felkorrigeringar.

>[!NOTE]
>
>Den senaste versionsinformationen för andra [!DNL Experience Platform] tjänster finns [här](../release-notes/latest/latest.md).

## 9 september 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för LGPD (Brasilien) | Privacy job can now be created under Brazil&#39;s [!DNL Lei Geral de Proteção de Dados] (LGPD) Regulation. Dessa jobb spåras enligt föreskriftskoden `lgpd_bra`. |

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | [!DNL Privacy] förfrågningar kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i [!DNL Privacy Service] användargränssnittet. Mer information finns i [användarhandboken](ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Privacy Service] omprofilering | Det tidigare namnet&quot;GDPR Service&quot; har ändrats till&quot;Service&quot; [!DNL Privacy Service] eftersom tjänsten har utvecklats för att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Bassökvägen för [!DNL Privacy Service] API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Ny obligatorisk `regulation` egenskap | När du skapar nya jobb i [!DNL Privacy Service] API måste en `regulation` egenskap anges i nyttolasten för begäran för att ange vilken regel som jobbet ska spåras under. Godkända värden är `gdpr` och `ccpa`. Mer information finns i dokumentet om [sekretessjobb](api/privacy-jobs.md) i [!DNL Privacy Service] utvecklarhandboken. |
| Stöd för Adobe Primetime-autentisering | [!DNL Privacy Service] godkänner nu begäranden om åtkomst/borttagning från Adobe Primetime Authentication, med `primetimeAuthentication` som produktvärde. Mer information finns i dokumentationen [för](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) Primetime-autentisering. |

### Förbättringar

* [!DNL Privacy Service] Förbättringar av användargränssnittet:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Ny *regeltypsmeny* för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begärandemått | Den nya mätinstrumentpanelen i [!DNL Privacy Service] användargränssnittet ger synlighet i inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att betjäna organisationer med både tekniska och icke-tekniska användare som skickar GDPR-förfrågningar har funktionen&quot;Skapa begäran&quot; lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i [!DNL Privacy Service] användargränssnittet för de organisationer som föredrar att fortsätta använda den. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts med hjälp av enskilda e-postmeddelanden är GDPR-händelsemeddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. [!DNL Privacy Service] UI-användare kan prenumerera på Adobe I/O GDPR-händelser för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 apr 2019

### Förbättringar

* Standardintervallet för statustabellen i [!DNL Privacy Service] användargränssnittet ändrat till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrade prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /` slutpunkten i [!DNL Privacy Service] API.

## 11 apr 2019

### Förbättringar

* Uppdaterat användargränssnitt som stöder nya funktioner för betakunder
* Nytt metrics API som stöder UI 2.0-funktioner i beta

## 9 apr 2019

### Förbättringar

* Uppdaterade alla API-anrop för sökning (GET) till standardvärdet för ett 30-dagars uppslagsintervall
* Begränsad API-användning med ett maximalt uppslagsintervall på 45 dagar

## 14 februari 2019

### Förbättringar

* Tvinga fram `include` fältet i varje POST som skickas.
* Tvinga `include` fältet när JSON överförs.

### Felkorrigeringar

* Ett problem där kunderna inte kunde läsa in [!DNL Privacy Service] gränssnittet har korrigerats.