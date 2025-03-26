---
title: Bomborametod
description: Läs mer om Bombora Intent-källan på Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 39bbd9505b931b82aa925cba0bf8675f25dbf498
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 0%

---

# [!DNL Bombora Intent]

[!DNL Bombora] är en omfattande målgruppslösning som specialiserar sig på B2B-avsiktsdata. [!DNL Bombora Intent] är en Adobe Experience Platform-källa som du kan använda för att ansluta ditt [!DNL Bombora]-konto till Experience Platform och integrera dina kontoåtergivningsdata.

Med källan [!DNL Bombora Intent] kan du integrera [!DNL Bombora's] företagsdata för att identifiera konton som aktivt söker efter dina produkter eller tjänster. Använd [!DNL Bombora] om du vill prioritera marknadskonton för att skapa exakta segment och köra hyperriktade ABM-kampanjer, vilket säkerställer att era marknadsföringssatsningar fokuserar på de konton som mest sannolikt konverteras. Dessutom kan ni utnyttja intent-drivna strategier för att optimera annonskostnaderna, öka engagemanget och maximera avkastningen.

Läs det här dokumentet om du vill ha information om krav för källan [!DNL Bombora].

## Användningsfall {#use-cases}

Läs följande exempel på användningsexempel som du kan använda för källan [!DNL Bombora].

### Integrering med Demand-Side Platform (DSP)

Som B2B-marknadsförare kan du skapa en kontolista i Real-Time CDP, identifiera företag som visar hög återgivning för dina produkter och sedan aktivera den här listan i [!DNL Bombora], som integreras direkt med DSP:er, så att du kan köra riktade programmatiska annonskampanjer med [!DNL Bombora's]-data. Detta garanterar att era annonskostnader fokuserar på de företag som mest sannolikt konverterar.

### Account-Based Marketing (ABM)

Som B2B-marknadsförare kan du skapa en kontolista baserad på första och tredje parts avsiktssignaler. Du kan sedan aktivera den här listan i [!DNL Bombora], där ABM-funktioner gör att du kan rikta in dig på de här kontona specifikt, så att annonserna når beslutsfattare snarare än en bred publik.

### Aktivering av flerkanals-ABM

Som B2B-marknadsförare kan du skapa en kontolista i Real-Time CDP, identifiera företag med hög återgivning och aktivera den i [!DNL Bombora] för att köra riktade kampanjer i flera kanaler. På betalda sociala medier kan du leverera personaliserade annonser till proffs på målkonton på plattformar som [!DNL Linkedin] och [!DNL Facebook].

Med inbyggda annonsplattformar kan ni se till att ert innehåll når beslutsfattare i relevanta sammanhang. Ni kan även utöka kampanjer till avancerad TV och leverera annonser till viktiga konton. Detta flerkanaliga arbetssätt säkerställer enhetliga meddelanden på olika plattformar och maximerar engagemanget och konverteringsgraden.

## Förhandskrav {#prerequisites}

Läs igenom följande avsnitt för nödvändiga steg innan du ansluter [!DNL Bombora] till Experience Platform.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till i en tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress i tillåtelselista ](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Bombora]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/abac/ui/permissions.md).

### Namnbegränsningar för filer och kataloger

De begränsningar som anges nedan måste beaktas när du namnger molnlagringsfilen eller -katalogen:

* Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
* Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
* Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
* Följande tecken tillåts inte: `" \ / : | < > * ?`.
* Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

### Samla in nödvändiga inloggningsuppgifter

[!DNL Bombora] på Experience Platform är värd för [!DNL Google Cloud Storage]. För att autentisera ditt [!DNL Bombora]-konto måste du ange lämpliga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomstnyckel-ID | Åtkomstnyckel-ID för [!DNL Bombora]. Det här är en 61 tecken lång alfanumerisk sträng som krävs för att autentisera ditt konto för Experience Platform. |
| Nyckel för hemlig åtkomst | Den hemliga åtkomstnyckeln [!DNL Bombora]. Detta är en 40-siffrig, base-64-kodad sträng som krävs för att autentisera ditt konto för Experience Platform. |
| Buckennamn | Den [!DNL Bombora]-bucket från vilken data hämtas. |

