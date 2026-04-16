---
title: Hur Adobe Experience Platform och program samverkar
description: Adobe Experience Platform och alla program fungerar var för sig och fungerar tillsammans som stöd för era kundmål.
solution: Experience Platform
feature: Getting Started
topic: Overview
role: Architect, Developer, Data Architect, Data Engineer, Business Practitioner
exl-id: c4f8e2a1-6b3d-4f92-9c7e-1a2b3c4d5e6f
source-git-commit: 60e7d803d72089348f11a34d6386aa9ccc51f487
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 0%

---


# Hur Adobe Experience Platform och program samverkar

Det här avsnittet förklarar tre idéer.

1. Vad [!DNL Adobe Experience Platform] gör själv.
2. Vad varje program gör själv.
3. Hur plattformen och tillämpningarna samverkar så att organisationen kan uppnå sina mål och betjäna kunderna på ett bra sätt.

Dela det här avsnittet med marknadsförare, produktägare och personer som bygger eller kör lösningen. När du har läst den kan du använda steg-för-steg-guider i [!DNL Experience League] när du behöver produktuppgifter eller teknisk information.

>[!NOTE]
>
>Det här avsnittet är en översikt. Instruktioner, åtgärder i användargränssnittet och API-information finns i länkarna i [Ytterligare resurser](#additional-resources).

## Vad programmen är och huvudsyftet med dem {#applications-at-a-glance}

I den här dokumentationen är ett program en licensierad Adobe-produkt som körs på [!DNL Adobe Experience Platform]. Program använder samma kundprofil, datastruktur, identitetslänkar och dataregler som plattformen. Varje program lägger till egna skärmar och arbetsflöden för en typ av arbete (till exempel att skicka målgrupper till kanaler, köra resor eller rapportera resultat).

Tabellen nedan visar de olika programmen. Den ger en kort beskrivning och ett huvudsyfte. Alla utgåvor listas inte. Vad du kan köpa beror på din licens.

| Program | Vad det är | Huvudsyfte |
|---------------|------------|----------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/home) | Ansökan om kunddata och målgrupper | Samla era egna kunddata. Bygg målgrupper som uppdateras ofta. Skicka målgrupper och attribut till annonser, e-post, mobilappar och andra verktyg. Dataregler tillämpas. Samma produktfamilj har stöd för konsumentföretag, företagskunder och blandade modeller. Se produkthjälpen för utgåvor. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Ansökan om resa och meddelanden | Planera och kör personaliserade resor (till exempel välkomstvägar, kundlojalitet eller uppföljning efter service). Skicka meddelanden över flera kanaler med live-event och profildata. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/en/docs/customer-journey-analytics) | Analysprogram för alla kanaler | Mät och studera hur kunderna rör sig genom resor och hur marknadsföringen fungerar. Använder data som har förberetts i [!DNL Adobe Experience Platform]. |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/en/docs/mix-modeler) | Ansökan om marknadsföringsmätning och -planering | Samla mätvärden (inklusive blandningsmodellering av marknadsföring). Planera utgiftsscenarier för marknadsföring. Använder data som är anslutna via [!DNL Adobe Experience Platform] så att team kan se vad som driver resultat och planera budgetar. |

>[!NOTE]
>
>Andra Adobe Experience Cloud-produkter kan ansluta till [!DNL Adobe Experience Platform]. Det här avsnittet fokuserar på program som använder plattformen som huvudkälla för kunddata. Produktnamn, utgåvor och vad som säljs kan variera beroende på licens och land eller region.

## Vad du förstår efter att ha läst {#learning-outcomes}

När du har läst det här avsnittet bör du kunna göra följande.

1. Beskriv plattformen separat - Förklara vad [!DNL Adobe Experience Platform] gör som delad bas för data- och dataregler. Du kan förklara detta utan att namnge ett specifikt program.
2. Beskriv varje huvudprogram separat - Upptäck vilket affärsmål varje program stöder och vilken typ av arbete det är avsett för.
3. Beskriv hur plattformar och applikationer passar ihop - Förklara hur kundprofiler, identiteter, dataformer (scheman) och dataregler rör sig från plattformen till applikationer. Förklara varför team inte behöver skapa separata, konfliktskapande dataredningar för varje verktyg.
4. Koppla ett mål till rätt del av lösningen - För ett exempelmål (t.ex.&quot;kör onboarding via e-post och mobil&quot;), ange vilka delar av plattformen och vilka program som vanligtvis stöder det målet.

