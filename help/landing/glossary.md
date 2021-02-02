---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Adobe Experience Platform ordlista
topic: getting started
description: En ordlista med viktig terminologi i Experience Platform.
translation-type: tm+mt
source-git-commit: a7ddba7c060e809478427ef3950360ccd67e6c60
workflow-type: tm+mt
source-wordcount: '7131'
ht-degree: 0%

---


# Adobe Experience Platform-ordlista {#adobe-experience-platform-glossary}

## A

**Åtkomstkontroll**: Med rollbaserad åtkomstkontroll kan administratörer tilldela åtkomst och behörigheter till användare i Experience Platform. Behörigheter omfattar möjligheten att visa och/eller använda Experience Platform-funktioner, som att skapa sandlådor, definiera scheman och hantera datauppsättningar.

**Åtkomstnyckel-ID**: Ett åtkomstnyckel-ID är en unik identifierare som är kopplad till en  [!DNL Amazon] S3-hemlig åtkomstnyckel. Åtkomstnyckel-ID och hemlig åtkomstnyckel används tillsammans för att signera [!DNL Amazon Web Services]-begäranden (AWS).

**Åtgärd**: I  [!DNL Platform Launch]är en åtgärd en specifik typ av regelkomponent som definierar vad som ska hända efter att en händelse inträffar och villkoren utvärderas och skickas.

**Aktivera**: Aktivera är den åtgärd som en användare utför för att mappa ett segment eller profiler till ett mål som  [!DNL Oracle Eloqua],  [!DNL Google]eller  [!DNL Salesforce Marketing Cloud].

**Aktivitet**: I  [!DNL Offer Decisioning]den här aktiviteten finns den logik som används för att välja ett erbjudande.

**Administratör**: En eller flera personer i organisationen som kan konfigurera och anpassa behörigheter för Experience Platform i Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console är en central plats för hantering av Adobe produktberättiganden och åtkomst för din organisation. Via konsolen kan administratörer ge grupper av användare åtkomstbehörigheter för olika plattformsfunktioner, som Hantera datauppsättningar, Visa datauppsättningar eller Hantera profiler.

**Adobe Experience Platform**: Adobe Experience Platform standardiserar data och innehåll i hela företaget, vilket driver konsumentprofiler i realtid, möjliggör datavetenskap och snabbar upp innehållets hastighet för att driva upplevelsepersonalisering över hela kundresan.

**Adobe Experience Platform Launch**:  [!DNL Platform Launch] är ett tagg- och SDK-hanteringssystem som är integrerat med Experience Platform och  [!DNL Experience Cloud] program. [!DNL Platform Launch] innehåller verktyg för att driftsätta, sammanställa och hantera analyser, marknadsföring och annonser som är nödvändiga för att driva relevanta kundupplevelser på alla kundenheter.

**Adobe Experience Platform Query Service**: Gör det möjligt för dataanalytiker att fråga efter händelser och profiler för användning i analyser och maskininlärning. Med Query Service kan datavetare och analytiker hämta alla sina datauppsättningar som lagras i Experience Platform (inklusive beteendedata och POS (Point-of-Sale), CRM (customer relationship management) med mera) och fråga dessa datauppsättningar för att få svar på specifika frågor om data.

**Adobe Experience Platform segmenteringstjänst**: Gör det möjligt att bygga segment och generera målgrupper från kundprofildata i realtid. Dessa målgrupper kan sedan exporteras till sina egna datamängder inom Data Lake.

**Adobe Intelligent Services**: Intelligenta tjänster som Attribution AI och kundens AI är maskininlärningsmodeller baserade på artificiell intelligens som är specialbyggda och kräver att Experience Platform fungerar och fungerar.

**Adobe I/O**: Adobe I/O ingår i Experience Platform och ger tillgång till allt utvecklare behöver för att integrera, utöka och anpassa plattformen, inklusive API:er, händelser, utvecklarkonsolen och praktiska verktyg.

**Adobe Sensei**: Adobe Sensei är intelligensramverket som ligger till grund för Experience Platform. Det innehåller också en uppsättning AI-tjänster som ger varumärken möjlighet att förbättra sin förmåga att leverera personaliserade kundupplevelser i realtid.

**Amazon S3-bucket**:  [!DNL Amazon S3] bucket är de grundläggande behållarna för data som lagras i  [!DNL Amazon] ekosystemet. Bucket innehåller objekt. Varje objekt lagras och hämtas med en unik utvecklartilldelad nyckel.

**Amazon S3-anslutning**: Med  [!DNL Amazon] S3-kontakten kan Experience Platform-kunder ansluta och komma åt sina  [!DNL Amazon] S3-data på ett säkert sätt.

**Lägg till sparstrategi**: Spara-strategin&quot;append&quot; är ett alternativ som används när du anger data från tredje part som ska importeras via en anslutning och lägger till nya data eller rader i slutet av datauppsättningen. De tidigare infogade raderna förblir orörda och endast rader som skapats sedan den senaste schemalagda körningen importeras till Experience Platform. Eventuella rader som har ändrats i källsystemet ändras inte i Experience Platform.

**Array**: Arrayer används för ordnade element med samma datatyp.

**Artificiell intelligens**: Artificiell intelligens är en teori om och utveckling av datorsystem som kan utföra uppgifter som normalt kräver mänsklig omvärldsbevakning, t.ex. visuell uppfattning, taligenkänning, beslutsfattande och översättning mellan språk.

**Attribut**: Attribut är angivna egenskaper som representerar en profil.

**Koppla** attribut: När du definierar en sammanfogningsprincip med hjälp av API:t för kundprofil i realtid, anger  `attributeMerge` objektet hur sammanfogningsprincipen ska prioritera profilattribut vid datakonflikter. Det motsvarar att välja en [!UICONTROL Merge method] när du definierar en sammanfogningsprincip i plattformsgränssnittet.

**Attribution AI**:  [!DNL Attribution AI] är en intelligent tjänst från Adobe Sensei som levererar algoritmiska flerkanalsattribueringsfunktioner under hela kundlivscykeln.

**Målgrupp**: En målgrupp är den resulterande uppsättningen profiler som uppfyller villkoren i en segmentdefinition.

**Målgruppsstorlek**: En målgruppsstorlek är det totala antalet profiler som uppfyller villkoren i en segmentdefinition och som är kvalificerade för medlemskap i målgruppen.

**Målgruppsbild**: En målgruppsbild fångar upp alla profiler som uppfyller villkoren vid tidpunkten för segmenteringen.

## B

