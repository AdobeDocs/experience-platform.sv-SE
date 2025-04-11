---
title: Modellkort för AI-modellgenomskinlighet i Adobe Experience Platform
description: Läs mer om modellkort i Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 74a8ef82-cff9-4a7e-95c8-f915eb664eda
source-git-commit: 1edecf0cb413b66d66973517421bc0062f475337
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 0%

---

# Modellkort för AI-modellgenomskinlighet i Adobe Experience Platform

Ett AI-modellkort är det standardformat som AI-modellens genomskinlighet kommuniceras med. Modellkort innehåller omfattande information om den underliggande modellen som ett visst AI-verktyg bygger på. Modellkort innehåller information om t.ex. AI-verktygets syfte, utbildningsdata, prestandamått, begränsningar och etiska överväganden. Du kan använda den genomskinlighet som modellkort ger för att bättre förstå modellens funktioner och begränsningar, samt för att bättre främja en ansvarsfull och rättvis användning av AI.

Modellkort är offentliga och är avsedda att förbättra både befintliga och potentiella kundinsikter om de AI-modeller som Adobe använder. Modellkort är vanligtvis statiska. Det finns dock flera aspekter av AI-modeller som kan ändras över tid, bland annat rad-, avvikelse- och andra genomskinlighetsattribut.

Läs det här dokumentet om du vill veta mer om modellkort i Adobe Experience Platform.

## Modellkortsavsnitt {#model-card-sections}

Ett modellkort består av en mängd olika sektioner, där var och en fokuserar på en viss aspekt av AI-modellen.

Här nedan finns en guide om de olika avsnitten i ett modellkort, inklusive information om vilka frågor de besvarar.

### Modellöversikt {#model-overview}

Modellöversikten innehåller allmän information om en AI-modell. Använd det här avsnittet för att ange information som namn, syfte och typ för AI-modellen. Dessutom kan du använda det här avsnittet för att identifiera de avsedda användarna och för att beskriva hur modellen kan integreras med Experience Platform.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vad heter modellen? | AI-modellens officiella namn och version | **CustomerAI Propensity Scoring Model v2.0** <br>CustomerAI är en AI-baserad modell som utformats för att generera benägenhetspoäng för användare baserat på deras tidigare beteenden och interaktioner med ett företag. Det bidrar till att förutsäga sannolikheten för att en kund vidtar specifika åtgärder, som att göra ett köp, engagera med innehåll eller krama bilder. Den här modellen distribueras inom Adobe Experience Platform och integreras med olika arbetsflöden för marknadsföring och kundanalys.</br> |
| Vad är syftet med modellen? | En kort beskrivning av vad modellen är avsedd att göra. | Modellen är utformad för att ge marknadsförare och kundinteraktionsteam åtgärdbara insikter genom att förutsäga sannolikheten för att en kund kommer att utföra en viss åtgärd, som att göra ett köp, registrera sig för en prenumeration eller engagera sig i en e-postkampanj. Tack vare resultaten kan företag optimera målgruppssegmentering och personalisera kundinteraktioner baserat på förutsedda beteenden. |
| Vilken typ av modell är det? | Modellens typ, till exempel klassificering, regression, generativ osv. | Detta är en s **kontrollerad inlärningsklassificeringsmodell** som förutser sannolikheten för en händelse som inträffar (t.ex. köp, köp, köp, engagemang) utifrån historiska kunddata. Den har tränats med hjälp av övertoningsstartsbeslutsträd (GBDT) med logistisk regression för att modellera benägenhetspoäng. |
| Vilka är de avsedda användarna? | De interna och externa användargrupper som modellen är avsedd för. | De främsta användarna i den här modellen är marknadsförare, dataanalytiker och kundinteraktionsteam som utnyttjar Adobe Experience Platform för att utveckla datadrivna marknadsföringsstrategier. |
| Hur integreras denna modell med Adobe Experience Platform? | Integreringsinformation och API:er som används samt hur de passar in i arbetsflödena. | CustomerAI integreras direkt i **Adobe Experience Platform AI-tjänster**, vilket gör att användare kan komma åt modellutdata via fördefinierade API:er och instrumentpaneler. Propensitetspoängen som genereras av modellen kan användas i **Adobe Journey Optimizer**, **och Adobe Real-Time CDP** för att förfina målgruppssegmenteringen och skräddarsy marknadsföringsstrategier. |

