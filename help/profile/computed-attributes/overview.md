---
title: Översikt över beräknade attribut
description: Beräknade attribut är funktioner för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.
source-git-commit: 7ed473750b673eefd84b8d727043ad6ea35c3a8e
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---


# Översikt över beräknade attribut

Personalisering baserad på användarbeteende är ett viktigt krav för marknadsförarna att maximera personaliseringens effekt. Anpassa till exempel marknadsföringsmejl med den senast visade produkten för att öka konverteringen, eller personalisera webbsidan baserat på det totala antalet köp som görs av användarna för att öka kundlojaliteten.

Beräknade attribut hjälper dig att snabbt konvertera profilbeteendedata till aggregerade värden på profilnivå utan att vara beroende av tekniska resurser för:

- Möjliggör riktad personalisering från en till en eller flera gånger med aktivering av beteendeaggregat till Real-time Customer Data Platform destinationer och användning i Adobe Journey Optimizer
- Förenklad målgruppssegmentering med lagring av beteendeaggregat som profilattribut
- Standardisering av aggregerade profilbeteendedata för användning över olika plattformar och appar
- Bättre datahantering med konsolidering av data från gamla profithändelser till meningsfulla beteendeinsikter

Dessa aggregat beräknas baserat på profilaktiverade Experience Event-datamängder som importerats till Adobe Experience Platform. Varje beräknat attribut är ett profilattribut som har skapats i ditt profilunionsschema och grupperas under fältgruppen &quot;SystemComputedAttribute&quot; i ditt unionsschema.

Exempel:

- Personalisera marknadsföringsmejl med totala belöningspoäng för att gratulera användarna till att de befordras till en premiumnivå
- Anpassa kommunikationen till användarna utifrån antal inköp och frekvens
- Anpassa e-postmeddelanden om kvarhållande baserat på förfallodatum för prenumeration
- Omdirigera användare som visade men inte köpte en produkt med den senast visade produkten
- Aktivera händelseaggregering via beräknade attribut till ett system längre fram i kedjan med Real-Time CDP Destinations
- Komprimera flera händelsebaserade målgrupper till en mer komprimerad grupp med beräknade attribut
- Oautentiserade användare kan återanvända sina partner-ID:n från händelser

Den här guiden hjälper dig att bättre förstå vilken roll beräknade attribut har inom plattformen, förutom att förklara grunderna för beräknade attribut.

## Förstå beräknade attribut

Med Adobe Experience Platform kan du enkelt importera och sammanfoga data från flera källor för att generera [!DNL Real-Time Customer Profiles]. Varje profil innehåller viktig information om en individ, t.ex. kontaktinformation, inställningar och inköpshistorik, vilket ger en helhetsbild av kunden.

En del av den information som samlas in i profilen är lätt att förstå när datafälten läses direkt (t.ex.&quot;förnamn&quot;) medan andra data kräver att man utför flera beräkningar eller använder andra fält och värden för att kunna generera informationen (t.ex.&quot;total livslängd&quot;). För att göra dessa data enklare att förstå i en överblick [!DNL Platform] I kan du skapa beräknade attribut som automatiskt utför dessa referenser och beräkningar och returnerar värdet i lämpligt fält.

Beräknade attribut inkluderar att skapa ett uttryck, eller &quot;rule&quot;, som fungerar på inkommande data och lagrar resultatvärdet i ett profilattribut. Uttryck kan definieras på flera olika sätt, så att du kan ange vilka händelser som ska aggregeras på, sammanställningsfunktioner eller svarstider.

### Funktioner

Med beräknade attribut kan du definiera händelseaggregat på ett självbetjäningssätt genom att utnyttja fördefinierade funktioner. Information om dessa funktioner finns nedan:

|  -funktion | Beskrivning | Datatyper som stöds | Exempel på användning |
| -------- | ----------- | -------------------- | ------------- |
| SUM | En funktion som **summor** det angivna värdet för kvalificerade händelser. | Heltal, siffror, långa | Summan av alla inköp de senaste 7 dagarna |
| COUNT | En funktion som **antal** antalet händelser som har inträffat för den angivna regeln. | Ej tillämpligt | Antal inköp de senaste tre månaderna |
| MIN | En funktion som hittar **minimum** värdet för de kvalificerade händelserna. | Heltal, siffror, lång tid, tidsstämplar | Första inköpsdata under de senaste 7 dagarna<br/>Minsta orderbelopp de senaste fyra veckorna |
| MAX | En funktion som hittar **maximum** värdet för de kvalificerade händelserna. | Heltal, siffror, lång tid, tidsstämplar | Senaste inköpsdata de senaste 7 dagarna<br/>Högsta orderbelopp de senaste fyra veckorna |
| MOST_RECENT | En funktion som hittar det angivna attributvärdet från den senaste kvalificerade händelsen. Den här funktionen ger **båda** värdet samt tidsstämpeln för attributet. | Alla primitiva värden, arrayer med primitiva värden | Den senaste produkten har visats de senaste 7 dagarna |

### Återställningsperioder

Beräknade attribut beräknas gruppvis, vilket gör att du kan hålla aggregaten aktuella och använda de senaste händelserna. För att stödja dessa nära realtidsscenarier varierar uppdateringsfrekvensen beroende på händelseuppslagsperioden.

Uppslagsperioden refererar till den tid som granskas när Experience Events för det beräknade attributet sammanställs. Den här tidsperioden kan definieras i timmar, dagar, veckor eller månader.

Uppdateringsfrekvensen avser den frekvens med vilken de beräknade attributen uppdateras. Värdet beror på uppslagsperioden och ställs in automatiskt.

| Sökperiod | Uppdateringsfrekvens |
| --------------- | ----------------- |
| Upp till 24 timmar | Varje timme |
| Upp till 7 dagar | Dagligen |
| Upp till 4 veckor | Veckovis |
| Upp till 6 månader | Månadsvis |

Om det beräknade attributet till exempel har en summeringsperiod på de senaste 7 dagarna, beräknas det här värdet baserat på värdena för de senaste 7 dagarna och uppdateras sedan dagligen.

>[!NOTE]
>
>Både veckor och månader anses vara **kalenderveckor** och **kalendermånader** när det används i händelsesökningar. Kalenderveckan börjar på **söndag** och slutar på **Lördag** Veckodag.

**Snabb uppdatering** {#fast-refresh}

Snabb uppdatering gör att du kan uppdatera dina attribut. Om du aktiverar det här alternativet kan du uppdatera dina beräknade attribut dagligen, även under längre uppslagsperioder, så att du snabbt kan reagera på användaraktiviteter.

>[!NOTE]
>
>Om du aktiverar snabb uppdatering kommer det att variera varaktigheten för din händelsesökning, eftersom uppslagsperioden rullar varje vecka eller månad.
>
>Om du skapar ett beräknat attribut med en tvåveckorsperiod för återsökning där snabb uppdatering är aktiverat innebär det att den inledande återsökningsperioden är två veckor. För varje daglig uppdatering kommer dock uppslagsperioden att innehålla händelser från den extra dagen. Det här tillagda antalet dagar fortsätter tills nästa kalendervecka startar, där uppslagsfönstret rullar över och återgår till två veckor.
>
>Om det till exempel fanns en tvåveckorsperiod för uppslag som började den 15 mars (söndag) med snabb uppdatering aktiverad och daglig uppdatering, kommer uppslagsperioden att fortsätta att växa till den 22 mars, där den återställs till två veckor. Det beräknade attributet är kort och gott **uppdaterad** varje dag, med en uppslagsperiod som ökar från **två** veckor till **tre** veckor under veckan och sedan återgår till **två** veckor.

## Nästa steg

Läs mer om hur du skapar och hanterar beräknade attribut i [API-guide för beräknade attribut](./api.md) eller [gränssnittshandbok för beräknade attribut](./ui.md).