**Backfill**: För schemalagda källor möjliggör alternativet för efterfyllnad inmatning av historiska data.

**Föråldringsperiod**: Förifyllningsperioden är ett alternativ för att ange hur lång tid det tar att hämta historikdata från tredje part via en källanslutning. Om du väljer att fylla i för alltid kommer källdatans hela historik att importeras till Experience Platform.

**Grupp**: En batch är en uppsättning data som samlats in under en tidsperiod och som bearbetas tillsammans som en enda enhet. Datauppsättningar består av flera grupper.

**Batch-ID**: Ett batch-ID är en Adobe-genererad identifierare för en datauppsättning.

**Batchförtäring**: Med batchöverföring kan du importera data till Experience Platform som gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet.

**Gruppsegmentering**: Gruppsegmentering är ett alternativ till en pågående dataurvalsprocess och flyttar alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När segmentet har skapats sparas det och lagras så att det kan exporteras för användning.

**Bygg**: I  [!DNL Platform Launch]är en bygge en fil eller en uppsättning filer som innehåller alla konfigurationer och all kod som behövs för att köra affärslogiken i ett bibliotek, så att du kan distribuera biblioteket på din webbplats eller i din mobilapp.

**Business Intelligence-verktyg**: Business Intelligence-verktyg (BI) är i första hand integrerade med  [!DNL Experience Platform Query Service]. BI-verktyg är typer av programprogramvara som samlar in och bearbetar stora mängder ostrukturerade data från interna och externa system.

## C

**Takning**: I  [!DNL Offer Decisioning]det här fallet används capping (även kallat frekvenscapping) i beslutsreglerna för att definiera hur många gånger ett erbjudande presenteras. Det finns två typer av versaler: hur många gånger ett erbjudande kan föreslås för den kombinerade målgruppen (kallas&quot;Global Cap&quot;) och hur många gånger ett erbjudande kan föreslås för samma slutanvändare (kallas&quot;Profile Cap&quot;).

**Katalog**: När det gäller källor och destinationer är en katalog ett galleri med tillgängliga kopplingar till Adobe-program och tredjepartstekniker. Ska inte blandas ihop med [!DNL Catalog Service].

**[!DNL Catalog Service]**:  [!DNL Catalog Service] (kallas ibland  [!DNL Catalog]) är arkivsystemet för dataplatser och -länkar inom Adobe Experience Platform. Alla data som importeras till Experience Platform lagras i datarjön som filer och kataloger, men [!DNL Catalog] innehåller metadata och beskrivning av dessa filer och kataloger för sökning, övervakning och datastyrning.

**Klass**: I Experience Data Model (XDM) definierar en klass den minsta uppsättning fält som används för att skapa ett schema och definierar basbeteendet för det affärsobjekt som schemat representerar.

**Klient**: En klient är ett externt verktyg eller program som ansluter till  [!DNL Query Service] via PostgreSQL-protokoll eller HTTP API.

**Samling**: I  [!DNL Offer Decisioning]det här fallet är samlingar delmängder av erbjudanden som baseras på fördefinierade villkor som definieras av en marknadsförare, t.ex. erbjudandets kategori.

**Kombinera med PII-marknadsföringsåtgärder**: En marknadsföringsåtgärd som kombinerar personligt identifierbar information (PII) med anonyma data. Kontrakt för data som hämtas från annonsnätverk, annonsservrar och tredjepartsleverantörer av data innehåller ofta särskilda avtalsförbud för användning av sådana data med direkt identifierbara data.

**Kommandoradsgränssnitt**: Ett kommandoradsgränssnitt är ett textbaserat verktyg som kan användas för att ansluta till  [!DNL Query Service] för körning av raw-frågor.

**Disposition**: En komposition är en gruppering av komponenter som bildar tillsammans för att bilda schemat.

**Villkor**: I  [!DNL Platform Launch]är ett villkor en regelkomponent som utvärderar en logisk programsats som måste returneras  `true` eller  `false`. Alla villkor måste utvärderas till `true` och alla undantagsvillkor måste utvärderas till `false` innan några åtgärder i regeln körs.

**Konsol**: I  [!DNL Query Service]konsolen finns information om status och funktion för en fråga. Konsolen visar anslutningsstatusen till [!DNL Query Service], frågeåtgärder som körs och eventuella felmeddelanden som kommer från dessa frågor.

**Kontraktsetiketter**: Dataanvändningsetiketter för kontrakt (&quot;C&quot;) används för att kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till en kunds datastyrningspolicy.

**C1-kontraktsetikett**: En etikett för  `C1` avtalsdataanvändning anger att data bara kan exporteras från Adobe Experience Cloud i en aggregerad form utan att det inkluderar individuella identifierare eller enhetsidentifierare. Till exempel data som kommer från sociala nätverk.

**C2-kontraktsetikett**: En etikett för  `C2` avtalsdataanvändning anger data som inte kan exporteras till en tredje part. Vissa dataleverantörer har villkor i sina kontrakt som förbjuder export av data som de ursprungligen samlades in från. Kontrakt för sociala nätverk begränsar till exempel ofta överföringen av data som du får från dem. C2 är mer restriktiv än C1, som bara kräver aggregation och anonyma uppgifter.

**C3-kontraktsetikett**: En etikett för  `C3` avtalsdataanvändning anger data som inte kan kombineras eller på annat sätt användas med direkt identifierbar information. Vissa dataleverantörer har villkor i sina kontrakt som förbjuder kombinationen eller användningen av dessa data med direkt identifierbar information. Till exempel innehåller kontrakt för data som hämtas från annonsnätverk, annonsservrar och tredjepartsleverantörer av data ofta specifika avtalsförbud för användning av direkt identifierbara data.

**C4-kontraktsetikett**: En etikett för  `C4` avtalsdataanvändning anger att data inte kan användas för annonsering eller innehåll, antingen på plats eller på en annan plats. C4 är den mest restriktiva etiketten eftersom den omfattar etiketterna C5, C6 och C7.

**C5-kontraktsetikett**: En etikett för  `C5` avtalsdataanvändning anger att data inte kan användas för målinriktning mellan webbplatser för intressebaserat innehåll eller annonser. Intressebaserad målinriktning, eller personalisering, uppstår om följande tre villkor uppfylls: De uppgifter som samlas in på plats används för att dra slutsatser om en användares intresse. används i ett annat sammanhang, t.ex. på en annan webbplats eller i en annan app, och används för att välja vilket innehåll eller vilka annonser som ska visas baserat på dessa slutsatser.