I det här avsnittet betyder&quot;dina mål&quot; vad din organisation vill ha (till exempel tillväxt, effektivitet eller kundförtroende). &quot;Era kunder&quot; innebär personer som interagerar med ert varumärke. Plattformen och tillämpningarna finns för att hjälpa era team att betjäna dessa kunder.

## Vem bör läsa detta ämne? {#who-should-read}

| Din roll | Så här hjälper det här avsnittet |
|-----------|------------------------|
| Företags- och marknadsföringsledare | Koppla samman kund- och varumärkesmål med plattformsfunktioner och applikationer. Använd samma ord som era tekniska team. |
| Personer inom marknadsföring, analys eller kundupplevelse | Se var data samlas, var val görs och vilket program som passar vilket steg. |
| Arkitekter, ingenjörer och utvecklare | Använd samma enkla modell och termer som resten av [!DNL Experience League] när du designar eller bygger. |

## Så här fungerar [!DNL Adobe Experience Platform] på egen hand {#platform-alone}

[!DNL Adobe Experience Platform] är baslagret för kundupplevelsedata. Det är inte en enda marknadsföringsskärm. Den bygger på tjänster som körs i bakgrunden. Innan du öppnar ett program kan plattformen göra följande.

| Vad plattformen gör | Därför hjälper detta dig |
|--------------------------|---------------------|
| Hämtar data från webbplatser, appar och affärssystem (i filer eller som en liveström) | Du är inte fast med en kanal eller en databas. Du kan skapa en mer detaljerad vy över tiden. |
| Strukturerar data med scheman baserade på Experience Data Model (XDM) så att händelser och fält har en gemensam betydelse | Team som analyserar data, skickar målgrupper och kontrollerar efterlevnad använder samma definitioner. Det minskar antalet misstag och upprepar arbete. |
| Länkar identiteter så att samma person eller konto kan identifieras i era regler på olika enheter och system | Team kan arbeta från en enda vy av kunden där policyn tillåter det. |
| Håller [!DNL Real-Time Customer Profile] uppdaterad som Live-vy för beslut och skicka ut data | Alternativen kan använda aktuella data, inte bara en gammal fil från igår. |
| Skapar målgrupper (segmentering) utifrån profildata, beteende och samtycke | Du definierar vilka som ska ingå på ett och samma ställe. Andra steg återanvänder den logiken. |
| Skickar data till mål (export och anslutna system) och tillämpar dataregler via etiketter, profiler och [!DNL Privacy Service] | Teamen kan röra sig snabbare samtidigt som de fortfarande följer samtycke och rätt. |

Plattformen sammanställer kunddata, tillämpar regler och förbereder data för användning. Det ersätter inte de kompletta skärmar som applikationerna erbjuder för resedesign, mediaarbetsflöden eller flerkanalsrapporter. Applikationerna ger dessa upplevelser.

### Plattformstjänster i korthet {#core-platform-services}

| Område | Vad det gör på baslagret |
|------|--------------------------------|
| Datainsamling ([!DNL Tags], [!DNL Experience Platform Web SDK], [!DNL Experience Platform Mobile SDK], datastreams) | Samla in data från digitala upplevelser på ett standardsätt. |
| Källor och datainhämtning | Koppla data från företagets system och molnkällor till plattformen. |
| XDM och scheman | Ange struktur och innebörd för upplevelsedata. |
| [!DNL Identity Service] | Koppla identifierare till en vy i en profil. |
| [!DNL Real-Time Customer Profile] | Håll kvar den live-profil som används för beslut och skicka ut data. |
| Segmentering | Definiera målgrupper utifrån profildata och händelser. |
| Mål | Skicka målgrupper och attribut till andra system som kör marknadsföring eller tjänster. |
| Datastyrning, [!DNL Privacy Service], samtycke | Styr hur data får användas. |
| [!DNL Data Science Workspace] | Bygg, utbilda och kör maskininlärningsmodeller på plattformsdata. Detta är en plattformsfunktion, inte ett program. |
| [!DNL Query Service] | Kör SQL på Experience Platform-data för analys och rapportering. Detta är en plattformstjänst, inte ett program. |