{style="table-layout:auto"}

+++

### Avsedd användning {#intended-use}

Avsnittet för avsedd användning innehåller information om AI-modellens primära användningsfall. Du kan använda det här avsnittet för att fördjupa dig i de problem som din modell avser att lösa, de branscher och/eller domäner som din modell är relevant för och de missbruk som bör undvikas när du använder din AI-modell.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka är de primära användningsfallen? | De scenarier där modellen förväntas användas. | Den här modellen används främst för **kundsegmentering, riktad marknadsföring och bortfallsförutsägelse**. Företag använder den här modellen för att **förutsäga kundens inköpsmetod, optimera marknadsföringskampanjer och förbättra personaliseringen**. Ett e-handelsföretag kan till exempel använda modellen för att identifiera kunder med hög återgivning och erbjuda dem exklusiva erbjudanden. |
| Vilka problem löser den här modellen? | De huvudproblem som modellen tar upp. | Marknadsförare kämpar ofta med att **identifiera rätt kunder för att målinrikta** och **optimera engagemanget**. Den här modellen **minskar gissningsarbetet** genom att tillhandahålla en **datadriven metod** för kundanpassning, vilket säkerställer att marknadsföringsresurserna fördelas effektivt. |
| Vilka branscher eller domäner är den här modellen relevant för? | En lista över tillämpliga branscher. | Modellen gäller i flera branscher, inklusive **e-handel, detaljhandel, finansiella tjänster, telekommunikation och media**. Alla företag som förlitar sig på kundengagemang och personaliserad marknadsföring kan dra nytta av den här modellen. |
| Hur ska den här modellen inte användas? | Eventuella missbruk som bör undvikas. | Modellen **ska inte användas för beslutsfattande med hög risk**, till exempel **bedömning av finansiella krediter, medicinsk diagnostik eller juridiska bedömningar**. Dessutom är den inte avsedd att användas i **prediktion för personligt känsliga beteenden** (t.ex. hälsotillstånd, politiska preferenser) på grund av potentiella etiska frågor. |

{style="table-layout:auto"}

+++

### Modellindata och -utdata {#model-inputs-and-outputs}