**C6-kontraktsetikett**: En etikett för  `C6` avtalsdataanvändning anger att data inte kan användas för annonsanpassning på plats. Annonsanpassning på plats omfattar val och leverans av annonser på organisationens webbplatser eller i appar eller för att mäta hur effektiva dessa annonser är och hur de levereras. Detta inkluderar att använda tidigare insamlade data på plats om användarnas intresse för att välja annonser, bearbeta data om vilka annonser som visades, när och var de visades och om användarna vidtagit några åtgärder som rör annonsen, som att välja en annons eller göra ett köp.

**C7-kontraktsetikett**: En etikett för  `C7` avtalsdataanvändning anger att data inte kan användas för att målinrikta innehåll på plats. Med målinriktning mot innehåll på plats kan du välja och leverera innehåll på organisationens webbplatser, eller i appar eller mäta hur effektivt innehållet levereras. Detta inkluderar tidigare insamlad information om användarnas intresse av att välja innehåll, bearbetning av data om vilket innehåll som visades, hur ofta eller hur länge det visades, när och var det visades, och om användarna vidtagit några åtgärder som rör innehållet, till exempel att välja innehåll.

**C8-kontraktsetikett**: En etikett för  `C8` avtalsdataanvändning anger att data inte kan användas för att mäta organisationens webbplatser eller appar. Detta inkluderar inte intressebaserad målinriktning, som är insamling av information om din användning av den här tjänsten för att senare personalisera innehåll och/eller annonsering i andra sammanhang.

**C9-kontraktsetikett**: En etikett för  `C9` avtalsdataanvändning anger att data inte kan användas i arbetsflöden för datavetenskap. Vissa avtal innehåller uttryckliga förbud mot data som används för datavetenskap. Ibland formuleras dessa i termer som förbjuder användning av data för artificiell intelligens (AI), maskininlärning (ML) eller modellering.

**C10 kontraktsetikett**: En etikett för användning av  `C10` avtalsdata anger att data inte kan användas för aktivering av sammanfogade identiteter. Vissa dataanvändningsprinciper begränsar användningen av sammanfogade identitetsdata för personalisering. `C10`-etiketten används automatiskt för segment om deras sammanfogningsprinciper använder alternativet &quot;privat diagram&quot;.

**Skapad den-kolumn**: Du kan välja en kolumn med skapat datum när du anger data från tredje part via en källanslutning. När strategin för att spara som tillägg har valts och datauppsättningsschemat innehåller flera datumfält, måste du välja från det tillgängliga schemat för att ange en nyckelkolumn för Skapat den. Alternativet Skapat den är inte tillgängligt när du har valt en sparningsstrategi för överskrivning.

**Skapa tabell som markerad**: Skapa tabell som markerad (CTAS) är ett SQL-kommando som, när det körs som en del av en fullständig och giltig SQL-fråga, instruerar  [!DNL Query Service] att behålla frågeresultatet i en datauppsättning. Du kan skapa en ny resultatuppsättning, skriva över tidigare resultat eller lägga till i tidigare resultat.

**Data** på olika webbplatser: Data på olika platser är en kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera externa källor.

**Marknadsföringsåtgärder** för flera webbplatser: En marknadsföringsåtgärd som använder data för annonsanpassning mellan webbplatser. En kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera källor utanför platsen, kallas data mellan olika platser. Data från olika webbplatser samlas vanligtvis in och behandlas för att man ska kunna dra slutsatser om kundernas intressen.

**Namnutrymme** för anpassad identitet: Anpassade identitetsnamnutrymmen kan skapas av din organisation för att representera identiteter för en viss organisation eller ett visst affärsfall.

**Egna etiketter**: Med anpassade etiketter för dataanvändning kan du skapa och använda specifika etiketter för datafält som uppfyller specifika affärsbehov.

**Kund-AI**: Kundens AI är en intelligent tjänst som drivs av Adobe Sensei och som berikar kundprofiler med AI-baserade egenskaper och ger bättre kundsegmentering och målgruppsinriktning.

## D

**Dataordlista**: I  [!DNL Platform Launch]är ett datalexikon (kallas även datamappning) en uppsättning dataelement som definieras i en egenskap.

**Dataelement**: Ett dataelement  [!DNL Platform Launch]är en pekare som används i regler och tillägg för att peka på en viss datadel som finns på klientenheten.

**Intag** av data: Intag av data är processen att lägga till data från en källa till Experience Platform. Data kan hämtas in till plattformen på flera olika sätt, inklusive strömning, batchar eller läggas till via källanslutningar.

**Datalager**: I  [!DNL Platform Launch]det här fallet är ett datalager en datastruktur som finns på klientenheten och som innehåller metadata om i vilket sammanhang en sida eller skärm visas.

**Datastyrning**: Datastyrning omfattar strategier och tekniker som används för att säkerställa att data överensstämmer med regler och organisationsstrategier när det gäller dataanvändning.

**Partners** för dataintegrering: Dataintegrationspartners förenklar och automatiserar inläsningen och omvandlingen av stora datavolymer från över 200 källor till Experience Platform utan att behöva skriva kod.

**Datauppsättningsrubriker**: Dataanvändningsetiketter kan läggas till i datauppsättningar. Alla fält i den datauppsättningen ärver datauppsättningens etiketter.

**Data Science Workspace**:  [!DNL Data Science Workspace] på Experience Platform kan man skapa maskininlärningsmodeller med data från olika plattformar och Adobe för att skapa intelligenta segment, generera insikter och förutse, vilket gör att man kan förbättra slutanvändarnas digitala upplevelser avsevärt.

**Datakälla**: En datakälla är en användardefinierad utgångspunkt för data. Exempel på en datakälla är en mobilapp, en profil och/eller upplevelsehändelser, webbplatsprofilhändelser eller en CRM.

**Stega** data: En dataförvaltare är den person som ansvarar för förvaltning, tillsyn och verkställighet av en organisations datatillgångar. En dataförvaltare säkerställer också att policyer för datastyrning skyddas och upprätthålls så att de överensstämmer med myndighetsbestämmelser och organisationsprofiler.

**Dataström**: En dataström är en uppsättning eller en samling meddelanden som delar samma schema och skickas av samma källa.

**Datatyp**: En datatyp är en återanvändbar XDM-resurs som definierar ett objekttypsfält som innehåller flera egenskaper i en hierarkisk representation.

**Dataanvändningsetiketter**: Med etiketter för dataanvändning kan ni kategorisera data som återspeglar integritetsrelaterade överväganden och avtalsvillkor så att de uppfyller regler och företagspolicyer. Dataanvändningsetiketter som läggs till i en datauppsättning ärvs ned eller används för alla fält i den datauppsättningen. Dataanvändningsetiketter kan också användas direkt i fält.