Dessa områden har stöd för ett enkelt flöde: samla ihop → förena → bestämma → aktivera → mått. Dataregler gäller för varje steg.

## Hur programmen fungerar på egen hand {#applications-alone}

En kort lista över varje program och dess huvudsyfte finns i [Vad programmen är och huvudsyftet med varje program](#applications-at-a-glance). Tabellen nedan lägger till detaljer. Den visar vad varje program gör på egen hand och vilket mål det stöder.

Applikationerna är användarupplevelser och arbetsflöden på plattformen. Var och en av dem hjälper era team att utföra en huvudtyp av arbete. Alla får samma profil och dataregler. Team behöver inte kopiera hela datastapeln för varje verktyg.

| Program | Vad det gör på egen hand (huvudarbete) | Vilket mål det hjälper er att nå |
|-------------|-------------------------------------|------------------------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/home) | Hantera målgrupper och aktivering: bygg segment, uppdatera medlemskap ofta, skicka målgrupper och attribut till destinationer. Har stöd för användningsområden som konsumenter, företag och blandad användning beroende på din licens. | Nå rätt personer och exkludera fel i betalda, ägda och partnerkanaler med hjälp av era egna enhetliga kunddata. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Designa resor och skicka meddelanden: reagera på händelser, förgreningsvägar och skicka över kanaler från en och samma arbetsyta. | Kör personaliserade sekvenser (t.ex. onboarding, retention eller serviceuppföljning) som svarar på det som kunden just gjorde. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/en/docs/customer-journey-analytics) | Rapportera och analysera resor och kampanjresultat med en enda datamängd. | Se vad som hände och varför i alla kanaler så att ni kan förbättra er investering och upplevelse. |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/en/docs/mix-modeler) | Kombinera plattformsanslutna data med modeller för att mäta kanaler och köra planeringsscenarier. | Planera och justera marknadsföringsbudgeten med en stadig bild av hur kanaler och andra faktorer påverkar resultatet. |

Kort och gott är hur man arbetar i arbetsgrupper (aktivering, resor, analys, marknadsföringsmätning). Plattformen är den plattform som innehåller kunddata och regler som alla dessa team litar på. Plattformen erbjuder även frågor och avancerad modellering via tjänsterna ovan.

>[!IMPORTANT]
>
>Vilka program du kan använda beror på din Adobe-licens. Funktioner, begränsningar och tillgänglighet kan ändras. Kontrollera ditt kontrakt och den senaste [!DNL Experience League]-dokumentationen.

## Hur plattformen och programmen fungerar tillsammans {#platform-and-apps-together}

När vi säger att plattform och program fungerar tillsammans menar vi tre saker.

1. En kundprofil, många produkter - [!DNL Real-Time Customer Profile], [!DNL Identity Service] och dataregler delas. [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] och [!DNL Adobe Mix Modeler] lästes från samma bas (och relaterade data). Ni har inte en kundlista för analyser och en annan lista för marknadsföring om inte er process kräver det.
2. En viktig faktor för det som hände - data formas med XDM-scheman. Samma händelse kan leda till rapportering, resor och målgruppsregler. Teamen ägnar mindre tid åt att argumentera om definitioner.
3. En plats för dataregler - etiketter och profiler gäller för de data som används i programmen. Dataregler läggs inte bara till senare i varje verktyg.


### Heltäckande flöden (hur arbetet fungerar på olika plattformar och i olika appar) {#end-to-end-flows}

