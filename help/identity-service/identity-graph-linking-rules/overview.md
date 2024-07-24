---
title: Översikt över regler för länkning av identitetsdiagram
description: Lär dig mer om länkningsregler för identitetsdiagram i identitetstjänsten.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 7daa9191f2e095f01c7c09f02f87aa8724e2e325
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Översikt över regler för länkning av identitetsdiagram

>[!AVAILABILITY]
>
>Länkningsregler för identitetsdiagram finns för närvarande i betaversionen. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna. Funktionen och dokumentationen kan komma att ändras.

## Innehållsförteckning

* [Översikt](./overview.md)
* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Gränssnitt för diagramsimulering](./graph-simulation.md)
* [Användargränssnitt för identitetsinställningar](./identity-settings-ui.md)
* [Exempel på diagramkonfigurationer](./configuration.md)
* [Exempel på scenarier](./example-scenarios.md)

Med Adobe Experience Platform Identity Service och Real-Time Customer Profile är det enkelt att anta att dina data är perfekt insamlade och att alla sammanfogade profiler representerar en enskild person via en personidentifierare, till exempel ett CRM-ID. Det finns emellertid möjliga scenarier där vissa data kan försöka sammanfoga flera olika profiler till en enda profil (&quot;komprimera diagram&quot;). För att förhindra dessa oönskade sammanfogningar kan du använda konfigurationer som tillhandahålls via länkningsregler för identitetsdiagram och tillåta korrekt personalisering för dina användare.

## Exempel på scenarier där komprimering av diagram kan inträffa

* **Delad enhet**: Delad enhet avser enheter som används av mer än en person. Exempel på delade enheter är surfplattor, biblioteksdatorer och kioskdatorer.
* **Felaktiga e-post- och telefonnummer**: Felaktiga e-post- och telefonnummer hänvisar till att slutanvändare registrerar ogiltig kontaktinformation, till exempel&quot;test<span>@test.com&quot; för e-post och&quot;+1-111-1111&quot; för telefonnummer.
* **Felaktiga eller felaktiga identitetsvärden**: Felaktiga eller felaktiga identitetsvärden refererar till icke-unika identitetsvärden som kan sammanfoga CRM-ID:n. IDFA:er måste till exempel ha 36 tecken (32 alfanumeriska tecken och fyra bindestreck), men det finns scenarier där en IDFA med identitetsvärdet &quot;user_null&quot; kan importeras. Telefonnummer har på liknande sätt bara stöd för numeriska tecken, men ett telefonnamnutrymme med identitetsvärdet &quot;inte specificerat&quot; kan kapslas.

Mer information om användningsscenarier för länkningsregler för identitetsdiagram finns i dokumentet om [exempelscenarier](./example-scenarios.md).

## Länkningsregler för identitetsdiagram {#identity-graph-linking-rules}

Med länkningsregler för identitetsdiagram kan du:

* Skapa ett enskilt identitetsdiagram/sammanfogad profil för varje användare genom att konfigurera unika namnutrymmen, vilket förhindrar att två olika personidentifierare sammanfogas i ett identitetsdiagram.
* Associera online-autentiserade händelser med personen genom att konfigurera prioriteringar

### Terminologi {#terminology}

| Terminologi | Beskrivning |
| --- | --- |
| Unikt namnutrymme | Ett unikt namnutrymme är ett identitetsnamnutrymme som har ställts in för att vara distinkt i sammanhanget för ett identitetsdiagram. Du kan konfigurera ett namnutrymme så att det är unikt med användargränssnittet. När ett namnutrymme definieras som unikt kan ett diagram bara ha en identitet som innehåller det namnutrymmet. |
| Namnområdesprioritet | Namnområdesprioritet avser den relativa vikten av namnutrymmen jämfört med varandra. Namnområdesprioriteten kan konfigureras via användargränssnittet. Du kan rangordna namnutrymmen i ett givet identitetsdiagram. När den är aktiverad används namnprioritet i olika scenarier, t.ex. indata för identitetsoptimeringsalgoritm och fastställande av primär identitet för upplevelsehändelsefragment. |
| Identitetsoptimeringsalgoritm | Identitetsoptimeringsalgoritmen ser till att riktlinjer som skapas genom att konfigurera en unik namnområdes- och namnområdesprioritet används i ett givet identitetsdiagram. |

### Unikt namnutrymme {#unique-namespace}

Du kan konfigurera ett namnutrymme så att det blir unikt med hjälp av arbetsytan för identitetsinställningar i användargränssnittet. Om du gör det informeras identitetsoptimeringsalgoritmen om att ett visst diagram bara kan ha en identitet som innehåller det unika namnutrymmet. Detta förhindrar sammanfogning av två olika personidentifierare i samma diagram.

