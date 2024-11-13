---
title: Uppskattning av naturspråk med AI Assistant
description: Lär dig hur du använder AI Assistants funktioner för beräkning av naturliga språk.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Naturlig språkinställning med AI Assistant

>[!AVAILABILITY]
>
>Den här funktionen är i Alpha och är kanske inte tillgänglig för din organisation. Om du vill delta i programmet Alpha och få tillgång till den här funktionen kontaktar du ditt kontoteam på Adobe.

Du kan använda funktionerna för beräkning av naturligt språk i AI Assistant för Adobe Experience Platform för att beräkna målgruppsstorlekar och förutse målgruppsegenskaper baserat på enkla, konversationsfrågor. Med den här funktionen kan ni göra målgruppsinsikter mer tillgängliga och intuitiva. Detta kan vara särskilt användbart för era affärs- och marknadsföringsaktiviteter, särskilt om ni hanterar era målgrupper dagligen och förlitar er på dessa insikter för att utforma effektiva marknadsföringsstrategier.

Med AI Assistants naturliga språkbehandlingsfunktioner kan du ställa frågor som:&quot;Hur många profiler har jag i Kalifornien mellan 25 och 35 år&quot; eller&quot;Hur många värdefulla kunder har vi?&quot; eller till och med&quot;Hur stor procentandel av min publik kommer att köpa under nästa månad?&quot; AI Assistant tolkar sedan dessa frågor och returnerar uppskattningar eller benägenhetspoäng som du kan använda för att fatta dataunderbyggda beslut.

Läs det här dokumentet om du vill veta hur du kan använda AI Assistants naturliga funktioner för språkinställningar.

## Viktiga termer och definitioner {#key-terminology-and-definitions}

I följande tabell finns en lista med viktiga termer och deras motsvarande definitioner.

| Terminologi | Definition |
| --- | --- |
| Beräkning av målgruppsstorlek | Processen att beräkna antalet medlemmar inom en viss målgrupp baserat på ett definierat kriterium. Du kan basera dina storleksuppskattningar på profildata, inklusive profiler som inte finns i en publik. Dessutom kan ni hämta uppskattningar av målgruppens storlek utan att först behöva skapa en målgrupp. Använd den här insikten för att förstå er räckvidd för riktade kampanjer. |
| Propensitetsuppskattning | En prognos över sannolikheten för att medlemmar inom en viss målgrupp kommer att uppvisa specifika beteenden (t.ex. att göra ett köp, köpa) inom en viss tidsram. Propensitetsberäkning är specifik för målgrupper inom Real-time Customer Data Platform, men kan inkludera profildata, inklusive profiler i alla målgrupper. Ni kan hänvisa till den här insikten när ni optimerar era kampanjer och hanterar strategier för målgruppsinnehållande. |
| Naturlig språkbearbetning | AI Assistants förmåga att tolka och besvara frågor på vardagsspråket, så att ni kan interagera med konversationer och få relevanta insikter utan att behöva använda tekniska frågor. |
| Fördefinierade tidsbildrutor | Standardtidsintervall (&quot;förra månaden&quot;,&quot;nästa 30 dagar&quot;) som stöds av AI Assistant för att beräkna målgruppens storlek och egenskaper. **Obs!** Anpassade tidsramar kanske inte stöds fullt ut på scenen Alpha. |
| Ögonblicksbildsdata | Den datauppsättning som AI Assistant använder för att tillhandahålla uppskattningar. Dessa data uppdateras från Real-time Customer Data Platform var 24:e till var 48:e timme och därför kanske insikterna inte återspeglar målgruppsändringar i realtid. |

{style="table-layout:auto"}

## Använd exempel på exempel {#use-case-examples}

Funktioner för beräkning av AI-assistentens naturliga språk kan vara särskilt användbara i följande fall:

### Marknadsföringsåtgärder

Som professionell marknadsoperatör kan ditt ansvar omfatta hantering och övervakning av målgruppsdata för att säkerställa att de är anpassade till era affärsmål. Med AI Assistants funktion för beräkning av naturens språk kan ni snabbt samla in insikter om målgruppernas storlek och egenskaper utan att behöva skapa en målgrupp först eller en omfattande kunskap om dataanalys.

hjälper dem att upprätthålla en konsekvent, datadriven strategi i sina arbetsflöden.

### Affärsanvändare och -marknadsförare

Som affärsanvändare och marknadsförare kan snabb tillgång till målgruppsdata vara avgörande för att er kampanjplanering, målgruppsanpassning och utvärdering ska lyckas. Med AI Assistants funktion för beräkning av naturliga språk kan ni förenkla er tillgång till målgruppsinformation, ställa enkla frågor och få användbara insikter som hjälper er att skapa målgrupper och optimera kampanjer.

## Viktiga funktioner

>[!IMPORTANT]
>
>Följande funktioner ligger i Alpha och fokuserar på grundläggande funktioner för en naturlig språkinställning. Eftersom den här funktionen är i Alpha måste du kontrollera att du har fått korrekta svar från AI Assistant.

### Beräkning av målgruppsstorlek

Du kan använda naturliga språkfrågor för att be AI Assistant att beräkna storleken på specifika målgrupper. Den här funktionen kan vara särskilt användbar för att mäta målgruppernas räckvidd och effekt. Som marknadsföringsstrateg kan du till exempel ställa frågor som:

* &quot;Hur många profiler bor i New York?&quot;
* &quot;Hur många profiler har jag med ett e-postmeddelande och har godkänt?&quot;

Använd den här funktionen för att förenkla processen att beräkna målgruppsstorlekar och få svar direkt utan att behöva navigera i komplexa datafilter eller segmentdefinitioner.

### Uppskattning av målgruppsbenägenhet

>[!TIP]
>
>Ditt Experience Platform-konto måste etableras med [Kund-AI](../../intelligent-services/customer-ai/overview.md) för att AI Assistants benägenhetsuppskattningsfunktioner ska kunna användas.

Ni kan använda uppskattningar av målgruppens benägenhet för att identifiera sannolikheten för specifika beteenden eller åtgärder inom en viss målgrupp. Du kan till exempel ställa frågor som:

* &quot;Hur stor procentandel av min nuvarande publik kommer att köpa under nästa månad?&quot;
* &quot;Hur många profiler har jag med stor benägenhet att konvertera?&quot;

Genom att ställa frågor om naturliga språk kan ni ta fram benägenhetspoäng som anger procentandelen eller sannolikheten för att målgruppsmedlemmar uppvisar vissa beteenden, vilket hjälper er att göra proaktiva justeringar av kampanjer eller strategier för kundlojalitet.

## Exempelfrågor om målgruppsstorlek och beräkning av benägenhet

Nedan följer några exempelfrågor som du kan ställa till AI Assistant för att få en förståelse för målgruppsstorlekar och beteendeegenskaper:

### Beräkning av målgruppsstorlek

* &quot;Hur många profiler har jag med ett e-postnummer eller mobiltelefonnummer?&quot;
* &quot;Hur många profiler har jag i New York?&quot;
* &quot;Vilka är de fem främsta lägena där mina kunder bor?&quot;

### Uppskattning av målgruppsbenägenhet

* &quot;Hur stor procentandel av min publik kommer att köpa under nästa månad?&quot;
* &quot;Hur många kunder förväntas konvertera under nästa kvartal?&quot;

Ni kan använda den flexibilitet som naturliga språkfrågor ger för att få snabba insikter i målgruppsdynamik utan att behöva ha teknisk expertis.

## Frågor och svar

I det här avsnittet finns svar på vanliga frågor om beräkning av naturspråk med AI Assistant.

### Hur ofta uppdaterar AI-assistenten målgruppsdata?

AI Assistentens data uppdateras var 24-48:e timme. Därför kan uppskattningarna återspegla små förseningar. Det innebär att när du frågar efter&quot;aktuella&quot; data återspeglar svaret den senaste ögonblicksbilden, som kan vara upp till 48 timmar gammal.

### Kan jag fråga efter målgrupper eller egenskaper med anpassade datumintervall?

För närvarande har AI Assistant stöd för fördefinierade datumintervall, t.ex.&quot;förra månaden&quot; eller&quot;nästa 30 dagar&quot;. Anpassade datumintervall efter dessa fördefinierade alternativ stöds inte fullt ut på scenen Alpha. Om en anpassad tidsram begärs, ger AI Assistant insikter baserat på den närmaste tillgängliga tidsramen.

### Hur beräknar AI Assistant benägenhetspoängen?

Propensitetspoäng beräknas med hjälp av [Kund-AI](../../intelligent-services/customer-ai/overview.md). AI Assistant använder maskininlärningsmodeller för att förutsäga sannolikheten för specifika målgruppsbeteenden, som inköp och bortfall, inom den begärda tidsramen. Vid beräkning av benägenhetspoäng i AI Assistant under Alpha-fasen används inte upplevelsehändelser eller beteendedata.

### Kommer AI Assistant att uppskatta målgruppens storlek eller egenskaper utifrån realtidsdata?

Nej, det finns för närvarande inga realtidsdata. Beräkningarna baseras på nyligen tagna ögonblicksbilder av data, som uppdateras var 24-48:e timme. Realtidsuppdateringar ligger utanför omfånget under Alpha.

### Hur beräknas egenskaperna?

AI Assistant förlitar sig på kundens AI-modeller för att svara på eventuella sannolikhets- eller benägenhetspoäng.

## Funktioner som inte är tillgängliga

Följande funktioner stöds för närvarande inte:

### Uppskattningar av målgruppsstorlek baserade på händelser med beteendedata

AI Assistant kan för närvarande inte besvara frågor baserat på beteendedata som **&quot;Hur många användare har lagt till en produkt i kundvagnen de senaste 30 dagarna&quot;**. Du kan dock skapa ett beräknat attribut i Real-Time CDP som kan förberäkna sådana värden. Dessa beräknade attribut är sedan tillgängliga i AI Assistant. Mer information finns i dokumentationen om [beräknade attribut](../../profile/computed-attributes/overview.md).

### Uppdateringar av realtidsdata

De uppskattningar som AI Assistant ger baseras på nyligen gjorda, men inte på realtidsögonblicksbilder av data. Data uppdateras var 24:e till var 48:e timme, så insikterna speglar denna fördröjning. Den här begränsningen innebär att användare inte kan ta emot ögonblickliga uppdateringar om ett segment eller en datauppsättning ändras avsevärt inom en kort tidsperiod.