**Dataflöde**: Ett dataflöde är en virtuell pipeline med data som flödar in i plattformen från en källa och ut till mål.

**Dataflödeskörning**: En dataflödeskörning är ett dataflöde som körs i Experience Platform baserat på ett användarspecificerat schema.

**Datauppsättning**: En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader).

**Datauppsättnings-ID**: En Adobe-genererad identifierare för en inkapslad datauppsättning.

**Datauppsättningsutdata**: Datauppsättningsutdata är en mekanism för att avgöra vad alternativet Skapa tabell som markerad ska användas för en viss  [!DNL Query Service] körning.

**Delta-kolumn**: Med en delta-kolumn kan du välja ett källdatafält som representerar en tidsstämpel för inkrementellt intag.

**Delta-sparstrategi**: Deltasparstrategin är ett alternativ för att hämta tredjepartsdata via en källanslutning. Med det här alternativet kan användaren ange att nya eller ändrade rader med källdata hämtas till Experience Platform. Nya rader läggs till i slutet av datauppsättningen och ändrade rader uppdateras i datauppsättningen på Experience Platform.

**Beskrivning**: I Experience Data Model (XDM) är en beskrivning en extra uppsättning schemarelaterade metadata som beskriver ett specifikt beteende för ett fält. Beskrivningar kan användas av Experience Platform för att förstå avsedd schemabeteende, som relationen mellan två scheman.

**Mål**: Ett mål är en allmän term för alla slutpunkter, till exempel ett Adobe-program, en annonsplattform, molnlagringstjänst eller marknadsföringstjänst, där en målgrupp aktiveras och levereras.

**Målkategori**: En destinationskategori är en gruppering av destinationer som har liknande egenskaper.

**Målkatalog**: En destinationskatalog är en lista över tillgängliga destinationer i Experience Platform.

**Regler** för direktsamtal: I  [!DNL Platform Launch]det här fallet är en regel för direktanrop en regel som körs när den anropas direkt från sidan, utan att händelsidentifierings- och uppslagssystemen åsidosätts.

**Visningsnamn**: I Experience Data Model (XDM) är ett visningsnamn ett användarvänligt namn för ett fält som visas i användargränssnittet.

## E

**Berättigat erbjudande**: Ett valbart erbjudande kan alltid erbjudas till en profil, eftersom det uppfyller de krav som anges ovan.

**Villkor**: I  [!DNL Offer Decisioning]används berättiganderegler för en profil som är relaterad till kalendern, schemat och begränsningsbegränsningar.

**Marknadsföringsåtgärd** för e-postmarknadsföring: En marknadsföringsåtgärd som använder data i e-postriktade kampanjer.

**Bädda in kod**: I  [!DNL Platform Launch]är inbäddningskoden en script-tagg som placeras i HTML-koden på en plats eller i en miljö. Inbäddningskoden instruerar webbläsaren var bygget ska hämtas.

**Uppräkning**: En uppräkning (uppräkning) är ett XDM-fält som begränsas till en uppsättning fördefinierade värden.

**Miljö**: I  [!DNL Platform Launch]är en miljö en uppsättning distributionsinstruktioner som anger värdleveransen och filformatet för ett bygge. Ett bibliotek måste kombineras med en miljö innan det kan byggas.

**Feldiagnostik**: Feldiagnostik möjliggör generering av detaljerade felmeddelanden för kapslade batchar. Med feltröskeln kan du konfigurera procentandelen godtagbara fel innan en batch misslyckas.

**Händelse**: I  [!DNL Platform Launch]är en händelse en specifik typ av regelkomponent, som är en utlösare som inträffar på en klientenhet för att börja köra en regel.

**Händelseentiteter**: När det gäller datamodellering representerar händelseenheter koncept som relaterar till åtgärder som en kund kan vidta, systemhändelser eller andra koncept där du kan vilja spåra ändringar över tid. Enheter som tillhör den här kategorin ska representeras av scheman baserade på klassen [!DNL XDM ExperienceEvent].

**Händelser**: Händelser är de beteendedata som är associerade med en profil.

**Experience Data Model (XDM)** [!DNL Experience Data Model]  (XDM) är ett ramverk med öppen källkod som använder standardscheman för att sammanställa data för användning med Experience Platform och Adobe Experience Cloud-program. XDM standardiserar hur data struktureras och snabbar upp och förenklar processen att få insikter från enorma mängder data.

**Experimentera**: Ett experiment är processen att skapa en utbildad modell genom att utbilda instansen med en exempeldel av data om produktion. Detta skiljer sig från en tränad modell som testas mot en testdatamängd för utelämnande. Detta skiljer sig också från konceptet med ett experiment i vissa maskininlärningsmiljöer där det i själva verket handlar om ett exempelmodelleringsprojekt.

**Experience Event**: En Experience Event representerar en ögonblicksbild av systemet när en interaktion eller händelse som rör en kundupplevelse inträffar. Experience Events är oföränderliga fakta om vad som hänt och representerar vad som hänt utan aggregering eller tolkning. I Experience Data Model (XDM) fångas det här konceptet av klassen [!DNL XDM ExperienceEvent].

**Tillägg**: I  [!DNL Platform Launch]är ett tillägg ett paket med funktioner som lagts till i en  [!DNL Platform Launch] egenskap. Ett tillägg är vanligtvis inriktat på en viss marknadsförings- eller analyslösning och innehåller de verktyg som behövs för att driftsätta tekniken i en klientmiljö.

**Tilläggspaket**: I  [!DNL Platform Launch]är ett tilläggspaket en ZIP-fil som skapas och överförs av en tilläggsutvecklare och som innehåller allt som  [!DNL Platform Launch] användarna behöver för att installera tillägget i sin egenskap. Ett tilläggspaket innehåller ett manifest som anger information om tillägget, den HTML/JavaScript som behövs för att slutanvändarna ska kunna konfigurera beteendet för tillägget [!DNL Platform Launch] och den körbara JavaScript som levereras till klientmiljön (om det behövs).

## F

**Reserverbjudanden**: Ett reserverbjudande är standarderbjudande som visas när en slutanvändare inte är berättigad till något av erbjudandena i den mängd som används.

**Funktionsmappning**: Funktionsmappning avser processen att mappa funktioner från data till indata- och målfunktioner som krävs av en maskininlärningsmodell.

