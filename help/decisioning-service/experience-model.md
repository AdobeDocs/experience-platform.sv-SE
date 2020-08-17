---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Domänmodell för Experience Decisioning
topic: overview
description: I detta avsnitt förklaras komponenterna i Beslutstjänsten och hur dessa komponenter interagerar är detaljerade. Begreppen och deras relationer utgör *Domänen* för beslutsproblemet. Dessa grundläggande komponenter kan användas oavsett hur du använder beslutstjänsten].
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---


# Upplev [!DNL Decisioning] domänmodell

I det här avsnittet förklaras komponenterna i [!DNL Decisioning Service] och hur dessa komponenter interagerar. Begreppen och deras relationer utgör *domänen* för beslutsproblemet. Dessa grundläggande komponenter kan användas oavsett hur du använder dem [!DNL Decisioning Service].

## Beslutsalternativ

Ett *alternativ* för upplevelsebeslut är en potentiell upplevelse som kan presenteras för en viss kund. Ett alternativ kallas också ett val eller alternativ. När du bestämmer dig för nästa bästa alternativ för en kund [!DNL Decisioning Service] är alternativ ***d<sub>1</sub>*** till ***<sub>dN</sub>*** bland en begränsad uppsättning alternativ **`D`**.

Beslut fattas genom att det bästa alternativet identifieras bland ett antal tillgängliga alternativ. Ett tillvägagångssätt är att successivt eliminera *beslutsalternativ* ***<sub>som skiljer</sub>*** sig från ***D*** -uppsättningen tills någon av dem är kvar och sedan välja en&quot;vinnare&quot; slumpmässigt från den återstående uppsättningen. Ett annat sätt att fatta beslut är att rangordna de återstående (valbara) beslutsalternativen utifrån det förväntade resultatet.

### Finite set of Decision Options

I domänen Experience Decisioning finns det alternativ från vilka ett eller flera alternativ väljs, och när ett beslut beräknas skapas inga nya alternativ direkt. Vi säger att valmöjligheterna är oändliga när besluten fattas. Det kan verka som en begränsning, men en begränsad uppsättning alternativ ger möjlighet att använda maskininlärningsalgoritmer och liknande tekniker för att avgöra vilket av alternativen som är&quot;det bästa&quot;. Många inlärningsalgoritmer skulle inte kunna skapa ett bästa alternativ bland en uppsättning oändliga alternativ som inte kan jämföras med varandra och för vilka det inte finns några exempeldata.

## Beslutsresultat

Det är viktigt att skilja mellan beslutets resultat `d` och resultatet, `o`dvs. de avsedda resultat som angavs i beslutet. Ett beslut kan ofta inte leda till ett direkt resultat. Beslutet är endast att välja (eller föreslå) alternativet med det bästa förväntade resultatet. Mellan utkast och resultat inträffar många händelser och interaktioner, ofta fördröjda med dagar eller veckor. I mer formella termer är resultatet en funktion av beslutet `o = f(d)`.

För att hitta det optimala beslutet tilldelas varje resultat ett ***verktygsvärde*** `U(o) = U(f(d))`.
I fråga om användning vid beslut om erbjudande skulle den funktionen beräkna kostnaden för att uppfylla erbjudandet och det värde som företaget får när erbjudandet accepteras av kunden. Resultatet skulle användas för att hitta det optimala beslutet (erbjudandet) genom att maximera värdet på nyttan över alla alternativ (erbjudanden).

Det är i allmänhet inte möjligt att med säkerhet förutsäga vilka följder ett visst beslut kommer att få, och därför krävs en sannolik strategi. Det ***allmännyttiga värdet*** blir `U(o)` det ***förväntade nyttovärdet för ett beslutsalternativ*** `EU(d)`

## Beslutsförslag

Ett *beslutsförslag* är ett urval av beslutsalternativ som gjordes som svar på en faktisk begäran om beslut. Som anges ovan kan resultaten av ett beslut komma mycket senare och resultaten kanske inte heller uppnås i ett steg. Det är därför viktigt att följa upp förslagen genom olika *upplevelsehändelser* så att de kan tillskrivas beslutsalternativen. Den här feedbackslingan används för att förbättra noggrannheten i förutsägelsen för `EU(d)`.

Ett förslag bevaras som en entitet och har också en identifierare. Enheten innehåller referenser till de valda alternativen och kan registrera kontextdata som användes när beslutet fattades. Om du har en identifierare kan andra enheter referera till den. En sådan enhet är *beslutshändelse*. Den innehåller tidsstämpeln, som markerar när beslutet (förslaget) fattades. En beslutshändelse är en registrerad förekomst av åtgärden för att verkställa beslutet. Andra händelser som refererar till förslagsenheten är upplevelsehändelser. Varje upplevelsehändelse kan utvidgas till att omfatta en hänvisning till ett beslutsförslag. Tolkningen av detta är att upplevelsehändelsen helt eller delvis kan tillskrivas beslutets förslag.

