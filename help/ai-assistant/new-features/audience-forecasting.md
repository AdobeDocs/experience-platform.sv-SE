---
title: Övervaka betydande ändringar och målgruppsprognoser med AI Assistant
description: Lär dig hur du använder AI Assistant för att övervaka viktiga förändringar och förutse målgrupper i Adobe Experience Platform.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Övervaka betydande förändringar och förutse målgruppens tillväxt med AI Assistant

>[!AVAILABILITY]
>
>Den här funktionen är i Alpha och är kanske inte tillgänglig för din organisation. Om du vill delta i programmet Alpha och få tillgång till den här funktionen kontaktar du ditt kontoteam på Adobe.

I dagens datadrivna marknadsföringslandskap är aktuella och korrekta insikter viktiga. Oavsett om du är företagsanvändare eller arbetar med marknadsföring behöver du kunna interagera med era målgrupper på ett konsekvent sätt och göra snabba och slagkraftiga justeringar baserade på tydliga insikter. För att bibehålla er inriktning eller uppnå era affärsmål måste ni ha den åtgärdbara information som behövs för att driva effektiva kampanjer och optimera resurserna.

Du kan använda AI Assistant för Adobe Experience Platform för att övervaka betydande ändringar och tillhandahålla tillväxtprognoser för er målgrupp och era datauppsättningar. Sedan kan ni använda den här informationen för att säkerställa integriteten för era målgruppsdata och erbjuda förutseende prognoser som stöder dataunderbyggda beslut.

Läs det här dokumentet om du vill veta hur du kan övervaka betydande förändringar och förutse publikens tillväxt och fluktuationer med hjälp av AI Assistant.

## Viktiga termer och definitioner {#key-terminology-and-definitions}

I följande tabell finns en lista med viktiga termer och deras motsvarande definitioner.

| Terminologi | Definition |
| --- | --- |
| Betydande ändring | En betydande förändring är en stor procentuell förändring av målgrupp eller datauppsättningsstorlek, som definieras av specifika tröskelvärden (till exempel 10 % för stora målgrupper). Betydande ändringar hjälper till att identifiera avvikelser som påverkar datastabiliteten. |
| Anomalier | Anomalier är oväntade variationer i data, till exempel en plötslig 20-procentig ökning hos en **HDR-målgrupp**. En avvikelse kan bero på ett potentiellt dataproblem eller en ändring av målgruppsdefinitionen. |
| Historiska data | Historiska data avser långsiktiga data, vanligtvis ett till tre år. Du kan använda historiska data för att spåra mönster. **Obs!** Under scenen Alpha tillhandahåller AI Assistant historiska data på upp till 13 månader. |
| Nya/senaste data | Nya data eller data avser datapunkter som observerats under en kort period, vanligtvis under en vecka eller upp till 30 dagar. Du kan använda nya eller nyligen använda data för att markera omedelbara trender och göra snabba justeringar. |
| Prognos | En prognos är prognoser för framtida målgrupper eller datauppsättningsstorlekar baserade på tidigare trender. Du kan använda prognosdata som stöd för långsiktig planering. |
| Målgruppsstorlek | Målgruppens storlek avser det totala antalet profiler inom en målgrupp. Målgruppsstorleken uppdateras med varje upprepning av datainmatning. |
| Tidsram för jämförelse | AI Assistant använder fördefinierade tidsramar för jämförelse. Senaste avvikelser är som standard sju dagars tillbakagång, medan tidigare avvikelser omfattar 30 dagar. Historiska trender sträcker sig upp till 13 månader. |

{style="table-layout:auto"}

## Använd exempel på exempel {#use-case-examples}

AI Assistants förmåga att övervaka betydande förändringar och förutse målgrupper kan vara särskilt användbart i följande fall:

### Marknadsföringsåtgärder

Marknadsförare ansvarar för att säkerställa att målgruppsdata är korrekta och konsekventa. Som medlem i ett marknadsföringsteam kan ditt ansvar omfatta övervakning av datakvalitet, åtgärder vid oväntade förändringar och en stabil grund för alla marknadsföringssatsningar. Ni kan använda AI Assistants avvikelseidentifiering för att identifiera och åtgärda viktiga målgrupps- eller datauppsättningsändringar, vilket förhindrar störningar som kan påverka kampanjens resultat.

### Affärsanvändare och -marknadsförare

Som affärsanvändare och marknadsförare kan ni förlita er på korrekta målgruppsinsikter för att fatta datadrivna beslut och se till att era kampanjer når de avsedda målgrupperna effektivt. Med prognosfunktionerna i AI Assistant kan ni förutse målgruppens tillväxt eller minskning och möjliggöra strategiska justeringar av resurser och målinriktning över tid.

## Viktiga funktioner

>[!IMPORTANT]
>
>Följande funktioner ligger i Alpha och fokuserar på grundläggande funktioner för övervakning och prognoser. Eftersom den här funktionen är i Alpha måste du kontrollera att du har fått korrekta svar från AI Assistant.

### Övervaka viktiga förändringar i målgrupp och data