Avsnittet för modellindata och -utdata innehåller information om de datatyper som stöds och som modellen använder som indata och returnerar som utdata. Du kan använda det här avsnittet för att ge exempel på indata och utdata som är relevanta för din AI-modell.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka typer av data använder modellen som indata? | De datatyper som modellen tar som indata, inklusive datafunktioner, format och källor. | Modellen behandlar **kundbeteendedata, demografiska attribut och historiska interaktioner**. Detta inkluderar data som besöksfrekvens på webbplatser, inköpshistorik, engagemang med marknadsföringsmejl och demografiska uppgifter. |
| Vilket format ska indata ha? | Godkända indataformat. | Indata måste struktureras som **JSON-objekt** som innehåller kundattribut och beteendesignaler. För gruppbearbetning accepterar modellen **CSV-filer** som är formaterade enligt Adobe Experience Platform standarder för dataimport. |
| Vad genererar modellen? | Den typ av utdata som genereras av modellen. | Modellen ger en benägenhetspoäng mellan 0 och 1, där högre värden anger en större sannolikhet för att den förväntade händelsen inträffar. Dessutom ger det funktionens prioritet och gör det möjligt för användarna att förstå vilka faktorer som påverkade förutsägelsen. |
| Vad är några exempel på indata och utdata? | Ett exempel på indata och motsvarande utdata. | <ul><li>**Exempelindata:** json { &quot;customer_id&quot;: 12345, &quot;previous_purchase&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0.4 }</li><li>**Exempelutdata:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Utbildningsdata {#training-data}

Avsnittet med utbildningsdata innehåller information om de datauppsättningar som användes för att utbilda en viss AI-modell. Du kan använda det här avsnittet för att gå igenom hur stora och källtana utbildningsdata är, vilka biaser som identifierades i datauppsättningen och hur data bearbetades i förväg.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka datauppsättningar användes för att utbilda modellen? | En beskrivning av datakällorna. | Modellen har utbildats på anonyma kundinteraktionsdata som samlats in via Adobe Experience Platform. Det omfattar historiska kundbeteendedata, transaktionsregistreringar, e-postinteraktioner och interaktionsstatistik över flera branscher. |
| Vilken storlek och källa har data? | Utbildningsdatamängdens volym och ursprung. | Utbildningsdata består av 10 miljoner kunddata från en mängd olika Adobe Experience Platform-kunder. Dessa register innehåller historiska kundinteraktioner, transaktionsdata, beteendeloggar och demografisk information från olika branscher som detaljhandel, e-handel, telekommunikation och finans. Data samlades in under en 24-månadersperiod för att säkerställa en tillräcklig representation av säsongstrender och långsiktiga engagemangsmönster. |
| Finns det några kända biaser i datauppsättningen? | Överväganden om avvikelser och motåtgärder. | Datauppsättningen kommer huvudsakligen från engagerande användare, vilket kan innebära en förskjutning av urvalet. För att minska detta tillämpar modellen stratifierad provtagning, teknik för revision av avvikelser och strategier för datainsamling. |
| Hur förbearbetas data? | Steg som vidtas för att rensa och förbereda data. | Datauppsättningen genomgår omfattande förbehandling för att säkerställa att data är konsekventa, håller hög kvalitet och är användbara. <ol><li>**Hantera saknade värden**: Saknade värden hanteras med en kombination av medelimputering (för numeriska fält), lägesimputering (för kategoriserade fält) och prediktiv modellering (för komplexa saknade fall).</li><li>**Kategorisisk kodning:** Kategorivariabler som kundsegment och inköpskategorier konverteras till numeriska representationer med kodnings- och målkodningstekniker som varmar ett och ett.</li><li>**Funktionsskalning och normalisering:** Min-max-skalning används för avgränsade variabler (t.ex. ålder, inkomst), medan z-score-standardisering används för normalt fördelade funktioner.</li><li>**Ytterligare förbehandling:** Pipelinen innehåller avdataidentifiering och borttagning, duplicerad filtrering, tidsstämpelstandardisering och funktionsteknik som förbättrar förutsägbarheten.</li></ol> |

{style="table-layout:auto"}

+++

### Modellarkitektur och utbildning {#model-architecture-and-training}

I modellarkitekturen och utbildningsavsnittet beskrivs hur AI-modellen kan utformas. I detta avsnitt hänvisas till AI-modellens struktur och utformning, inklusive detaljer om den typ av algoritm och de utvärderingsmetoder som används. Du kan också använda det här avsnittet för att ange information om vilka utbildningsramverk som används samt vilka datorresurser som användes i utbildningen.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilken arkitektur använder modellen? | Typ av neuralnätverk, ensemble-metod osv. | Modellen utnyttjar GBDT (Gradient Boosting Decision Trees) med XGBoost, optimerat för strukturerade data. Det har utbildats på historiska kundhändelsesekvenser för att identifiera prediktiva beteendemönster. |
| Vilka algoritmer tillämpades? | Maskininlärningstekniker som användes. | Modellen byggs med en övervakad inlärningsstrategi som utnyttjar GBDT (Gradient Boosting Decision Trees) med XGBoost som den primära inlärningsalgoritmen. Dessutom ingår logistisk regression som en basmodell för riktmärkning av prediktiv precision. |
| Vilka utbildningsramverk användes? | Bibliotek eller plattformar som används för utbildning. | Modellen utvecklades med TensorFlow, XGBoost och scikit-learn. Utbildning körs på Adobe AI-molninfrastruktur med grafikprocessorerna NVIDIA V100 som stöder storskaliga datamängder. |
| Vilka beräkningsresurser användes för utbildningen? | Maskinvaru- och molnresurserna som användes för utbildning. | NVIDIA V100 GPU:er, utbildade i Google Cloud-infrastruktur. |
| Vilka bedömningsmetoder användes? | Mätvärden och testmetoder som användes för utvärderingen. | AUC-ROC, precisionsåterkallning och korsvalidering. |

{style="table-layout:auto"}

+++

### Resultat och utvärdering {#performance-and-evaluation}

Avsnittet om prestanda och utvärdering innehåller information om de mätvärden och metoder som används för att bedöma hur väl modellen utför sina avsedda uppgifter. Du kan använda det här avsnittet för att ge information om de utvärderingsmått som användes, samt om identifierade svagheter eller misslyckanden.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Hur testades modellen? | De metoder som används för att validera prestanda. | Modellen testades med en demovalideringsmetod, där 80 % av data användes för utbildning och 20 % reserverades för utvärdering. |
| Vilka mätvärden användes? | De viktigaste resultatindikatorerna. | Modellens effektivitet mäts med **AUC-ROC (0,85)**, **precision-revanrop (0,78)** och **F1-poäng (0,80)**. Dessa mätvärden hjälper till att bedöma modellens prediktiva styrka i olika segment. |
| Hur varierar prestanda mellan olika scenarier? | De sammanhangsspecifika prestandavariationerna. | Lägre precision för nya kundsegment med begränsade historiska data. |
| Finns det några kända svagheter eller misslyckanden? | Eventuella begränsningar eller felpunkter. | Modellen kanske inte fungerar som den ska för kunder med begränsade historiska data (problem med kallstart). Dessutom kan säsongseffekter, t.ex. semestershoppingtrender, kräva frekvent omskolning för att bibehålla noggrannheten. |

{style="table-layout:auto"}

+++

### Fairness and bias {#fairness-and-bias}

Avsnittet om rättvisa och avvikelse innehåller information om hur AI-modellen fungerade när det gäller mätegenskaper för rättvisa och avvikelse. Fairness avser modellens förmåga att ge likvärdiga resultat i olika demografiska grupper och användningsfall, medan avvikelse avser systematiska fel som leder till orättvisa resultat. Använd det här avsnittet för att gå närmare igenom de rimlighetskontroller som utfördes och för att diskutera hur modellen minskar fördomar.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka rimlighetskontroller utfördes? | De bias-analyser och reduceringsprocesser som utfördes. | Modellen genomgick demografiska paritetstester och konsariella rimlighetsbedömningar för att upptäcka prestandaskillnader mellan olika användarsegment. |
| Påverkar modellen vissa grupper oproportionerligt? | Eventuella skillnader i prestanda som har identifierats. | Analysen visade en prestandaminskning på 5 % för användare med låga historiska interaktionsdata. För att åtgärda detta innehåller modellen tekniker för omviktning under utbildningen. |
| Hur mildrar modellen de negativa effekterna? | De tekniker som används för att ta itu med avvikelser. | Datauppsättningen är stratifierad för att säkerställa proportionell återgivning av olika kunddemografi, och under utbildningens gång införs krav på rättvisa för att förhindra att modellen gynnar en viss grupp. Regelbunden kontroll av systematiska avvikelser genomförs med hjälp av demografiska analyser, vilket gör det möjligt att justera om resultatskillnader upptäcks. |

{style="table-layout:auto"}

+++

### Förklara och tolka {#explainability-and-interpretability}

Avsnittet Förklaring och tolkbarhet innehåller information om en AI-modells förmåga att tillhandahålla tydliga och begripliga förklaringar och hur enkelt en mänsklig användare kan förstå hur indatafunktioner påverkar prognoser och svar. Använd det här avsnittet för att förklara hur användare bättre kan förstå varför din modell fattar vissa beslut och vilka verktyg eller tekniker som är tillgängliga för att tolkas.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Kan användare förstå varför modellen fattar vissa beslut? | De tolkningsmetoder som används av modellen. | Modellen utnyttjar **SHAP (SHapley Additive Explanations)** för att kvantifiera effekten av varje indatafunktion på sina prognoser, vilket ger transparens i hur kundattribut påverkar benägenhetspoängen. SHAP-värden möjliggör både global tolkning och identifierar de mest inflytelserika faktorerna i alla prognoser, samt lokal tolkning som förklarar individuella prognoser för specifika kunder. |
| Vilka verktyg och tekniker finns tillgängliga för att tolka? | De tillgängliga förklaringsverktygen. | Modellen har stöd för **Local Interpretable Model-Agnostic Förklarations (LIME)** och SHAP för att ge insikter om hur indatafunktioner påverkar förutsägelser. LIME genererar lokala förklaringar genom att skapa störda versioner av indata och observera förändringar i förutsägelser, medan SHAP tilldelar bidragsvärden till varje funktion, vilket ger både global och lokal tolkning av modellbeslut. |

{style="table-layout:auto"}

+++

### Robusta funktioner och generalisering {#robustness-and-generalization}

Avsnittet om tillförlitlighet och generalisering innehåller information om hur bra AI-modellen kan fungera på osynliga data. Dessutom kan du använda det här avsnittet för att gå igenom hur modellen behåller sin prestanda och precision med oväntade eller utmanande indata.

>[!TIP]
>
>I AI avser&quot;osynliga data&quot; data som skiljer sig från de data som en viss modell har utbildats på.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Hur bra fungerar modellen på osynliga data? | Resultaten av testning av generaliseringsprestanda. | Modellen bevarar **80% AUC-ROC** när den testas på osynliga datamängder, vilket visar en stark generalisering till nya kundposter. Prestandan är stabil för olika kundsegment men försämras något när användarbeteendet avviker avsevärt från historiska mönster. |
| Har modellen stresstestats för konsariella indata? | Information från utvärderingen av tillförlitlighet. | Modellen har utvärderats mot störd och konsariell inmatning, inklusive saknade data, avledningsbar injektion och avsiktlig felmärkning. Prestandan är stabil under normala förhållanden, men en mindre noggrannhetsförsämring (cirka 3-5%) observerades under extrema negativa förändringar. |

{style="table-layout:auto"}

+++

### Säkerhet och integritet {#security-and-privacy-considerations}

Avsnittet om säkerhet och integritet innehåller information om de åtgärder och den praxis som används för att skydda känsliga data och säkerställa att modellen används på ett säkert sätt. Du kan använda det här avsnittet för att besvara frågor om hur modellen hanterar känsliga data.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Hanterar modellen känsliga data? | All information följer sekretesslagstiftningen. | Modellen behandlar inte eller bevarar någon personligt identifierbar information och alla data som används för utbildning anonymiseras och slås samman. Den följer strikta regler för efterlevnad av GDPR, CCPA och Adobe interna integritetspolicyer för att säkerställa ansvarsfull dataanvändning. |
| Vilka sekretessbeständiga tekniker användes? | De tekniker som används för att säkerställa integritetsåtgärder. | Modellen innehåller olika integritetstekniker som lägger till kontrollerat brus i data och förhindrar återidentifiering av individer. Dessutom används metoderna för hashning, anonymisering och tokenisering för att ta bort PII före modellutbildning och -härledning. |

{style="table-layout:auto"}

+++

### Övervakning och underhåll {#monitoring-and-maintenance}

Övervaknings- och underhållsavsnittet innehåller information om hur modellens prestanda övervakas över tid och hur ofta modellen omskolas. Du kan använda det här avsnittet för att ange information om hur mätvärden som precision, precision, återkallande och fördröjning spåras.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Hur övervakas modellens prestanda över tid? | Information om de spårningsmekanismer som används för modellen. | Modellen övervakas kontinuerligt via WatsonX, med spårning av nyckeltal för prestandaindikatorer som noggrannhetsdrift, viktiga funktionsförändringar och förutsägelsestabilitet. Mekanismerna för avvikelseidentifiering och varningar meddelar teamet när det finns betydande avvikelser från förväntat beteende. |
| Hur ofta omskolas modellen? | Frekvensen för uppdateringar av modellen. | Modellen omskolas månadsvis med uppdaterade kundinteraktionsdata för att säkerställa fortsatt relevans. Regelbunden omskolning bidrar till att minska dataavdrift och säsongsrelaterade fluktuationer som kan påverka prediktiv precision. |

{style="table-layout:auto"}

+++

### Etiska överväganden och ansvarsfull AI {#ethical-considerations-and-responsible-ai}

De etiska övervägandena och det ansvariga AI-avsnittet innehåller information om eventuella etiska problem som är kopplade till din AI-modell. Det här avsnittet innehåller även hur bra din modell passar in med ansvarsfulla AI-principer. Använd det här avsnittet för att ge information om de potentiella etiska effekterna av din modells användning, inklusive erkännande av biaser, säkerställande av rättvisa och förebyggande av skador för individer eller grupper.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka etiska problem är kopplade till denna modell? | De potentiella risker som har identifierats. | Modellen skulle kunna ge upphov till partiskhet i beslutsfattandet om den inte övervakas korrekt. Om vissa demografiska data till exempel är överrepresenterade i utbildningsdata kan modellen leda till en orättvis fördel för specifika kundgrupper. |
| Hur överensstämmer modellen med principerna för ansvarsfull AI? | Information om hur modellen uppfyller AI:s etiska riktlinjer. | Adobe Experience Platform följer riktlinjerna för ansvarsfull AI och ser till att modellerna genomgår partiska revisioner, rimlighetstestning och mänsklig tillsyn före driftsättningen. |

{style="table-layout:auto"}

+++

### Kända begränsningar {#known-limitations}

Avsnittet Kända begränsningar innehåller information om befintliga begränsningar som har identifierats för AI-modellen. Använd det här avsnittet för att stryka under de förhållanden under vilka AI-modellen kan fungera dåligt och för att ange eventuella begränsningar som användarna måste känna till.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka är kända begränsningar för modellen? | Alla identifierade prestanda eller begränsningar för användningsfall. | Det kan vara svårt att exakt förutsäga resultaten för nyligen lanserade produkter eller kundsegment där det inte finns tillräckligt med historiska data. Dessutom kan säsongsvariationer i kundbeteenden orsaka variationer i prediktiv noggrannhet om de inte tas med i omutbildningen. |
| Under vilka förhållanden fungerar modellen dåligt? | Alla identifierade svagheter med avseende på modellen. | Prestandan minskar när kundupplevelsen är begränsad, till exempel för förstagångsköpare eller användare med minimala engagemangsdata. Dessutom, om kundbeteenden förändras på grund av externa faktorer som ekonomiska nedgångar eller branschtrender, kan modellen kräva snabb anpassning för att bibehålla noggrannheten. |

{style="table-layout:auto"}

+++

### Framtida förbättringar {#future-improvements}

Avsnittet om framtida förbättringar innehåller information om funktionsuppdateringar som planeras för AI-modellen. Använd det här avsnittet för att gå vidare till din färdplan för förbättringar.

+++Visa frågor och exempelsvar

| Fråga | Information krävs | Exempel på svar |
| --- | --- | --- |
| Vilka förbättringar planeras för framtida iterationer? | Vägkartan för förbättringar. | Framtida iterationer kommer att innehålla teknik för att överföra inlärning för att förbättra prestandan för kallstartsanvändare och förbättra anpassningsförmågan till förändrade kundbeteenden. Dessutom kommer dataintegrering i realtid att introduceras för att förbättra modellernas svarstider och exakthet i dynamiska marknadsföringsmiljöer. |

{style="table-layout:auto"}

+++