## Beslutsstrategi - algoritm

Med en begränsad uppsättning alternativ att välja bland är varje *beslutsstrategi* i princip en algoritm - eller en funktion - som tar **`N`** beslutsalternativ *{d<sub>1</sub>, d<sub>2</sub>, ...<sub>dN</sub>* *<sub></sub><sub></sub><sub></sub>* }¥ som indata och skapar en rankad lista med beslutsalternativ¥(¥dr1Under, Underdr2Under,...¥drk¥)¥, där det första alternativet i listan anses optimalt enligt ett förväntat verktyg, anses det andra alternativet i resultatlistan sedan vara det näst bästa alternativet o.s.v. Vanligtvis kommer uppsättningen att ha en högre kardinalitet än den resulterande rankade listan eftersom beslutsalgoritmen tar bort alternativ som inte är berättigade och en algoritm kan konfigureras så att den bara returnerar de översta **`K`** alternativen, vilket stoppar när tillräckligt många alternativ hittas.
Den allmänna beslutsramen visas i följande diagram.

![Bild 1](./images/decisioning-optimization.png)

## Beslutsverksamhet

*Beslutsaktiviteter* konfigurerar algoritmen och leveransparametrar för en specifik beslutsstrategi. Strategiparametrarna innehåller begränsningar för alternativen och rangordningsfunktionen. Alla beslut fattas inom ramen för en aktivitet. [!DNL Decisioning Service] är värd för många aktiviteter, och aktiviteter kan återanvändas i alla kanaler. Det bästa alternativet utvärderas alltid baserat på den senaste uppsättningen begränsningar, regler och modeller.

En beslutsaktivitet definierar den samling av beslutsalternativ som ska övervägas. Den filtrerar bort deluppsättningen av alla alternativ som är av intresse för den här aktiviteten. På så sätt kan användaren [!DNL Decisioning service] hantera ämneskategorier i katalogen med alla alternativ.

En beslutsaktivitet anger ett *reservalternativ* om de kombinerade begränsningarna inte uppfyller alla andra alternativ. Det innebär att det alltid finns ett svar på frågan: Vad är för närvarande det bästa alternativet?

I beslutsverksamheterna kan det anges var upplevelsen ska genomföras. Detta minskar ytterligare antalet beslutsalternativ som kan övervägas och är en annan begränsning som beslutaktiviteten innebär. Detta kallas *placeringsbegränsning*. Endast de beslutsalternativ som har innehåll som uppfyller den här placeringsbegränsningen kommer att beaktas. Detta utvärderas i de tidiga faserna av beslutsstrategin. När definitionerna ändrar placeringsbegränsningarna för varje beslutsaktivitet omprövas och beslutsalternativet kan komma i fråga eller falla ur betydelse för en eller flera beslutsaktiviteter.

## Beslutskontext

Hittills har endast den *affärslogik* som påverkar beslutet beskrivits. Men än mer effektfullt för resultatet är de *indata* som beslutet ger. Dessa data kallas *beslutskontext* och skiljer sig åt för varje användare och varje gång ett beslut fattas, till skillnad från begränsningar, regler och modeller som är desamma för olika användare för samma aktivitet. Reglerna, begränsningarna och modellerna ändras också mindre ofta. För beslut i realtid måste beslutskontexten också bestämmas i realtid.

Data för beslutskontext kan delas in i användarprofilrelaterade data, affärsdata och internt insamlade data.

- *Profilentiteter* används för att representera slutanvändardata, men inte alla profilentiteter representerar en individ. Det kan vara ett hushåll, en samhällsgrupp eller något annat ämne. Experience-händelser är dataposter i tidsserier som är kopplade till en profil. Om det finns någon erfarenhet är dessa data *föremålet* för upplevelsen.
- Å andra sidan finns det *affärsenheterna*. De kan ses som *objekt* i interaktionen. Dessa enheter hänvisas ofta till i upplevelsehändelser för profilentiteter. Exempel på affärsenheter är webbplatser och sidor, butiker, produktinformation, digitalt innehåll, produktinventeringsdata osv.
- Den sista datakategorin i beslutskontexten är data som skapades under åtgärden av [!DNL Decisioning Service]. Varje beslutshändelse tillhör den kategorin, tillsammans med svaren från kunderna utgör förslagsinformationen en intern datauppsättning som kallas *förslagshistorik*.

Det finns tre vägar som data kan ta för att bli en del av beslutssammanhanget. Data från post- och tidsserier kan överföras via datauppsättningsfiler. Den här sökvägen används främst för gruppsynkronisering med externa system. Data från post- och tidsserier kan också strömmas till [!DNL Platform] den plats där data indexeras och kopplas till formulärentiteter. Via den tredje sökvägen kan kontextdata skickas som parametrar till beslutsbegäran. Denna form av uppgifter är av tillfällig natur och är endast relevant för det beslut som begärs. Den är inte beständig som en entitet och är inte tillgänglig för andra begäranden.