**Fält**: Ett fält är det lägsta nivåelementet i en datauppsättning, enligt definitionen i datauppsättningens XDM-schema. Varje fält har ett namn för referensändamål och en typ som anger vilken typ av data det innehåller. Fälttyper kan innehålla (men är inte begränsade till) heltal, tal, sträng, booleskt värde och objekt.

**Fältetiketter**: Fältetiketter är datastyrningsetiketter som antingen ärvs från en datamängd eller tillämpas direkt på ett fält.

**Fältnamn**: Ett fältnamn används för att referera till värdet för ett fält i frågor och underordnade tjänster.

**Frekvens**: I  [!DNL Query Service]bestämmer frekvensen hur ofta en återkommande schemalagd fråga ska köras.

## G

**Geofence**: En geofence är en virtuell geografisk gräns, som definieras av GPS- eller RFID-teknik, som gör att programvara kan utlösa ett svar när en mobil enhet kommer in i eller lämnar ett visst område.

**GDPR (General Data Protection Regulation)**: Den allmänna dataskyddsförordningen (GDPR) är en rättslig ram som fastställer riktlinjer för insamling och behandling av personuppgifter inom EU. Den allmänna dataskyddsförordningen fastställer principerna för datahantering och individens rättigheter och omfattar alla företag som hanterar EU-medborgarnas uppgifter.

## H

**Värd**: I  [!DNL Platform Launch]anger en värd den plats, domän och de användarautentiseringsuppgifter som krävs för  [!DNL Platform Launch] att leverera ett bygge.

## I

**Identitet**: En identitet är en identifierare som unikt representerar en enskild kund, till exempel ett cookie-ID, ett enhets-ID eller ett e-post-ID.

**Identitetsfält**: Identitetsfält är XDM-fält som används för att sammanfoga information om enskilda kunder som kommer från flera datakällor. En primär identitet måste definieras för att schemat ska kunna aktiveras för användning i kundprofilen i realtid.

**Identitetsetiketter** (&quot;I&quot;): Etiketter för identitetsanvändning (&quot;I&quot;) används för att kategorisera data som kan identifiera eller kontakta en viss person.

**Identitetsdiagram**: Ett identitetsdiagram är en karta över relationer mellan sammanfogade och länkade identiteter som finns för en enskild kund. Varje identitetsdiagram uppdateras i nära realtid med kundaktivitet. Den gemensamma strukturen för identitetsrelationer i dina data representeras av [!UICONTROL Private Graph], som fungerar som en strukturell plan för varje enskilt identitetsdiagram.

**Identitetsnamnutrymme**: Ett identitetsnamnutrymme definierar kontexten för en identifierare, till exempel en e-postadress eller ett CRM-ID.

**Identitetstjänst**:  [!DNL Experience Platform Identity Service] gör det möjligt att skapa och hantera identitetstyper, så att ni kan länka samman kundidentiteter mellan olika enheter och kanaler. Tjänstens förmåga att länka samman identiteter gör det möjligt för kundprofiler i realtid att tillhandahålla en fullständig representation av varje enskild kund.

**Häftning** av identitet: Identitetssammanfogning är processen att identifiera databragment och sammanfoga dem till en fullständig profilpost.

**Identitetssymbol**: En identitetssymbol är en förkortning av ett identitetsnamnutrymme som kan användas som referens i API:er.

**Identitetsvärde**: Ett identitetsvärde i kombination med ett identitetsnamnutrymme är en identifierare som representerar en unik individ, organisation eller resurs. När postdata matchas mellan profilfragment måste namnutrymmet och identitetsvärdet matcha.

**Etikett** för dataanvändning i1: Etiketten för  `I1` dataanvändning används för att klassificera data som direkt kan identifiera eller kontakta en viss person i stället för en enhet.

**Etikett** för användning av I2-data: Etiketten för  `I2` dataanvändning används för att klassificera data som kan användas i kombination med andra data för att indirekt identifiera eller kontakta en viss person.

**IMS-organisation**: En IMS-organisation (kallas ibland IMS-organisation) är det namn som används för att identifiera ett företag eller en viss grupp inom ett företag mellan olika Adobe-produkter. Administratörer kan konfigurera och hantera åtkomst och behörigheter för funktioner för användare i en organisation.

**Inmatning**: Se dataintag.

**Inmatningsschema**: Ett intag-schema ger tidsbaserade alternativ när man ska äta från en källa till Experience Platform.

**Indatafunktion**: En inmatningsfunktion anges i funktionsmappningen och används av en maskininlärningsmodell för att göra prognoser.

**[!DNL Intelligent Services]**:  [!DNL Intelligent Services] som  [!DNL Attribution AI] och  [!DNL Customer AI] är maskininlärningsmodeller som bygger på artificiell intelligens och som kräver att Experience Platform (eller program som är byggda ovanpå plattformen, t.ex. kunddataplattformen i realtid) körs och fungerar.

**Intressebaserad målinriktning eller personalisering**: Intressebaserad målinriktning, som också kallas personalisering, uppstår om följande tre villkor uppfylls:

1. Data som samlas in på plats används för att dra slutsatser om en användares intresse.
1. Data används i ett annat sammanhang, till exempel på en annan webbplats eller i en annan app (utanför webbplatsen).
1. Data används för att välja vilket innehåll eller vilka annonser som ska hanteras baserat på dessa slutsatser.

## J

**[!DNL JupyterLab]**: Ett webbaserat gränssnitt för Project med öppen källkod  [!DNL Jupyter] som är integrerat i användargränssnittet för plattformen.

**[!DNL Jupyter Notebook]**: Jupyter Notebooks är integrerade med JupyterLab och gör det möjligt att rensa och omvandla data, numerisk simulering, statistisk modellering, datavisualisering, maskininlärning med mera på dina Experience Platform-data på en rad olika språk som Python, Scala och PySpark.

## K

## L

**Bibliotek**: I  [!DNL Platform Launch]är ett bibliotek en uppsättning affärslogik som innehåller instruktioner för hur  [!DNL Platform Launch] biblioteket ska fungera på klientenheten.

**Sökentiteter**: I samband med datamodellering representerar sökenheter koncept som kan relatera till en enskild person, men som inte kan användas direkt för att identifiera den enskilda personen. Enheter som tillhör den här kategorin ska representeras av scheman som baseras på anpassade XDM-klasser (Experience Data Model).

## M

**Maskinininlärning (ML)**: Maskininlärning är det studieområde där datorer kan lära sig utan att programmeras explicit.