Tänk på följande scenario:

* Scott använder en surfplatta och öppnar sin webbläsare Google Chrome för att gå till nike<span>.com, där han loggar in och bläddrar efter nya basketskor.
   * Bakom scenerna loggar det här scenariot följande identiteter:
      * Ett ECID-namnutrymme och -värde som representerar webbläsarens användning
      * Ett CRM ID-namnutrymme och värde som representerar den autentiserade användaren (Scott loggade in med kombinationen användarnamn och lösenord).
* Hans son Peter använder sedan samma surfplatta och även Google Chrome för att gå till nike<span>.com, där han loggar in med sitt eget konto för att söka efter fotbollsutrustning.
   * Bakom scenerna loggar det här scenariot följande identiteter:
      * Samma ECID-namnutrymme och värde som representerar webbläsaren.
      * Ett nytt CRM ID-namnutrymme och värde som representerar den autentiserade användaren.

Om CRM-ID har konfigurerats som ett unikt namnområde delas CRM-ID:n upp i två separata identitetsdiagram i identitetoptimeringsalgoritmen, i stället för att sammanfoga dem.

Om du inte konfigurerar ett unikt namnutrymme kan du få oönskade diagramsammanfogningar, till exempel två identiteter med samma CRM ID-namnutrymme, men olika identitetsvärden (scenarier som dessa representerar ofta två olika personenheter i samma diagram).

Du måste konfigurera ett unikt namnutrymme för att informera algoritmen för identitetsoptimering om du vill tillämpa begränsningar för identitetsdata som hämtas till ett givet identitetsdiagram.

### Namnområdesprioritet {#namespace-priority}

Namnområdesprioritet avser den relativa vikten av namnutrymmen jämfört med varandra. Namnområdesprioriteten kan konfigureras via användargränssnittet och du kan rangordna namnutrymmen i ett givet identitetsdiagram.

Ett sätt som namnområdesprioriteten används på är att fastställa den primära identiteten för händelsefragment (användarbeteende) i kundprofilen i realtid. Om prioritetsinställningar har konfigurerats kommer den primära identitetsinställningen på Web SDK inte längre att användas för att avgöra vilka profilfragment som lagras.

Både unika namnutrymmen och namnområdesprioriteter kan konfigureras på arbetsytan för identitetsinställningar. Effekterna av deras konfigurationer är dock annorlunda:

| | Identitetstjänst | Kundprofil i realtid |
| --- | --- | --- |
| Unikt namnutrymme | I identitetstjänsten refererar algoritmen för identitetsoptimering till unika namnutrymmen för att bestämma vilka identitetsdata som importeras till ett visst identitetsdiagram. | Unika namnutrymmen påverkar inte kundprofilen i realtid. |
| Namnområdesprioritet | I identitetstjänsten avgör namnområdesprioriteten att rätt länkar tas bort för diagram som har flera lager. | När en upplevelsehändelse kapslas in i en profil blir det namnutrymme som har högst prioritet den primära identiteten för profilfragmentet. |

* Namnområdesprioriteten påverkar inte diagrambeteendet när gränsen på 50 identiteter per diagram nås.
* **Namnområdesprioriteten är ett numeriskt värde** som tilldelats ett namnutrymme och anger dess relativa betydelse. Detta är en egenskap för ett namnutrymme.
* **Primär identitet är den identitet i vilken ett profilfragment lagras mot**. Ett profilfragment är en datapost som lagrar information om en viss användare: attribut (som vanligtvis hämtas via CRM-poster) eller händelser (som vanligtvis hämtas från upplevelsehändelser eller onlinedata).
* Namnområdesprioriteten avgör den primära identiteten för händelsesegment för upplevelser.
   * För profilposter kan du använda arbetsytan för scheman i användargränssnittet i Experience Platform för att definiera identitetsfält, inklusive den primära identiteten. Mer information finns i guiden [Definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md).
* Om en upplevelsehändelse har två eller flera identiteter med den högsta namnområdesprioriteten i identityMap, kommer den att nekas att matas in eftersom den betraktas som &quot;felaktiga data&quot;. Om identityMap till exempel innehåller `{ECID: 111, CRMID: John, CRMID: Jane}` kommer hela händelsen att avvisas som felaktiga data eftersom det betyder att händelsen är kopplad till både `CRMID: John` och `CRMID: Jane` samtidigt.

Mer information finns i handboken om [namnområdesprioritet](./namespace-priority.md).

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md).
* [Namnområdesprioritet](./namespace-priority.md).
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md).
