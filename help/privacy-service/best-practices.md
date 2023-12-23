---
title: Bästa tillvägagångssätt för Privacy Service
description: Lär dig hur du kan minska behandlingstiden och kostnaderna för din organisation när du slutför sekretessförfrågningar genom att följa dessa riktlinjer för optimal användning.
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Bästa tillvägagångssätt för Privacy Service

Använd Privacy Service för att automatisera regelefterlevnaden för datasekretess när kunderna vill få tillgång till eller ta bort sina personuppgifter från era datalager. Privacy Servicen erbjuder ett RESTful-API och användargränssnitt för att skicka in begäran om åtkomst och borttagning av kunddata mellan olika Adobe Experience Cloud-program.

I den här guiden beskrivs de bästa sätten att effektivt behandla sekretessförfrågningar och optimera svarstiderna vid slutförande när kunddataförfrågningar hanteras.

## Komma igång {#getting-started}

Den här guiden kräver en fungerande förståelse av [Privacy Service](./home.md) och hur det gör det möjligt att hantera förfrågningar från registrerade (kunder) i olika Adobe Experience Cloud-program. Du bör också läsa guiden på [skapa en begäran om sekretessjobb i användargränssnittet](./ui/user-guide.md#create-a-new-privacy-job-request) eller [API](./api/overview.md)och förstå hur du utför dessa åtgärder programmatiskt.

## Förutsättningar {#prerequisites}

Åtkomsten till Adobe Experience Platform Privacy Service regleras genom detaljerade rollbaserade behörigheter i Adobe Admin Console. Du behöver de behörigheter som krävs i en produktprofil för att kunna använda vissa funktioner i Privacy Servicens användargränssnitt och API. Kontakta systemadministratören om du behöver ytterligare behörigheter.

Administratörer kan se guiden på [hantera behörigheter för Privacy Service](./permissions.md) för mer information.

## Riktlinjer för att skapa sekretessjobb {#creation-guidelines}

Om du vill effektivisera behandlingen av begäranden och förbättra svarstiderna bör du följa nedanstående riktlinjer när du skapar sekretessjobb. Detta gäller både API- och gränssnittsmetoderna.

1. **Maximera antalet registrerade per begäran:** Inkludera så många registrerade som möjligt, upp till 1 000, per begäran.
2. **Grupp-ID för effektivitet:** Gruppera flera ID:n för en enskild registrerade (upp till nio) i varje begäran. The **ID:n kan komma från olika Adobe-tjänster i samma begäran**.
3. **Kombinera åtkomst- och borttagningsjobb:** Inkludera båda jobbtyperna &quot;access&quot; och &quot;delete&quot; i en enda begäran om det behövs av den registrerade.
4. **Inkludera endast nödvändiga produkter:** Inkludera endast produkter som är obligatoriska eller licensierade. Ytterligare produkter kan förkorta bearbetningstiden och öka kostnaderna.

## Övervaka sekretessjobbstatus {#monitor-status}

För att effektivt kunna övervaka sekretessjobb och kontrollera deras status finns det tre metoder i Privacy Servicen. De metoder som är tillgängliga anges nedan i den ordning som effektiviteten och produktiviteten övervakas. Varje metod innehåller riktlinjer för god praxis för att förbättra din upplevelse, följt av ett idealiskt scenario som kombinerar alla metoder.

### Få meddelanden i realtid {#real-time-notifications}

**I/O-händelser** ger nästan statusövervakning i realtid via statushändelser. Detta är den mest effektiva metoden eftersom man slipper använda avsökningsmekanismer och utlösa ytterligare API-trafik.

**Recommendations:**

- **Webkrok-konfiguration:** Konfigurera webhooks för att ta emot push-meddelanden när statusändringar inträffar för skickade jobb. Detta underlättar övervakning i realtid.
- **Meddelanden:** Använd meddelanden på både jobb- och produktnivå för att övervaka processen för begäranden.

Läs dokumentationen om [prenumerera på Privacy Service](./privacy-events.md) för instruktioner om hur du ställer in en händelseregistrering för Privacy Service-meddelanden och hur du tolkar meddelandenyttolaster.

### Hämta alla jobb baserat på filter {#retrieve-filtered-responses-for-all-jobs}

Om du vill hämta alla dina sekretessjobbdata baserat på angivna filter **utföra en GET-förfrågan till `/jobs` slutpunkt**. Det här API-anropet är användbart för att ge en översikt på hög nivå över den aktuella jobbstatusen för stora uppsättningar jobb-ID:n med endast en begäran. Det saknas dock detaljerade produktsvar, men de finns i [`/jobs/{jobID}` slutpunkt](#retrieve-detailed-responses-for-specific-jobs).

En GET-förfrågan till `/jobs` slutpunkten används bäst för att samla in eller jämföra statusdata för en stor uppsättning jobb-ID, men är **not** avsedd för regelbundna avsökningstypsaktiviteter.

**Recommendations:**

- **Frågeparametrar:** Använd specifika filter för att begränsa resultaten, till exempel dataintervall, regeltyper och status (bearbetning, fullständig och så vidare).

Du kan visa en lista över alla aktuella sekretessjobb i din organisation via användargränssnittet för Privacy Service. Se [hantera sekretessjobb i gränssnittsdokumentationen](./ui/user-guide.md#job-requests) om du vill ha information om hur du filtrerar jobbeställningslistan. Du kan även läsa dokumentationen om [användning av slutpunkten /job i Privacy Service-API:t](./api/privacy-jobs.md).

Privacy Services-API-dokumentationen innehåller information om [tillgängliga frågeparameterfilter](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Hämta detaljerade svar för ett enskilt jobb {#retrieve-detailed-responses-for-specific-jobs}

Om du vill hämta detaljerade svar för ett enskilt jobb, **utföra en GET-begäran till /job/{jobID} slutpunkt**. Den här metoden är avsedd för djupare informationsinsamling, som produktspecifika svar och meddelanden om lyckade resultat. Ett anrop till den här slutpunkten är det bästa sättet att se vilka produkter som har svarat och vilka som fortfarande väntar, även om det är **not** avsedd för vanlig avsökningsaktivitet.

Se `/jobs/{JOB_ID}` slutpunktsdokumentation för information om [kontrollera status för ett specifikt jobb](./api/privacy-jobs.md#check-status).

### Exempel på idealiskt scenario {#ideal-scenario}

Använd en webkrok så att systemet automatiskt kan uppdatera poster och tillhandahålla rapporter eller varningar när grupper av ID:n från en begäran är slutförda. Om jobb fortfarande är utestående hämtar systemet dessa jobbstatusvärden med en GET-begäran till Privacy Service-API:t `/jobs` slutpunkt och tillhandahåller en högnivåuppdatering av listan.

Om ett visst jobb fortfarande väntar, eller har returnerat ett fel, kan du hämta det detaljerade svaret med en GET-förfrågan till `/job/{jobId}` slutpunkt.

## Data för åtkomstbegäran {#access-request-data}

När information om registrerade personer begärs, returnerar varje tjänst data i ett format som överensstämmer med det sätt på vilket de lagrar och använder dessa data. När alla tjänster har slutfört begäran anges en URL för ZIP-arkivfilen i jobbinformationen så att dessa data kan hämtas. Se felsökningsguiden för mer information om [hur man hämtar resultat från sekretessjobb](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Nedan följer viktiga anmärkningar som rör hanteringen av dataarkivet:

- Alla arkivfiler tas bort från Experience Platform-servrar efter 30 dagar. Du kan inte fråga kunddata som är äldre än 30 dagar.
- Arkivfilens struktur omfattar mappar för varje produkt som ingår i begäran och de datafiler som ingår i den. Arkivfiler eller mappar kan vara tomma om inga data hittades för det angivna ID:t.
- Data för tidigare skapade jobb är bara tillgängliga i 30 dagar efter slutförandedatumet. Efter den tiden tas data bort från systemet och en ny begäran måste göras.

**Recommendations:**

- **Protect dataarkiv:** Både URL- och ZIP-filen bör skyddas eftersom de kan innehålla personligt identifierbar information för den registrerade.

## Tekniska överväganden {#technical-considerations}

Det finns vissa tekniska överväganden att tänka på när du slutför en begäran om Privacy Service:

- **Datalagringsperiod:** Den maximala summeringsperioden är 60 dagar för alla grupper av jobb och den maximala tidsrymden för en fråga är 30 dagar (från-/till-datum).
- **Gatewaytimeout:** Tänk på att din begäran kan tas bort från gatewayen om den överstiger 60 sekunder.
- **Felhantering:** Granska felmeddelandena noggrant och skicka in förfrågningar på nytt där det är lämpligt. Privacy Servicen bearbetar inte automatiskt jobb som ett fel.
- **Om HTTP 429-fel:** Bekanta dig med felmeddelanden i HTTP 429 och de åtgärder som krävs för att åtgärda problemen. HTTP 429-fel orsakas av &#39;För många begäranden&#39;. Se [Vanliga felmeddelanden](./troubleshooting-guide.md#common-error-messages) i felsökningsguiden för mer information om hur du löser problemet.

## Nästa steg

Genom att läsa det här dokumentet har du nu den kunskap och de rutiner som krävs för att Privacy Servicen ska kunna användas på ett effektivt sätt. Nästa steg är att se [felsökningsguide](./troubleshooting-guide.md) om du vill ha svar på vanliga frågor om Privacy Service och information om vanliga fel i API:t.