**Maskininlärningsmodell**: En maskininlärningsmodell är en instans av ett maskininlärningsrecept som har utbildats med hjälp av historiska data och konfigurationer för att lösa ett affärsärende. I Adobe Experience Platform Data Science Workspace kallas maskininlärningsmodeller recept.

**Mappning**: Datamappning är processen att mappa källdatafält till relaterade målfält i ett mål.

**Marknadsföringsåtgärd**: I datastyrningsramverket är en marknadsföringsåtgärd (även kallat marknadsföringsfall) en åtgärd som en datakonsument utför på Experience Platform, och där det finns ett behov av att kontrollera överträdelser av dataanvändningspolicyer.

**Sammanfogningsmetod**: När du definierar en sammanfogningsprincip med hjälp av plattformsgränssnittet anger sammanfogningsmetoden hur datafel ska prioriteras när en konflikt uppstår. När du använder Real-time Customer Profile API för att definiera en sammanfogningsprincip, bestäms sammanfogningsmetoden med objektet `attributeMerge`.

**Kopplingsprincip**: Sammanslagningsprinciper är regler som Experience Platform använder för att avgöra hur kunddatafragment från flera källor kombineras för att skapa en enskild profil. När en datakonflikt inträffar avgör sammanfogningsprincipen vilka data som ska prioriteras för att inkluderas i profilen.

**Blandning**: I Experience Data Model (XDM) ger en blandning användare möjlighet att utöka återanvändbara fält för att definiera ett eller flera attribut som ska ingå i ett schema.

**Modul**: I  [!DNL Platform Launch]är en modul ett fragment av körbar JavaScript som tillhandahålls av ett tillägg, som utför åtgärder i en klientmiljö utan att behöva skapa en regel.

## N

**Icke-produktionssandlåda**: Sandlådor som inte är produktionssandlådor är sandlådor som vanligtvis används för utvecklingsexperiment, testning och testning. Till skillnad från produktionssandlådor kan icke-produktionssandlådor återställas och tas bort.

**[!DNL Notebooks]**:  [!DNL Notebooks] skapas med  [!DNL Jupyter Notebook] och kan köras för att utföra dataanalys.

## O

**Erbjudande**: Ett erbjudande är ett marknadsföringsmeddelande som innehåller ett företags- eller säljförslag till en (potentiell) kund. Erbjudandena har ofta särskilda regler som avgör vem som är berättigad att se eller ta emot dem.

**[!DNL Offer Decisioning]**:  [!DNL Offer Decisioning] gör det möjligt för marknadsförare att hantera regler och tränade modeller för erbjudandeförslag när de interagerar med slutanvändare baserat på data som samlats in över olika kanaler och tillämpningar.

**Erbjudandebibliotek**: Erbjudandebiblioteket är ett centralt bibliotek som används för att hantera personaliserade erbjudanden och reserverbjudanden, beslutsregler och aktiviteter.

**Marknadsföringsåtgärd** för personalisering på plats: En marknadsföringsåtgärd som använder data för innehållspersonalisering på plats. Webbplatspersonalisering är alla data som används för att dra slutsatser om användarnas intressen och används för att välja vilket innehåll eller vilka annonser som ska hanteras baserat på dessa slutsatser.

**Marknadsföringsåtgärder** för riktad marknadsföring på plats: En marknadsföringsåtgärd som använder data för annonser på plats, inklusive urval och leverans av annonser på organisationens webbplatser eller appar, eller för att mäta leveransen och effektiviteten av sådana annonser.

**Skriv över sparstrategi**: Spara-strategin&quot;Skriv över&quot; är ett alternativ för att hämta tredjepartsdata via en anslutning, där du kan ange om inmatade data ska skrivas över enligt ett angivet schema.

## P

**Delvis intag**: Delvis förtäring möjliggör förtäring av giltiga poster med batchdata inom ett angivet feltröskelvärde. Feldiagnostik för misslyckade poster kan hämtas eller nås i en översikt över dataflödeskörningen i [!UICONTROL Monitoring] eller [!UICONTROL Sources].

**Parquet-filer**: En Parquet-fil är ett kolumnlagringsfilformat med komplexa kapslade datastrukturer. Parquet-filer krävs för att lägga till data för att fylla i en schemadatauppsättning.

**Personaliserade erbjudanden**: Ett personaliserat erbjudande är ett anpassningsbart marknadsföringsmeddelande som baseras på regler och begränsningar för behörighet.

**Placeringar**: En placering är den plats och/eller det sammanhang där ett erbjudande visas för en slutanvändare.

**Arbetsytan** Profiler: En arbetsyta i användargränssnittet för plattformen som gör det möjligt för dataförvaltare att visa och hantera etiketter och policyer för dataanvändning för din organisation.

**Princip**: En dataanvändningspolicy är en regel som anger marknadsföringsåtgärder som är begränsade baserat på användningen av användningsetiketter som används på plattformsdata.

**Politiska åtgärder**: Gör att ni kan tillämpa dataanvändningspolicyer med tillämpade marknadsföringsåtgärder för att förhindra dataåtgärder som utgör policyöverträdelser inom en organisation.

**Primärnyckel**: En primärnyckel är en beteckning i ett schema som unikt identifierar alla poster.

**Prioritet**: Prioriteten  [!DNL Offer Decisioning]används för att rangordna erbjudanden som uppfyller alla krav, som berättigande, kalender och appning.

**Privat identitetsdiagram**: Det privata identitetsdiagrammet (kallas ibland för ett privat diagram) är en privat karta över relationer mellan sammanfogade och länkade identiteter som bygger på dina egna data och som bara är synlig för din organisation. Det finns bara ett privat diagram för varje organisation och det fungerar som en strukturell plan för de enskilda identitetsdiagram som genereras för varje kund och som interagerar med ert varumärke.

**Produktprofil**: Med produktprofiler kan administratörer ge användare åtkomst till alla eller en delmängd av tjänster som är kopplade till Experience Platform.

**Produktionssandlåda**: En produktionssandlåda är en sandlåda som är avsedd att användas i din produktionsmiljö. Till skillnad från icke-produktionssandlådor kan produktionssandlådor inte återställas eller tas bort.

**Profil**: En profil är en fullständig representation av en enskild kund, som bygger på sammanfogade data från olika källor och tidsseriedata, och ska inte blandas ihop med kundprofilen i realtid som en tjänst.

**Profilåtkomst**: Med  `/entities` slutpunkten i kundprofils-API:t i realtid kan du komma åt postdata och tidsseriehändelser i profildatalagret. Se även: Profilenheter