| Stadie | Vad plattformen gör | Vilka program lägger vanligtvis till |
|-------|----------------------------|-------------------------------------|
| Know | Hämta in data, strukturera den, länkidentitet, uppdatera profil | Program läser profil och händelser. De ersätter inte steget att föra in data. |
| Decide | Bygg segment och kontrollera vem som kvalificerar sig med enhetliga data | [!DNL Real-Time CDP] för att skapa målgrupper. [!DNL Adobe Journey Optimizer] för resesökvägar och nästa bästa åtgärd i kontexten. |
| Aktivera | Destinationer och kontrollerad export av målgrupper och attribut | [!DNL Real-Time CDP] stöder många aktiveringsmönster. Resor skickar meddelanden via de kanaler som du har konfigurerat. |
| Mät | Händelser och identiteter som följer en modell i datalagret | [!DNL Customer Journey Analytics] för rese- och kampanjrapportering. [!DNL Adobe Mix Modeler] för enhetlig marknadsföringsmätning och planering som använder plattformsanslutna data. |

## Exempel: Ett arbetsflöde som använder plattformen och alla fyra programmen {#example-full-stack-workflow}

Artikeln nedan är ett vanligt mönster. Dina team kan ändra ordningen eller hoppa över ett steg. Målet är att visa hur [!DNL Adobe Experience Platform] och [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] och [!DNL Adobe Mix Modeler] kan visas i samma program.

### Scenariot {#example-scenario}

Ett detaljhandelsvarumärke driver ett säsongsbaserat förvärvs- och introduktionsprogram. Ledarskapet vill planera sina utgifter, nå nya köpare med betalda medier, välkomna nya kunder med budskap och rapportera om resultaten. Varumärket använder enhetliga kunddata på [!DNL Adobe Experience Platform].

### Vad som händer i arbetsflödet {#example-steps}

1. [!DNL Adobe Experience Platform] (plattformen)\
   Team tar in webb- och appevent, beställningar, samtycke och kostnads- eller prestandadata från annonser där de är tillgängliga. Data använder delade XDM-scheman. [!DNL Identity Service] länkar kända kunder. [!DNL Real-Time Customer Profile] uppdateras som personer handlar och registrerar sig. Dataregler och samtycke lagras på plattformen.\
   *Utan det här steget har programmen nedan inget tillförlitligt att läsa.*

2. [!DNL Adobe Mix Modeler]\
   Marknadsföring och finansiering granskar hur kanalerna bidrar till försäljningen och hur man delar upp budgeten i olika medier för säsongen. De använder modeller och planeringsvyer som bygger på harmoniserade marknadsförings- och resultatdata kopplade till plattformen.\
   *I det här steget beskrivs hur ska vi investera på planeringsnivå. Det skickar inte e-post eller bygger dagliga målgrupper separat.*

3. [!DNL Real-Time CDP]\
   Förvärvningsteam bygger målgrupper (t.ex. troliga köpare eller personer som lämnat objekten i en kundvagn). De aktiverar dessa målgrupper för annonsering och andra destinationer. De kan också bygga upp grupper som hindrar kunderna så att befintliga kunder inte blir presumtiva.\
   *Det här steget besvarar&quot;vem ska vi nå eller exkludera i betalda och ägda kanaler&quot;.*

4. [!DNL Adobe Journey Optimizer]\
   Livscykelteamen gör en välkomstresa efter ett köp eller en registrering. Resan lyssnar efter profil- eller händelselägen, grenar (till exempel första köp eller upprepning) och skickar e-post eller mobilmeddelanden.\
   *Det här steget besvarar&quot;vilket meddelande eller vilken sökväg personen kommer efter&quot;.*

5. [!DNL Customer Journey Analytics]\
   Analysteam bygger rapporter och kontrollpaneler på den fullständiga vägen från annonser till köp och introduktion. De mäter trattar, kanaler och segment med hjälp av samma händelser och profilbaserade definitioner som används i andra verksamheter.\
   *Det här steget besvarar&quot;vad som hände under resan och vilka delar som fungerade&quot;.*

Team kör ofta steg 2 till 5 parallellt över en fjärdedel. Mix Modeler-uppdateringar kan ske långsammare än aktiva målgrupper eller resor. Det är normalt.

