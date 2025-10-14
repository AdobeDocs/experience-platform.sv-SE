---
title: Demandbase-metod
description: Läs mer om Demandbase Intent-källan på Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: 8a5fdcfcf503df1b9d5aa338ff530181a2d03b5d
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] är en kontobaserad marknadsföringsplattform som du kan använda för B2B-försäljning och marknadsföring. [!DNL Demandbase Intent] är en Adobe Experience Platform-källa som du kan använda för att ansluta ditt [!DNL Demandbase]-konto till Experience Platform och integrera dina kontoåtergivningsdata.

Med källan [!DNL Demandbase] kan du identifiera intressevärda konton baserat på realtidsengagemang. Genom att prioritera de starkaste avsiktssignalerna kan ni skapa exakta segment och leverera hyperriktade kampanjer, så att era marknadsföringssatsningar fokuserar på de konton som mest sannolikt konverteras. Genom att aktivera intent-drivna strategier kan ni optimera annonskostnaderna, öka engagemanget och få högre avkastning.

Läs det här dokumentet om du vill ha information om krav för källan [!DNL Demandbase].

## Förhandskrav {#prerequisites}

Läs igenom följande avsnitt för nödvändiga steg innan du ansluter [!DNL Demandbase] till Experience Platform.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till i en tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress i tillåtelselista &#x200B;](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Demandbase]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/abac/ui/permissions.md).

### Namnbegränsningar för filer och kataloger

De begränsningar som anges nedan måste beaktas när du namnger molnlagringsfilen eller -katalogen:

* Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
* Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
* Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
* Följande tecken tillåts inte: `" \ / : | < > * ?`.
* Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

### Samla in nödvändiga inloggningsuppgifter

[!DNL Demandbase] på Experience Platform är värd för [!DNL Google Cloud Storage]. För att autentisera ditt [!DNL Demandbase]-konto måste du ange lämpliga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomstnyckel-ID | Åtkomstnyckel-ID för [!DNL Demandbase]. Det här är en 61 tecken lång alfanumerisk sträng som krävs för att autentisera ditt konto för Experience Platform. |
| Nyckel för hemlig åtkomst | Den hemliga åtkomstnyckeln [!DNL Demandbase]. Detta är en 40-siffrig, base-64-kodad sträng som krävs för att autentisera ditt konto för Experience Platform. |
| Buckennamn | Den [!DNL Demandbase]-bucket från vilken data hämtas. |
| Mappsökväg | Sökvägen till mappen som du vill ge åtkomst till. |