**Profildata**: Profildata avser alla data som finns i profildatalagret.

**Profildatalager**: Profildatalagret (kallas ibland profilarkivet) är ett datalagringssystem som är skilt från datasjön och som används av kundprofilen i realtid för att skapa och lagra profiler.

**Profilentiteter**: Profilenheter representerar attribut som relaterar till en enskild person, vanligtvis en kund. Enheter som tillhör den här kategorin ska representeras av scheman baserade på klassen [!DNL XDM Individual Profile]. Se även: Profilåtkomst

**Profilexport**:  [!DNL Profile] exporten är en av de två destinationstyperna i Experience Platform. [!DNL Profile] vid export genereras en fil som innehåller profiler och attribut, och obearbetade PII-data används med e-post för att integreras med marknadsförings- och e-postautomatiseringsplattformar.

**Profilfragment**: Ett profilfragment är profilinformationen för endast en identitet från listan över identiteter som finns för en viss kund.

**Profil-ID**: Ett profil-ID är en automatiskt genererad identifierare som är associerad med en identitetstyp och representerar en profil.

**Egenskap**: I  [!DNL Platform Launch]är en egenskap en behållare för allt som behövs för att distribuera en uppsättning taggar.

## Q

**Fråga**: Frågor är förfrågningar om data från databastabeller.

**Frågeredigeraren**: Frågeredigeraren är ett verktyg för att skriva, validera och skicka SQL-satser i  [!DNL Query Service].

## R

**Kunddataplattform** i realtid:  [!DNL Real-time Customer Data Platform] sammanför kända och okända kunddata för att skapa tillförlitliga kundprofiler med förenklad integrering, intelligent segmentering och realtidsaktivering under hela den digitala kundresan.

**Kundprofil** i realtid: Kundprofil i realtid (kallas ibland profil) ger en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. Med en profil kan ni sammanställa kunddata i enskilda profiler som erbjuder åtgärdbara, tidsstämplade konton för varje kundinteraktion.

**Mottagare**: Ett recept är en Adobe term för en modellspecifikation och är en behållare på den översta nivån som representerar specifika maskininlärningsprocesser, AI-algoritmer, bearbetningslogik och konfigurationsparametrar som krävs för att skapa och köra en utbildad modell och därmed bidra till att lösa specifika affärsproblem.

**Post**: En post är data som kvarstår som rader i en datauppsättning.

**Postdata**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.

**Återkommande**: I  [!DNL Query Service]definierar en upprepning om en fråga schemaläggs att köras endast en gång eller med återkommande intervall.

**Representation**: I  [!DNL Offer Decisioning]detta exempel är en representation information som används av en kanal för att visa ett erbjudande, till exempel plats eller språk.

**Resurs**: I  [!DNL Platform Launch]det här fallet är en resurs en allmän term som refererar till alternativ som  [!DNL Platform Launch] användaren kan konfigurera i klientmiljön, inklusive tillägg, dataelement och regler.

**Rollbaserad åtkomstkontroll**: Med rollbaserad åtkomstkontroll kan administratörer tilldela åtkomst och behörigheter till användare i Experience Platform. Behörigheter omfattar möjligheten att visa och/eller använda Experience Platform-funktioner, som att skapa sandlådor, definiera scheman och hantera datauppsättningar.

**Regel**: I  [!DNL Platform Launch]är en regel en samling komponenter som definierar en specifik uppsättning händelser, villkor och åtgärder som ska grupperas logiskt.

**Regelkomponent**: Regelkomponenter är i  [!DNL Platform Launch]sin tur händelser, villkor och åtgärder som utgör en regel.

**Körtid**: Körningsmiljön anger en körningsmiljö för ett maskininlärningsrecept. [!DNL Python]Med körningsmiljöerna , R,  [!DNL Spark]PySpark och Tensorflow kan du ange en URL till en Docker-bild för en receptkälla.

## S

**Exempeldata**: Exempeldata är en förhandsgranskning av en datafil, vanligtvis de första 100 raderna, som ger en datavetare eller tekniker en uppfattning om vilket schema eller vilka data som finns i datafilen.

**Sandlåda**: En sandlåda är en virtuell konstruktion som partitionerar en enda plattformsinstans till en separat virtuell miljö, för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

**Återställ** sandlåda: En sandlådeåterställning tar bort alla data inklusive data, profiler och segment i en sandlåda. Sandlådeåterställning kan påverka data som är anslutna till interna eller externa mål.

**Sandlådeväxlare**: Med sandlådeväxlarkontrollen i Experience Platform kan användare navigera mellan sandlådor som de har tillgång till. Om du byter en sandlåda ändras allt innehåll och funktionsåtkomst kan ändras baserat på behörigheter.

**Schema**: Ett schema är en användardefinierad specifikation av frekvens eller avbruten datainmatning från en datakälla från tredje part till Adobe Experience Platform.

**Poäng**: Poängberäkning är processen att generera insikter från data med hjälp av en tränad modell.

**Schema**: Ett schema är en uppsättning regler som representerar och validerar datastrukturen och dataformatet. Ett schema består av en klass och valfria mixiner och används för att skapa datauppsättningar och datastreams. Ett schema kan innehålla beteendeattribut, tidsstämplar, identiteter, attributdefinitioner, relationer med mera.

**Schemabibliotek**: Schemabiblioteket innehåller XDM-resurser som är branschstandard och som Adobe tillhandahåller, samt anpassade resurser som definierats av din organisation.

**Schemaregister**: Schemaregistret innehåller ett användargränssnitt och RESTful API som används för att visa och hantera alla schemarelaterade resurser i schemabiblioteket.

**Hemlig åtkomstnyckel**: En hemlig åtkomstnyckel är en  [!DNL Amazon] S3-nyckel som används tillsammans med åtkomstnyckel-ID för att signera AWS-begäranden.

**Segment**: Ett segment är en uppsättning regler som innehåller attribut och händelsedata som kvalificerar ett antal profiler för att bli en målgrupp.

**Segment Builder**: Det  [!DNL Segment Builder] är en visuell utvecklingsmiljö som används för att skapa segmentdefinitioner. Det är en vanlig komponent i alla program som använder segmenteringstjänsten Experience Platform.

**Segmentdefinition**: En segmentdefinition är den regeluppsättning som används för att beskriva en målgrupps nyckelegenskaper eller beteende. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment.

**Metod** för segmentutvärdering: Det finns två metoder för segmentutvärdering: schemalagd och on-demand. Schemalagd utvärdering möjliggör ett återkommande schema för körning av ett exportjobb vid en viss tidpunkt, medan behovsutvärdering innebär att ett segmentjobb skapas för att skapa målgruppen omedelbart.