### Hur programmen fungerar tillsammans {#example-together}

- En profil och en händelsemodell Samma person och samma händelser kommer från plattformen till [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer] och [!DNL Customer Journey Analytics]. Mix Modeler använder sammankopplade och harmoniserade data från plattformen. Det kan använda sammanfattningar (t.ex. veckoutgifter) samt händelsenivådata, beroende på konfiguration.
- Olika jobb, samma sanning. [!DNL Real-Time CDP] pushar vem som ska nås. [!DNL Adobe Journey Optimizer] kör det som händer efter en åtgärd. [!DNL Customer Journey Analytics] visar vad som har hänt i steg. [!DNL Adobe Mix Modeler] har stöd för varför budget ska flyttas på en högre nivå.
- Dataregler följer med data. Etiketter och samtycke på plattformen påverkar vilka profiler som kan användas i segment, resor och rapportering.

### Konfigurationsvarningar {#example-gotchas}

>[!IMPORTANT]
>
>Detta skapar förvirring i verkliga projekt. Hantera dem som kontrollpunkter för arkitekter och administratörer.

| Område | Vad du ska titta på |
|------|----------------|
| Identitet | Om webben, appar och CRM skickar olika identifierare eller namnområdesinställningar kan profilen dela upp en person i två delar. Segment, resor och rapporter kommer inte att överensstämma. Justera identitetsregler och primära ID:n innan du skalförändrar aktiveringen. |
| Regler för samtycke och data | Om datauppsättningar som används i [!DNL Real-Time CDP] eller [!DNL Adobe Journey Optimizer] inte är korrekt märkta eller godkända kan du aktivera eller skicka meddelanden till personer som du inte ska göra. Granska etiketter, policyer och godkännandefält på samma datauppsättningar som du använder för målgrupper och resor. |
| [!DNL Real-Time CDP] och [!DNL Adobe Journey Optimizer] samtidigt | Samma person kan befinna sig i en aktiverad målgrupp och på en resa. Du kan dubbelskicka meddelanden eller skapa konflikter med erbjudanden om du inte använder undertryckslistor, filter för reseanmälan eller tydliga regler för vem som ska ta sig in på en resa. Koordinera team och testa i en sandlåda först. |
| [!DNL Customer Journey Analytics] definitioner | Rapporterna använder [!UICONTROL Data views] och måttregler. Om dessa definitioner inte matchar de händelser eller attribut som marknadsförarna använder i [!DNL Real-Time CDP] eller [!DNL Adobe Journey Optimizer], kommer instrumentpanelerna inte att hålla med om kampanjrapporter. Justera dimensionerna och måttdefinitionerna efter intressenter. |
| [!DNL Adobe Mix Modeler] timing och dataform | Blandningsmodellering använder ofta harmoniserade eller sammanslagna indata och schemalagda uppdateringar. Förvänta dig inte samma realtidssvar som [!DNL Real-Time Customer Profile]. Utgifts- och resultatdata måste kartläggas och rensas i harmonisering. Felaktiga mappningar skevar kanalkredit och budgetråd. |
| Mix Modeler jämfört med Journey Analytics | Mix Modeler fokuserar på bidrag och planering på kanalnivå. [!DNL Customer Journey Analytics] fokuserar på resvägar och segment. De besvarar relaterade men olika frågor. Tvinga inte en KPI att matcha den andra utan en dokumenterad brygga. |
| Sandlådor | Konfiguration i en sandlåda flyttas inte automatiskt till produktion. Planera en kampanjprocess för scheman, segment, resor och anslutningar. |
| Tidszoner | Resor, rapportfönster och annonsplattformar kan använda olika tidszoner. Feljusterade fönster orsakar fel antal och bruten resepost. |

### Skyddsritningar och begränsningar {#example-guardrails}

Adobe publicerar skyddsutkast för [!DNL Adobe Experience Platform] och för varje program. I skyddsritningar beskrivs gränser, förväntade prestanda och säkra intervall för konfiguration. De hjälper dig att undvika fel, flaskhalsar och instabilt beteende. Garantier är inte servicenivåavtal (SLA). De garanterar inte hastighet eller drifttid i rättsligt hänseende.