Mer information om dessa autentiseringsuppgifter finns i handboken [[!DNL Google Cloud Storage] HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anvisningar om hur du skapar en egen åtkomstnyckel finns i guiden [Krav i  [!DNL Google Cloud Storage] källöversikten](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Demandbase]-schema

Läs det här avsnittet för information om schemat och datastrukturen för [!DNL Demandbase].

Schemat [!DNL Demandbase] kallas **B2B Demandbase-kontoåtergivning**. Det är veckovis information om avsikter (anonym B2B-köparundersökning och innehållskonsumtion) för angivna konton och nyckelord. Data är i parquetformat.

* Klass - XDM [!DNL Demandbase Account Intent]
* Namnutrymme - B2B [!DNL Demandbase Account Intent]
* Primär identitet - `intentID`
* Relationer - B2B-konto

| Fältnamn | Datatyp | Beskrivning |
|--------------------------|-----------|-------------------------------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJEKT | Det här fältet innehåller systemgranskningsinformation från den externa källan. |
| `_id` | STRÄNG | Detta är den unika systemidentifieraren för posten. |
| `accountDomain` | STRÄNG | Det här fältet innehåller kontodomänen. |
| `accountID` | STRÄNG | Detta är det B2B-konto-ID som den här intent-posten är associerad med. |
| `demandbaseAccountID` | STRÄNG | Det här är företagets ID i [!DNL Demandbase]. |
| `durationType` | STRÄNG | I det här fältet anges typen av giltighetsperiod, t.ex. &quot;vecka&quot;. |
| `endDate` | DATUM | Detta är slutdatumet för den ingående giltighetsperioden. |
| `intentID` | STRÄNG | Detta är ett systemgenererat unikt värde för intent-posten. |
| `intentStrength` | STRÄNG | I det här fältet anges typen av giltighetsperiod, t.ex. &quot;DAY&quot;, &quot;WEEK&quot; eller &quot;MONTH&quot;. |
| `isTrending` | BOOLEAN | Det här fältet anger om nyckelordet är trendmässigt, med möjliga värden låg, Medium eller hög. |
| `keyword` | STRÄNG | Det här fältet innehåller nyckelordet eller frasen som anger metod från [!DNL Demandbase]. |
| `keywordSetID` | STRÄNG | Detta är identifieraren för nyckelordsuppsättningen. |
| `keywordSetName` | STRÄNG | Det här är namnet på nyckelordsuppsättningen. |
| `numTrendingDays` | INTEGER | I det här fältet anges antalet dagar som nyckelordet har trendats. |
| `partitionDate` | DATUM | Detta är partitionsdatumet för posten. |
| `peopleResearchingCount` | INTEGER | I det här fältet visas antalet personer som söker efter nyckelordet. |
| `startDate` | DATUM | Detta är startdatumet för den ingående giltighetsperioden. |
| `trendingScore` | INTEGER | Det här fältet innehåller trendspåret för nyckelordet. |

{style="table-layout:auto"}

>[!TIP]
>
>Alla ändringar i schemat meddelas Adobe i förväg. För att stödja sömlös schemautveckling är det viktigt att bibehålla bakåtkompatibiliteten. Experience Platform tillämpar en metod som bara har additiv versionshantering, vilket säkerställer att alla uppdateringar av schemat är icke-förstörande. Det innebär att ändringar som bryts inte tillåts alls, och endast ändringar som förbättrar eller utökar det befintliga schemat tillåts.

## Anslut ditt [!DNL Demandbase]-konto till Experience Platform i användargränssnittet

När du är klar med konfigurationen av din förutsättning kan du läsa självstudiekursen om hur du [ansluter ditt [!DNL Demandbase] konto till Experience Platform](../../tutorials/ui/create/data-partners/demandbase.md) för att starta integreringen.

## Vanliga frågor och svar {#faq}

I det här avsnittet finns svar på vanliga frågor om källan [!DNL Demandbase].

### Måste jag ha ett befintligt kontrakt med [!DNL Demandbase] för att kunna använda kontoavsiktsdata i Real-Time CDP B2B edition?

+++Svar

Ja, du måste ha ett aktivt kontrakt med [!DNL Demandbase] för att få tillgång till och använda deras avsiktsdata i Experience Platform och Real-Time CDP B2B edition. Integreringen utnyttjar ditt befintliga avtal med [!DNL Demandbase] för att importera och aktivera kontoavsiktssignaler i Experience Platform och Real-Time CDP.

+++

### Stöds anpassade fält från [!DNL Demandbase] i den här integreringen?

+++Svar

För närvarande kan du bara använda [!DNL Demandbase]-standardfält för inmatning och aktivering. Om du vill visa en lista över fält som stöds läser du [[!DNL Demandbase] schemaguiden](#schema) för mer information om fälttillgänglighet.

+++

### Kan jag importera data från [!DNL Demandbase] till Experience Platform på ad hoc-basis?

+++Svar

Ja, du kan importera data från [!DNL Demandbase] på ad hoc-basis. Du kan skapa ett nytt dataflöde om du vill importera de senaste återgivningsdata, förutsatt att det finns nya data från [!DNL Demandbase]. Du kan dock bara ha ett aktivt dataflöde åt gången. Se därför till att du tar bort det befintliga dataflödet innan du skapar ett nytt.

+++

### Vilken är valideringsprocessen för återgivna data och hur kan jag kontrollera vilka återgivningsdata som är länkade till ett visst konto?

+++Svar

Använd [Adobe Experience Platform Query Service](../../../query-service/home.md) av AccountID om du vill validera intent data och avgöra vilka intent-signaler som är kopplade till specifika konton.

+++

### Hur hittar jag en metod för ett visst företag?

+++Svar

Kör en SQL-fråga i [frågetjänsten](../../../query-service/home.md) om du vill söka efter avsiktsdata med företagsnamnet eller konto-ID:t. Om du vill visa alla intent-data för ett visst företag kan du köra en SQL-fråga i Query Service med företagsnamnet eller konto-ID för att hämta alla associerade intent-signaler.

+++


### Jag hittade ett problem med kontomatchningen i Experience Platform, vad ska jag göra?

+++Svar

Upplösningen beror på det specifika problemet:

* **Felaktig eller saknad företagsdomän i Experience Platform**: Om felet beror på ett felaktigt företagsdomänvärde i kontoinformationen måste du uppdatera företagsdomänfältet i Experience Platform för att säkerställa korrekt matchning.
* **Felaktig fältmappning i dataflöde**: Om felet beror på en felaktig sökväg till företagsdomänfält i dataflödet uppdaterar du dataflödeskonfigurationen så att den refererar till rätt fältsökväg.

+++

### Hur tar jag bort avsiktsdata i Experience Platform?

+++Svar

Du måste [ta bort datauppsättningen](../../../catalog/datasets/user-guide.md#delete-a-dataset) för att kunna ta bort avsiktsdata i Experience Platform.

+++

### Vilket fält används för att matcha konton från [!DNL Demandbase] till Experience Platform?

+++Svar

Fältet `accountOrganization.domain` används för att matcha konton. Om din organisation använder ett annat anpassat fält för att lagra webbplatsnamnet måste du ange rätt fältsökväg för korrekt mappning.

+++

### Vad händer när en företagsdomän uppdateras i Experience Platform?

+++Svar

När en företagsdomän uppdateras tillämpas det nya domänvärdet i nästa dataflödeskörning. Detta säkerställer att

* I framtida intent data-import används den uppdaterade domänen för kontomatchning.
* Tidigare felmatchade intent-signaler kan nu justeras korrekt mot det avsedda kontot.
* Inga retroaktiva ändringar görs i tidigare inkapslade data. Nya och inkommande data speglar uppdateringen.

+++

### Vad är domänmatchningsprocessen?

+++Svar

Domänmatchning i Experience Platform baseras på en exakt matchning av det rensade domänfältets värde. Experience Platform tar automatiskt bort prefix (t.ex. https:/<span>/www.) och behåller domänen på den översta nivån (t.ex. adobe.com). Matchning kräver ett exakt domänvärde, utan stöd för luddig matchning eller underdomäner.

+++

### Var kan jag använda avsiktsdata?

+++Svar

Återgivningsdata kan användas i [målgrupper för konto](../../../segmentation/types/account-audiences.md) för att förbättra målgruppsanpassning, segmentering och personalisering. Genom att utnyttja avsiktssignaler kan företag identifiera och interagera med konton som visar ett stort intresse för specifika ämnen, optimera marknadsförings- och säljkontakten

+++