**Segmentexport**: Segmentexport är en av de två typerna av destinationer i Experience Platform. Vid segmentexport kan du skicka de profiler som är kvalificerade och har mappats till målet. Använder segment- och användar-ID:n och pseudonyma data och integreras vanligtvis med sociala nätverk och andra målplattformar för digitala medier.

**Segment-ID**: Ett segment-ID är en automatiskt genererad identifierare som är kopplad till ett segment.

**Segmentmedlemskap**: Segmentmedlemskap visar vilka segment en profil tillhör för närvarande.

**Segmentregler**: Segmentregler definierar villkoren som avgör om en profil kvalificerar sig för ett segment.

**Segmentering**: Segmentering är processen att dela upp en stor grupp kunder, potentiella kunder eller konsumenter i mindre grupper som har liknande attribut och som kommer att svara på liknande sätt som specifika marknadsföringsstrategier.

**Sensei ML Framework**: Sensei ML Framework är ett enhetligt ramverk för maskininlärning (ML) som utnyttjar data från Experience Platform för att möjliggöra för datavetare att utveckla ML-drivna underrättelsetjänster på ett snabbare, skalbart och återanvändbart sätt.

**Känsliga (&quot;S&quot;) etiketter**: Känsliga (&quot;S&quot;) etiketter används för att kategorisera data som anses vara känsliga, till exempel olika typer av beteendedata eller geografiska data som du vill ska markeras som känsliga.

**Tjänster**: Ett kraftfullt ramverk för att driftsätta AI- och ML-tjänster genom att utnyttja Adobe Intelligent Services. Tjänsterna ger personaliserade kundupplevelser i realtid eller driftsätter anpassade intelligenta tjänster.

**Marknadsföringsåtgärd** för personalisering av en identitet: En marknadsföringsåtgärd som använder data för innehållspersonalisering på plats. Personalisering på plats är alla data som används för att dra slutsatser om användarnas intressen, och används för att välja vilket innehåll eller vilka annonser som betjänas baserat på dessa slutsatser.

**Dataanvändningsetikett** för S1: En  `S1` dataanvändningsetikett används för att klassificera data som anger latitud och longitud som kan användas för att bestämma den exakta placeringen av en enhet.

**Etikett** för S2-dataanvändning: En  `S2` dataanvändningsetikett används för att klassificera data som kan användas för att fastställa ett brett definierat geostaktionsområde.

**Källa**: En källa är en allmän term för alla indataanslutningar i Platform. Se även: Källkoppling

**Källattribut**: Ett källattribut är ett fält i källdatauppsättningen. Källattribut mappas till målschemafält.

**Källkatalog**: Källkatalogen är en lista över tillgängliga källanslutningar i Experience Platform.

**Källkategori**: En källkategori är en gruppering av källor som har liknande egenskaper.

**Källkoppling**: Källkopplingar (kallas även källor) hjälper användarna att enkelt importera data från flera källor, vilket möjliggör strukturering, märkning och förbättring av data med hjälp av Experience Platform-tjänster. Data kan hämtas från en mängd olika källor som molnbaserad lagring, tredjepartsprogramvara och CRM-system.

**Direktuppspelningsanslutning**: En direktuppspelningsanslutning är en unik slutpunkt som tillhandahålls av Adobe och som är knuten till en kunds IMS-organisation för att strömma data till Experience Platform.

**Standardnamnutrymme** för identitet: Standardnamnutrymmen för identiteter är fördefinierade namnutrymmen för identiteter från Adobe, som representerar branschstandardlösningar som är vanliga för att identifiera kunder.

**Direktinmatning**: Med direktuppspelad inmatning kan ni skicka data från klient- och serverenheter till Experience Platform i realtid.

**Direktuppspelningssegmentering**: Direktuppspelningssegmentering är en kontinuerlig process för urval av data som uppdaterar segment som svar på användaraktivitet. När ett segment har skapats och sparats tillämpas segmentdefinitionen på inkommande data till [!DNL Real-time Customer Profile]. Tillägg och borttagningar av segment behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

**Systemvy**: Systemvyn är en visuell representation av källdatauppsättningar som flödar igenom  [!DNL Real-time Customer Profile] till mål.

## T

**Målfunktioner**: Vid funktionsmappning är en målfunktion den funktion som förutses av en modell.

**Tidsseriedata**: Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av en registrerade.

**Utbildad modell**: En utbildad modell representerar den körbara utmatningen av en modellutbildningsprocess, där en uppsättning utbildningsdata tillämpades på modellinstansen. En utbildad modell behåller en referens till alla intelligenta webbtjänster som skapas utifrån den. En tränad modell är lämplig för bedömning och för att skapa en intelligent webbtjänst.

**Token**: En token är en typ av tvåfaktorsautentiseringssäkerhet som kan användas för att auktorisera användning av datortjänster med  [!DNL Query Service].

## U

**Unionsschema**: Ett unionsschema är en konsolidering av scheman som delar samma klass och har aktiverats för  [!DNL Real-time Customer Profile]. Det kan finnas flera unionsscheman för en organisation, men det kan bara finnas ett unionsschema per klass.

## V

## W

## X

**XDM**: Se Experience Data Model (XDM).

**XDM-beslutshändelse**: XDM Decision Event är en tidsseriebaserad klass som används för att samla in observationer om utfallet och sammanhanget för en beslutsaktivitet. Detta omfattar information om hur beslutet fattades, när det fattades, vilka alternativ som föreslogs (och valdes) och vilket kontextuellt läge som antingen påverkade beslutet eller kunde observeras under beslutsprocessen.

**XDM ExperienceEvent**: XDM ExperienceEvent är en tidsseriebaserad klass som används för att fånga systemets tillstånd när en händelse (eller uppsättning händelser) inträffar, inklusive tidpunkten och identiteten för det berörda ämnet. Se även: Experience Event

**Individuell XDM-profil**: XDM  [!DNL Individual Profile] är en postbaserad klass som bildar en unik representation av attributen hos både identifierade och delvis identifierade ämnen. Profiler som är välidentifierade kan användas för personlig kommunikation eller målinriktade åtaganden och kan innehålla detaljerad personlig information som namn, kön, födelsedatum, plats och kontaktinformation, inklusive telefonnummer och e-postadresser.

**XDM-system**: XDM System representerar det ramverk som opererar XDM-scheman för användning i Experience Platform-tjänster i senare led.

## Y

## Z