Du kan använda AI Assistant för att identifiera signifikanta förändringar i målgrupper och datauppsättningar genom att spåra avvikelser från typiska mönster. Varje betydande förändring baseras på fördefinierade tröskelvärden som är anpassade efter målgruppens storlek.

| Målgruppsstorlek | Antal profiler | Beskrivning |
| --- | --- | --- |
| Små målgrupper | 1 till 100 000 profiler | Flaggar en ändring på 30 % eller mer om inte en viss procentsats anges. |
| Medium målgrupper | 100 000 till 500 000 profiler | Flaggar en ändring på 25 % eller mer om inte en viss procentsats anges. |
| Stora målgrupper | 500 000 till 1 miljon profiler | Flaggar en ändring på 20 % eller mer om inte en viss procentsats anges. |
| Mycket stora målgrupper | Över 1 miljon profiler | Flaggar en ändring på 10 % eller mer om inte en viss procentsats anges. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Exempel på scenario

Betydande förändringar tyder på avvikelser som kan påverka målgruppernas stabilitet eller datatillförlitlighet. Om till exempel en **HDR**-målgrupp råkar ut för en plötslig minskning med 15 % av storleken, kommer AI Assistant att märka detta som en betydande förändring. Sedan kan ni använda den här informationen för att undersöka och lösa potentiella problem innan de påverkar era kampanjer.

>[!ENDSHADEBOX]

>[!TIP]
>
>AI Assistant meddelar dig inte automatiskt om stora förändringar i publikens storlek inträffar. Du måste inleda en konversation med AI Assistant och fråga vilka målgrupper som har ändrats avsevärt eller med en viss marginal inom en viss tidsperiod.

### Prognoser för målgrupp och datamängdstillväxt

Du kan använda AI Assistant för att referera till historiska datatrender och projicera framtida målgrupper och datamängdsstorlekar. Sedan kan ni använda dessa insikter för att stödja er resursplanering och strategiska justeringar. För närvarande kan ni använda AI Assistant för att förutsäga målgrupps- och datamängdstillväxt i 30 dagar. Genom att förstå förväntad målgruppstillväxt eller tillbakagång kan ni anpassa era målinriktningsstrategier och fördela resurserna därefter.

### Insikter om historiska målgruppsstorlekar

Förutom att identifiera betydande ändringar kan du använda AI Assistant för att hämta historiska insikter och jämföra den aktuella målgruppen eller datamängdsstorleken med tidigare data. Den här funktionen har stöd för att spåra långsiktiga trender och utvärdera effekten av tidigare marknadsföringsaktiviteter.

Du kan ställa frågor om AI Assistant, till exempel&quot;Vilken storlek hade min&quot;lojalskund&quot; förra månaden? för att se historiska data om denna specifika målgrupps tillväxt eller nedgång.

## Exempelfrågor för övervakning av viktiga ändringar

Du kan rama in dina AI Assistant-frågor på flera olika sätt.

* Om din fråga innehåller ett procenttal, till exempel **&quot;Vilka målgrupper har ändrats över 30 % eller mer?&quot;**, kommer AI Assistant att använda procentandelen som referenspunkt.
* Om din fråga inte anger ett procenttal tolkar AI Assistant viktiga ändringar baserat på standardinställningarna.

Se följande tabeller för exempel på frågor som illustrerar hur AI Assistant tolkar betydande ändringar baserat på målgruppens storlek:

| Målgruppsinformation eller målgruppsändring | Exempel |
| --- | --- |
| <ul><li>Vilken är den aktuella storleken på {AUDIENCE_NAME}?</li><li>Visa målgrupperna som har visat en ändring av {PERCENT} över {DATE_DURATION}.</li></ul> | <ul><li>Vilken är den nuvarande storleken för den som handlar med High Value Shoppers?</li><li>Visa de målgrupper som har visat en förändring på 20 % under den senaste veckan.</li></ul> |

{style="table-layout:auto"}

| Målgruppsspecifika frågor | Exempel |
| --- | --- |
| <ul><li>Vilka målgrupper har ändrat mer än {PERCENT} i {DATE_OR_DURATION}?</li><li>Visa mig målgrupper med en betydande förändring över {DATE_OR_DURATION}.</li><li>Visa mig fördelningen av målgrupper med de största förändringarna över {DATE_OR_DURATION}.</li><li>Visa målgrupper som har minskat mer än {PERCENT} på {DATE_OR_DURATION}.</li></ul> | <ul><li>Vilka målgrupper har förändrats mer än 20 % den senaste veckan?</li><li>Visa mig målgrupper med stor förändring under de senaste sex månaderna.</li><li>Visa mig hur de största förändringarna är mellan den 1 och 31 oktober.</li><li> Visa mig målgrupper som har minskat med över 20 % sedan 31 augusti. |

{style="table-layout:auto"}

## Ytterligare information

### Förstå tröskelvärdet för&quot;betydande förändring&quot;