Ditt kontrakt, din produktbeskrivning och din försäljningsorder kan ange avtalsbegränsningar eller rättigheter. Dessa regler kan skilja sig från den allmänna dokumentationen. Använd ditt avtal och Adobe-kontoteam tillsammans med [!DNL Experience League] när du är osäker.

| Ämne | Vad du ska planera för |
|-------|------------------|
| Mjuka gränser och hårda gränser | Vissa gränser är riktlinjer. Om du går långt förbi dem kan prestanda försämras eller latensen öka. Andra begränsningar har fastställts av systemet eller av ditt kontrakt. Du får inte överskrida dem utan att ändra inställningarna eller köpet. |
| Var begränsningar ska tillämpas | Många begränsningar gäller på organisationsnivå, inte per sandlåda. Sandlådemiljöer har ofta mindre tak än produktion. Testresultat i en sandlåda kanske inte visar prestanda i full skala. |
| Inmatning och profil | Hög händelsemängd, identitetsvolym eller antal profiler påverkar kostnader, hastighet och stabilitet. Följ skyddsriktlinjerna för dataöverföring och profil när du designar rörledningar. Mycket stora målgrupper eller mycket frekventa uppdateringar kan stressa aktiveringsvägar. |
| Segmentering och aktivering | [!DNL Real-Time CDP] har skyddsprofiler för segment, aktivering och mål. Partnermål har också egna versaler, filstorlekar eller obligatoriska fält. Ett segment som fungerar i användargränssnittet kan fortfarande misslyckas eller kortas av vid ett mål om du ignorerar båda sidorna. |
| [!DNL Adobe Journey Optimizer] | Resor, kanaler och meddelandehastigheter har produktbegränsningar. Komplexa resor eller stora volymer måste granskas mot [!DNL Adobe Journey Optimizer] skyddsräcken så att meddelandena förblir tillförlitliga. |
| [!DNL Customer Journey Analytics] | Rapporteringen har begränsningar för anslutningar, [!UICONTROL Data views], rader och kardinalitet. Stora dimensioner eller mycket stora händelsvolymer kräver designgranskning så att rapporterna förblir användbara. |
| [!DNL Adobe Mix Modeler] | Modellering och planering bygger på tillräcklig historik och rena harmoniserade data. Det finns produktbegränsningar för datauppsättningar, modeller och uppdateringsbeteende. Tunna eller högljudda data skapar svaga eller instabila modeller. |
| API:er och automatisering | Programmatiska anrop använder hastighetsbegränsningar och kvoter. Batchjobb som ignorerar dessa begränsningar kan misslyckas eller strypas. |
| Regioner och tillgänglighet | Vissa funktioner, mål och program är inte tillgängliga i alla regioner. Bekräfta region för dataresistens och produkttillgänglighet innan du utformar hela arbetsflödet. |

>[!NOTE]
>
>Numeriska gränser och standardvärden ändras över tid. Kopiera inte begränsningar från den här översikten till ett designdokument. Använd de aktuella skyddsprofilsidorna i [!DNL Experience League], användningsvyerna för din licens där din organisation har dem och ditt kontrakt.

### Var kan jag läsa mer? {#where-to-read-guardrails}

* [Experience Platform och programskyddsutkast](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-diagrams/architecture-overview/guardrails) - Översikt över hur skyddsutkast fungerar på olika plattformar och i olika program.
* [Garantier för datainhämtning](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails) - Inmatningsgenomströmning och relaterade begränsningar.
* [Real-Time CDP skyddsräcken](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) - Segment, aktivering och användning av Real-Time CDP.
* [Licensanvändning](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/data-management-best-practices) - Datahantering och licenshantering på Experience Platform (där det är tillämpligt för din organisation).

Om ditt arbetsflöde lutar mycket på [!DNL Customer Journey Analytics], [!DNL Adobe Journey Optimizer], [!DNL Adobe Mix Modeler] eller [!DNL Query Service] läser du informationen om skyddsinformation för de produkterna i deras produkthjälp.

