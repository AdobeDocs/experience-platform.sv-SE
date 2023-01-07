---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Versionsinformation om Privacy Service
description: Den senaste versionsinformationen för Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Versionsinformation om [!DNL Privacy Service]

Det här dokumentet innehåller information om nya funktioner för Adobe Experience Platform [!DNL Privacy Service], samt förbättringar och viktiga felkorrigeringar.

>[!NOTE]
>
>Den senaste versionsinformationen för andra [!DNL Experience Platform] tjänster kan hittas [här](../release-notes/latest/latest.md).

## 9 september 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för LGPD (Brasilien) | Integritetsjobb kan nu skapas i Brasilien [!DNL Lei Geral de Proteção de Dados] LGPD-regler. Dessa jobb spåras enligt regelkoden `lgpd_bra`. |

## 8 april 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | [!DNL Privacy] förfrågningar kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När sekretessförfrågningar görs i API:t `regulation` arrayen accepterar värdet &quot;pdpa_tha&quot;. |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i [!DNL Privacy Service] Gränssnitt. Se [användarhandbok](ui/user-guide.md) för mer information. |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

## 14 januari 2020

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Privacy Service] omprofilering | Det tidigare namnet&quot;GDPR Service&quot; har ändrats till [!DNL Privacy Service] eftersom tjänsten har växt till att stödja andra bestämmelser utöver GDPR. |
| Nya API-slutpunkter | Grundsökväg för [!DNL Privacy Service] API har uppdaterats från `/data/privacy/gdpr` till `/data/core/privacy/jobs` |
| Nytt krävs `regulation` property | När nya jobb skapas i [!DNL Privacy Service] API, en `regulation` egenskapen måste anges i nyttolasten för att ange vilken regel som ska gälla för att spåra jobbet under. Godkända värden är `gdpr` och `ccpa`. Visa dokumentet på [sekretessjobb](api/privacy-jobs.md) i [!DNL Privacy Service] API-guide för mer information. |
| Stöd för Adobe Primetime-autentisering | [!DNL Privacy Service] nu accepterar åtkomst-/borttagningsbegäranden från Adobe Primetime-autentisering med `primetimeAuthentication` som produktvärde. Se [Autentiseringsdokumentation för Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) för mer information. |

### Förbättringar

* [!DNL Privacy Service] Förbättringar av användargränssnittet:
   * Separata jobbspårningssidor för GDPR- och CCPA-regler.
   * Nytt *Regeltyp* för att växla mellan spårningsdata för GDPR och CCPA.

## 25 juli 2019

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Kontrollpanel för begärandemått | Den nya mätinstrumentpanelen i [!DNL Privacy Service] Gränssnittet ger synlighet i inskickade, felaktiga och slutförda GDPR-begäranden. |
| Request Builder | För att betjäna organisationer med både tekniska och icke-tekniska användare som skickar GDPR-förfrågningar har funktionen&quot;Skapa begäran&quot; lagts till i användargränssnittet. Funktionen för att skicka JSON-filer är fortfarande tillgänglig i [!DNL Privacy Service] Gränssnitt för de organisationer som föredrar att fortsätta använda det. |
| Meddelanden om GDPR-jobbhändelser | Händelsemeddelanden om GDPR-jobbstatus är viktiga för många arbetsflöden. Meddelanden som tidigare sänts med hjälp av enskilda e-postmeddelanden är GDPR-händelsemeddelanden som utnyttjar Adobe I/O-händelser, som skickas till en konfigurerad webkrok som underlättar automatisering av jobbförfrågningar. [!DNL Privacy Service] UI-användare kan prenumerera på Adobe I/O GDPR-händelser för att få uppdateringar när en produkt eller GDPR-jobbet har slutförts. |

## 18 apr 2019

### Förbättringar

* Standardintervall för statusregistret i [!DNL Privacy Service] Gränssnittet har ändrats till ett 7-dagarsintervall.
* Bättre intern undantagshantering.
* Förbättrade prestanda genom att införa cachelagring för vanliga interna anrop med låg dataförändringsfrekvens.

### Felkorrigeringar

* Lagt till loggningsinformation som saknas för filtrerade frågor för `GET /` slutpunkt i [!DNL Privacy Service] API.

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

* Tvinga `include` i varje POST.
* Tvinga `include` fält vid överföring av JSON.

### Felkorrigeringar

* Ett problem där kunderna inte kunde läsa in [!DNL Privacy Service] Gränssnitt.