Du kan ange en viss procentandel när du frågar efter information om viktiga ändringar i AI Assistant. Om du inte anger en viss procentandel refererar AI Assistant till en fördefinierad uppsättning tröskelvärden för att avgöra vad som räknas som en betydande ändring. Standardtröskelvärdena baseras på storleken på en viss målgrupp. I följande tabell finns information om vad som utgör en betydande förändring, baserat på målgruppens storlek:

| Målgruppsstorlek | Vad är viktigt? |
| --- | --- |
| 1 miljon eller mer | 10 % eller mer |
| 500-1 miljon | 20 % eller mer |
| 100 till 500 kB | 25 % eller mer |
| Mindre än 100 kB | 30 % eller mer |

### Allmänna tidslinjer och specifika datum

AI Assistant stöder både specifika och generiska tidsbaserade jämförelser för målgruppsstorlekar och tolkar dem baserat på sammanhanget i frågan.

>[!BEGINTABS]

>[!TAB Allmänna tidslinjer]

Allmänna tidslinjer hänvisar till frågor som använder språk som &quot;den här veckan&quot; eller &quot;sista veckan&quot;. Om du ställer en fråga från AI Assistant, t.ex.&quot;Vilka målgrupper har ändrats med mer än 20 % den senaste veckan?&quot;, kommer AI Assistant att beräkna och jämföra den **genomsnittliga publiken** under den angivna perioden.

Använd den här metoden för att få en bredare bild av hur publiken förändras över tiden, så att ni bättre kan förstå trender inom varje vecka eller månad.

>[!TAB Specifika datum]

Om din fråga refererar till ett visst datum kommer AI Assistant att jämföra de **exakta målgruppsstorlekarna** för varje angivet datum.

Använd den här exakta jämförelsen för att analysera förändringar mellan specifika tidpunkter och få klarhet i hur målgruppens storlek kan utvecklas under vissa dagar.

>[!ENDTABS]

Ni kan utnyttja den här flexibiliteten för att bättre förstå målgruppsdynamiken över både breda och exakta tidsramar. Oavsett om du håller på att spåra allmänna trender eller undersöker exakta skift mellan specifika datum kan du använda AI Assistants adaptiva mekanism för att hämta den mest relativa jämförelsen för din fråga.

## Vanliga frågor och svar {#faq}

I det här avsnittet finns svar på vanliga frågor om övervakning av viktiga ändringar och målgruppsprognoser med AI Assistant.

### Hur mycket historiska data kan jag titta på för att se hur stor publiken blir?

AI Assistant sparar 12 månaders historiskt data om målgruppens storlek. Du kan ställa frågor om målgruppsändringar inom den här tidsramen för att förstå mönster för tillväxt eller nedgång under det senaste året.

### Hur långt tillbaka i historiken kan jag gå för att se förändringar i publiken?

AI Assistant håller reda på förändringar från den dag de aktiveras i organisationen och går så långt tillbaka som den senaste målgruppsdefinitionen ändras. När AI Assistant har aktiverats kan du kontinuerligt övervaka och registrera definitionsändringar i upp till 12 månader, vilket möjliggör framtida uppföljning och jämförelse av data.

### Hur mycket historik behövs för en prognos?

Minst 30 dagars data krävs för tillförlitliga prognoser från den senaste ändringen av målgruppsdefinitionen. I vissa fall, t.ex. vid prognoser för [!DNL Black Friday], kan AI Assistant behöva upp till 12 månader med historiska data.

### Hur tolkar AI-assistenten&quot;nyligen&quot;?

AI-assistenten tolkar&quot;nyligen&quot; som de senaste sju dagarna. För frågor som refererar till nyligen gjorda ändringar hanterar AI Assistant data från den här tidsperioden för att identifiera trender eller förändringar.

### Hur jämför AI Assistant målgruppsstorlekar?

När specifika datum anges jämför AI Assistant målgruppsstorlekarna på dessa specifika dagar. För mer allmänna frågor, t.ex. de som refererar till&quot;senaste tre månaderna&quot; eller&quot;förra veckan&quot;, jämför AI Assistant den genomsnittliga storleken för den perioden med den senaste dagens genomsnitt.

### Hur aktuella är AI-assistentens målgruppsdata?

Det kan ta 24 till 48 timmar för AI Assistant att uppdatera data från Real-time Customer Data Platform. För frågor som refererar till&quot;igår&quot; tolkar AI Assistant detta som en dag innan den senaste informationen finns tillgänglig.

## Funktioner som inte är tillgängliga

Följande funktioner stöds för närvarande inte:

### Avancerad analys av rotorsak

AI Assistant kan identifiera betydande ändringar, men kan för närvarande inte tillhandahålla en detaljerad analys av rotorsaker för dessa förändringar. Framtida iterationer av AI Assistant syftar till att specificera vilka datauppsättningar eller attribut som bidrar till betydande förändringar hos era målgrupper.

### Omfattande storlekar för historiska datamängder

För närvarande stöds inte fullständig historikspårning av datastorlekar. För närvarande tillhandahåller AI Assistant målgrupps- och datauppsättningshistorik i upp till 13 månader.