Mer information om dessa autentiseringsuppgifter finns i handboken [[!DNL Google Cloud Storage] HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anvisningar om hur du skapar en egen åtkomstnyckel finns i guiden [Krav i  [!DNL Google Cloud Storage] källöversikten](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Bombora]-schema {#schema}

Läs det här avsnittet för information om schemat och datastrukturen för [!DNL Bombora].

Schemat [!DNL Bombora] kallas **kontoåtergivning varje vecka**. Det är information om avsikter varje vecka (anonym B2B-köparundersökning och innehållskonsumtion) för angivna konton och ämnen. Data är i parquetformat.

| Fältnamn | Datatyp | Obligatoriskt | Affärsnyckel | Anteckningar |
| --- | --- | --- | --- | --- |
| `Account_Name` | STRÄNG | TRUE | JA | Företagets kanoniska namn. |
| `Domain` | STRÄNG | TRUE | JA | Domänen för det identifierade konto som visar avsikt. |
| `Topic_Id` | STRÄNG | TRUE | JA | Ämne-ID för [!DNL Bombora]. |
| `Topic_Name` | STRÄNG | TRUE | | Ämnesnamnet [!DNL Bombora]. |
| `Cluster_Name` | STRÄNG | TRUE | | Klusternamnet på [!DNL Bombora] för ett visst ämne. |
| `Cluster_Id` | STRÄNG | TRUE | | Det kluster-ID som är associerat med ett visst ämne. |
| `Composite_Score` | INTEGER | TRUE | | Den sammansatta poängen representerar en domäns konsumtionsmönster för ett visst ämne under en viss tidsperiod. Den sammansatta poängen mäts mellan 0 och 100, där 100 representerar den högsta möjliga poängen och 0 den lägsta möjliga poängen. En sammansatt poäng på över 60 representerar en ökning av intresset för ett visst ämne av en domän. Detta kallas också för en &quot;ökning&quot;. |
| `Partition_Date` | DATUM | TRUE | | Kalenderdatum för en ögonblicksbild. Detta görs varje vecka i slutet av veckan i formatet `mm/dd/yyyy`. |

{style="table-layout:auto"}

>[!TIP]
>
>Alla ändringar i schemat meddelas Adobe i förväg. För att stödja sömlös schemautveckling är det viktigt att bibehålla bakåtkompatibiliteten. Experience Platform tillämpar en metod som bara har additiv versionshantering, vilket säkerställer att alla uppdateringar av schemat är icke-förstörande. Det innebär att ändringar som bryts inte tillåts alls, och endast ändringar som förbättrar eller utökar det befintliga schemat tillåts.

## Anslut ditt [!DNL Bombora]-konto till Experience Platform i användargränssnittet

När du är klar med konfigurationen av din förutsättning kan du läsa självstudiekursen om hur du [ansluter ditt [!DNL Bombora] konto till Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) för att starta integreringen.

## Vanliga frågor och svar {#faq}

I det här avsnittet finns svar på vanliga frågor om källan [!DNL Bombora].

### Måste jag ha ett befintligt kontrakt med [!DNL Bombora] för att kunna använda kontoavsiktsdata i Real-Time CDP B2B edition?

+++Svar

Ja, du måste ha ett aktivt kontrakt med [!DNL Bombora] för att få tillgång till och använda deras avsiktsdata i Experience Platform och Real-Time CDP B2B edition. Integreringen utnyttjar ditt befintliga avtal med [!DNL Bombora] för att importera och aktivera kontoavsiktssignaler i Experience Platform och Real-Time CDP.

+++

### Stöds anpassade fält från [!DNL Bombora] i den här integreringen?

+++Svar

För närvarande kan du bara använda [!DNL Bombora]-standardfält för inmatning och aktivering. Om du vill visa en lista över fält som stöds läser du [[!DNL Bombora] schemaguiden](#schema) för mer information om fälttillgänglighet.

+++

### Kan jag importera data från [!DNL Bombora] till Experience Platform på ad hoc-basis?

+++Svar

Ja, du kan importera data från [!DNL Bombora] på ad hoc-basis. Du kan skapa ett nytt dataflöde om du vill importera de senaste återgivningsdata, förutsatt att det finns nya data från [!DNL Bombora]. Du kan dock bara ha ett aktivt dataflöde åt gången. Se därför till att du tar bort det befintliga dataflödet innan du skapar ett nytt.

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

### Vilket fält används för att matcha konton från [!DNL Bombora] till Experience Platform?

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

Återgivningsdata kan användas i [målgrupper för konto](../../../segmentation/types/account-audiences.md) för att förbättra målgruppsanpassning, segmentering och personalisering. Genom att utnyttja avsiktssignaler kan företag identifiera och interagera med konton som visar ett stort intresse för specifika ämnen, optimera marknadsförings- och säljkontakten.

+++
