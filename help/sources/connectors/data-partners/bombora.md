---
title: Bombora avsikt
description: Lär dig mer om Bombora Intent-källan på Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 9ab2c4725d2188f772bde1f7a89db2bb47c7a46b
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 0%

---

# [!DNL Bombora Intent]

[!DNL Bombora] är en omfattande målgruppslösning som specialiserar sig på B2B-avsiktsdata. [!DNL Bombora Intent] är en Adobe Experience Platform-källa som du kan använda för att ansluta ditt [!DNL Bombora] konto till Experience Platform och integrera dina kontots avsiktsdata.

Med källan [!DNL Bombora Intent] kan du integrera [!DNL Bombora's] företagsdata för att identifiera konton som aktivt söker efter dina produkter eller tjänster. Använd [!DNL Bombora] om du vill prioritera marknadskonton för att skapa exakta segment och köra hyperriktade ABM-kampanjer, vilket säkerställer att era marknadsföringssatsningar fokuserar på de konton som mest sannolikt konverteras. Dessutom kan ni utnyttja intent-drivna strategier för att optimera annonskostnaderna, öka engagemanget och maximera avkastningen.

Läs det här dokumentet om du vill ha information om krav för källan [!DNL Bombora].

## Användningsfall {#use-cases}

Läs följande exempel på användningsexempel som du kan använda för källan [!DNL Bombora].

### Integrering med DSP (Demand-Side Platform)

Som B2B-marknadsförare kan du skapa en kontolista i Real-Time CDP, identifiera företag som visar hög återgivning för dina produkter och sedan aktivera den här listan i [!DNL Bombora], som integreras direkt med DSP:er, så att du kan köra riktade programmatiska annonskampanjer med [!DNL Bombora's]-data. Detta säkerställer att dina annonsutgifter är fokuserade på företag som mest sannolikt kommer att konvertera.

### Account-Based Marketing (ABM)

Som B2B-marknadsförare kan du skapa en kontolista baserad på första och tredje parts avsiktssignaler. Du kan sedan aktivera den här listan i [!DNL Bombora], där ABM-funktioner gör att du kan rikta in dig på de här kontona specifikt, så att annonserna når beslutsfattare snarare än en bred publik.

### Aktivering av flerkanals-ABM

Som B2B-marknadsförare kan du skapa en kontolista i Real-Time CDP, identifiera företag med hög återgivning och aktivera den i [!DNL Bombora] för att köra riktade kampanjer i flera kanaler. På betalda sociala medier kan du visa personliga annonser till proffs på målkonton på plattformar som [!DNL Linkedin] och [!DNL Facebook].

Med hjälp av inbyggda annonsplattformar kan du se till att ditt innehåll når beslutsfattare i relevanta sammanhang. Du kan också utöka kampanjer till avancerad TV och leverera annonser till nyckelkonton. Detta flerkanalstillvägagångssätt säkerställer konsekventa meddelanden på alla plattformar, vilket maximerar engagemang och konverteringsfrekvenser.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för nödvändiga steg innan du ansluter [!DNL Bombora] till Experience Platform.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till i en tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress i tillåtelselista ](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Bombora]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i användargränssnittsguiden [&#128279;](../../../access-control/abac/ui/permissions.md)för åtkomstkontroll.

### Namngivningsbegränsningar för filer och kataloger

Begränsningarna som anges nedan måste beaktas när du namnger din molnlagringsfil eller katalog:

* Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
* Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
* Följande reserverade URL-tecken måste vara korrekt undantagna: `! ' ( ) ; @ & = + $ , % # [ ]`
* Följande tecken är inte tillåtna: `" \ / : | < > * ?`.
* Ogiltiga tecken för URL-sökvägar är inte tillåtna. Kodpunkter som `\uE000`, även om de är giltiga i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom är vissa ASCII- eller Unicode-tecken, till exempel kontrolltecken (0x00 till 0x1F, \u0081 osv.), inte heller tillåtna. Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundläggande regler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (..).

### Samla in nödvändiga autentiseringsuppgifter

[!DNL Bombora] på Experience Platform drivs av [!DNL Google Cloud Storage]. För att kunna autentisera ditt [!DNL Bombora] konto måste du ange lämpliga värden för följande autentiseringsuppgifter:

| Referens | Beskrivning |
| --- | --- |
| ID för åtkomstnyckel | Åtkomstnyckel-ID för [!DNL Bombora]. Det här är en alfanumerisk sträng på 61 tecken som krävs för att autentisera ditt konto till Experience Platform. |
| Nyckel för hemlig åtkomst | Den hemliga åtkomstnyckeln [!DNL Bombora] . Det här är en 40-teckens, base-64-kodad sträng som krävs för att autentisera ditt konto till Experience Platform. |
| Namn på bucket | Bucketen [!DNL Bombora] som data ska hämtas från. |

Mer information om dessa autentiseringsuppgifter finns i guiden[&#128279;](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) för [!DNL Google Cloud Storage] HMAC-nycklar. Anvisningar om hur du skapar en egen åtkomstnyckel finns [i kravguiden i källöversikten [!DNL Google Cloud Storage] ](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## [!DNL Bombora] Schemat {#schema}

Läs det här avsnittet om du vill ha information om schemat och datastrukturen [!DNL Bombora] .

Schemat [!DNL Bombora] kallas **Account Intent Weekly**. Det är den veckovisa avsiktsinformationen (anonym B2B-köparundersökning och innehållskonsumtion) om angivna konton och ämnen. Data är i parquet-format.

| Fältnamn | Datatyp | Krävs | Nyckel för företag | Anteckningar |
| --- | --- | --- | --- | --- |
| `Account_Name` | STRÄNG | TRUE | JA | Företagets kanoniska namn. |
| `Domain` | STRÄNG | SANN | JA | Domänen för det identifierade konto som visar avsikt. |
| `Topic_Id` | STRÄNG | TRUE | JA | Ämnes-ID [!DNL Bombora] . |
| `Topic_Name` | STRÄNG | TRUE | | Ämnesnamnet [!DNL Bombora]. |
| `Cluster_Name` | STRÄNG | TRUE | | Klusternamnet på [!DNL Bombora] för ett visst ämne. |
| `Cluster_Id` | STRÄNG | SANN | | Kluster-ID:t som är associerat med ett visst ämne. |
| `Composite_Score` | HELTAL | TRUE | | Den sammansatta poängen representerar en domäns konsumtionsmönster för ett visst ämne under en viss tidsperiod. Den sammansatta poängen mäts mellan 0 och 100, där 100 representerar den högsta möjliga poängen och 0 den lägsta möjliga poängen. En sammansatt poäng på över 60 representerar en ökning av intresset för ett visst ämne av en domän. Detta kallas också för en &quot;ökning&quot;. |
| `Partition_Date` | DATUM | TRUE | | Kalenderdatumet för en ögonblicksbild. Detta görs varje vecka, i slutet av veckan, i `mm/dd/yyyy` format. |

{style="table-layout:auto"}

>[!TIP]
>
>Alla ändringar i schemat meddelas Adobe i förväg. För att stödja sömlös schemautveckling är det viktigt att bibehålla bakåtkompatibiliteten. Experience Platform tillämpar en metod som bara har additiv versionshantering, vilket säkerställer att alla uppdateringar av schemat är icke-förstörande. Det innebär att ändringar som bryts inte tillåts alls, och endast ändringar som förbättrar eller utökar det befintliga schemat tillåts.

## Anslut ditt [!DNL Bombora]-konto till Experience Platform i användargränssnittet

När du är klar med konfigurationen av din förutsättning kan du läsa självstudiekursen om hur du [ansluter ditt [!DNL Bombora] konto till Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) för att starta integreringen.

## Vanliga frågor och svar {#faq}

I det här avsnittet finns svar på vanliga frågor om källan [!DNL Bombora].

### Måste jag ha ett befintligt avtal med [!DNL Bombora] för att få använda deras kontoavsiktsdata i Real-Time CDP B2B Edition?

+++Svar

Ja, du måste ha ett aktivt avtal med [!DNL Bombora] dem för att få tillgång till och använda deras avsiktsdata i Experience Platform och Real-Time CDP B2B Edition. Integreringen utnyttjar ditt befintliga avtal för [!DNL Bombora] att importera och aktivera signaler för kontoavsikt i Experience Platform och Real-Time CDP.

+++

### Stöds anpassade fält från [!DNL Bombora] i den här integreringen?

+++Svar

För närvarande kan du bara använda [!DNL Bombora]-standardfält för inmatning och aktivering. Om du vill visa en lista över fält som stöds läser du [[!DNL Bombora] schemaguiden](#schema) för mer information om fälttillgänglighet.

+++

### Kan jag importera data från [!DNL Bombora] till Experience Platform på ad hoc-basis?

+++Svar

Ja, du kan mata in data från [!DNL Bombora] ad hoc. Du kan skapa ett nytt dataflöde för att importera de senaste avsiktsdata, så länge det finns nya data från [!DNL Bombora]. Du kan dock bara ha ett aktivt dataflöde i taget. Se därför till att du tar bort det befintliga dataflödet innan du skapar ett nytt.

+++

### Hur ser valideringsprocessen ut för avsiktsdata och hur kan jag kontrollera vilka avsiktsdata som är länkade till ett visst konto?

+++Svar

Använd [Adobe Experience Platform Query Service](../../../query-service/home.md) av AccountID om du vill validera intent data och avgöra vilka intent-signaler som är kopplade till specifika konton.

+++

### Hur kan jag slå upp en avsikt för ett specifikt företag?

+++Svar

Kör en SQL-fråga i [Query Service](../../../query-service/home.md) för att söka efter avsiktsdata med hjälp av företagsnamnet eller AccountID. Om du vill visa alla avsiktsdata för ett visst företag kan du köra en SQL-fråga i Query Service med hjälp av företagsnamnet eller AccountID för att hämta alla associerade avsiktssignaler.

+++


### Jag hittade ett problem med kontomatchningsprocessen i Experience Platform, vad ska jag göra?

+++Svar

Lösningen beror på den specifika frågan:

* **Felaktig eller saknad företagsdomän i Experience Platform**: Om problemet beror på ett felaktigt företagsdomänvärde i kontodata uppdaterar du fältet för företagsdomän i Experience Platform för att säkerställa korrekt matchning.
* **Felaktig fältmappning i dataflödet**: Om problemet beror på en felaktig fältsökväg för företagsdomänen i dataflödet uppdaterar du dataflödeskonfigurationen så att den refererar till rätt fältsökväg.

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

Återgivningsdata kan användas i [målgrupper för konto](../../../segmentation/types/account-audiences.md) för att förbättra målgruppsanpassning, segmentering och personalisering. Genom att utnyttja avsiktssignaler kan företag identifiera och engagera sig med konton som visar stort intresse för specifika ämnen, vilket optimerar marknadsföring och försäljningsuppsökande verksamhet.

+++