## Kartlägg era mål för plattformen och programmen {#goals-map}

Använd den här tabellen för att se vad du vill ha, vad plattformen erbjuder och vilka program som hjälper dig.

| Ditt mål | Vad som ska användas från plattformen | Så här använder du program |
|-----------|-------------------------------------|--------------------------------------|
| Se en person eller ett konto i alla kanaler | [!DNL Identity Service], [!DNL Real-Time Customer Profile], XDM | Alla program i listan har fördelar. [!DNL Real-Time CDP] och [!DNL Adobe Journey Optimizer] använder profil för att skicka målgrupper och resor. |
| Köra kampanjer och listor med aktuellt medlemskap | Profil, segmentering, mål, dataregler | [!DNL Real-Time CDP] för hur målgrupper skickas. Destinationer innehåller principkontext. |
| Köra flerstegsupplevelser som reagerar på beteenden | Profil, live-event, dataregler | [!DNL Adobe Journey Optimizer] för reslogik och meddelanden. |
| Rapport om resor och kanaler med matchande nummer | Delade XDM-händelser och identiteter | [!DNL Customer Journey Analytics] för analys av samma data. |
| Se hur kanaler bidrar till marknadsföringsbudgeten och planera marknadsföringsbudgeten | United datasets, data rules, data ready for models | [!DNL Adobe Mix Modeler] för blandningsmodellering och kostnadsplanering. |
| Anpassa marknadsföring och service efter kundfakta | Profil, dataregler, valfria anslutningar till andra system | Hur du ansluter andra system kan variera. Plattformen är fortfarande grunden för kunddata. |

## Roller och överlämningar {#roles-and-handoffs}

| Stadie | Vem är ofta involverad? | Vad de huvudsakligen använder |
|-------|------------------------|----------------------|
| Definiera innebörd och regler för data | Datastyrning, juridik, marknadsföring, ledarskap | Scheman, etiketter, principer för plattformen |
| Ställ in insamlings- och dataledningar | Datatekniker, marknadsföringsteknik | [!DNL Tags], SDK:er, källor, dataförberedelse på plattformen |
| Bygg målgrupper och resor | Marknadsföring, CRM, kundresor | Program ([!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer]) ovanpå samma profil |
| Aktivera och kör dag till dag | Marknadsföringsverksamhet, media, livscykelteam | Destinationer, reserapportering, aviseringar |
| Granska och förbättra | Analyser, efterlevnad, verksamhet | Granskningsloggar, övervakning, kontrollpaneler |

## Terminologi {#terminology}

* [!DNL Adobe Experience Platform] - Delade tjänster och funktioner: datainhämtning, datamodellering, [!DNL Identity Service], [!DNL Real-Time Customer Profile], segmentering, mål, datastyrning, sekretess och funktioner som [!DNL Data Science Workspace] och [!DNL Query Service].
* Program - licensierade produkter på plattformen (till exempel [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Mix Modeler]) som paketerar arbetsflöden för specifika jobb. De är inte samma som plattformstjänster som [!DNL Query Service] och [!DNL Data Science Workspace].

Detta matchar hur [Experience Platform-dokumentationsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) grupperar innehåll.

## Ytterligare resurser {#additional-resources}

* [Adobe Experience Platform - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home) - Huvudstartpunkter för hjälp.
* [Översikt över Experience Platform-dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) - Hur hjälpavsnitten är ordnade.
* [Planer för digitala upplevelser](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/overview/experience-cloud) - Exempel på designer efter användningsfall och bransch.

Om du behöver lära dig mer kan du läsa självstudiekurser och kurser i [!DNL Experience League] på [!DNL Experience Platform Web SDK], XDM och scheman, identitet, segmentering och mål.

>[!NOTE]
>
>När du lägger till det här avsnittet i en Adobe-dokumentationsdatabas kontrollerar du `exl-id`, `feature` och `topic` mot dina svarsregler. Ersätt platshållaren `exl-id` i YAML-huvudet om arbetsflödet tilldelar ett nytt ID.
