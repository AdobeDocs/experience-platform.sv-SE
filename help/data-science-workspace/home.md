---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Översikt över arbetsytan Datavetenskap
topic: overview
translation-type: tm+mt
source-git-commit: 3190f2f01ae13d25cc3a3a540b83cc1fc0819f0a

---


# Översikt över arbetsytan Datavetenskap

Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att få insikter från era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med ert innehåll och era dataresurser över alla Adobes lösningar.

Datavetare på alla kunskapsnivåer hittar sofistikerade, lättanvända verktyg som stöder snabb utveckling, utbildning och anpassning av maskininlärningsrecepten - alla fördelarna med AI-tekniken, utan komplexiteten.

Med Data Science Workspace kan datavetare enkelt skapa API:er för intelligenta tjänster - som bygger på maskininlärning. Dessa tjänster fungerar med andra Adobe-tjänster, inklusive Adobe Target och Adobe Analytics Cloud, och hjälper er att automatisera personaliserade, målinriktade digitala upplevelser i webben, datorer och mobilappar.

Den här guiden ger en översikt över de viktigaste begreppen för datavetenskapen.

## Introduktion

Dagens företag sätter hög prioritet på att ta fram big data för prognoser och insikter som hjälper dem att personalisera kundupplevelser och leverera mer värde till kunder - och till företaget.
Lika viktigt som det är kan det vara en hög kostnad att gå från data till insikter. Det kräver ofta kunniga datavetare som bedriver intensiv och tidsödande dataforskning för att utveckla maskininlärningsmodeller, eller recept, som driver intelligenta tjänster. Processen är lång, tekniken är komplex och kvalificerade datavetare kan vara svåra att hitta.

Med Data Science Workspace kan ni med Adobe Experience Platform få upplevelsefokuserad AI i hela företaget och effektivisera och snabba upp data-till-insikter-till-kod med:
- Ett ramverk för maskininlärning och körning
- Integrerad åtkomst till data som lagras i Adobe Experience Platform
- Ett enhetligt dataschema som bygger på Experience Data Model (XDM)
- Den datorkraft som krävs för maskininlärning/AI och hantering av stora datamängder
- Färdiga maskininlärningsrecept som snabbar upp övergången till AI-baserade upplevelser
- Förenklad framställning, återanvändning och modifiering av recept för datavetare med olika kunskapsnivåer
- Intelligent publicering och delning av tjänster med bara några klick - utan utvecklare - och övervakning och omskolning för kontinuerlig optimering av personaliserade kundupplevelser

Datavetare på alla kunskapsnivåer kommer att få insikter snabbare och effektivare digitala upplevelser.

## Komma igång

Här följer en kort sammanfattning av nyckeltermerna innan du börjar gå in på detaljerna i Data Science Workspace:

| Term | Definition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Datavetenskapens arbetsyta | Data Science Workspace inom Experience Platform gör det möjligt för kunder att skapa maskininlärningsmodeller med hjälp av data i Experience Platform och Adobe Solutions för att generera intelligenta insikter och prognoser som väver sevärda digitala upplevelser för slutanvändarna. |
| Artificiell intelligens | Artificiell intelligens är en teori om och utveckling av datorsystem som kan utföra uppgifter som normalt kräver mänsklig omvärldsbevakning, t.ex. visuell uppfattning, taligenkänning, beslutsfattande och översättning mellan språk. |
| Maskinininlärning | Maskininlärning är det studieområde som gör det möjligt för datorer att lära sig utan att programmeras explicit. |
| Sensei ML Framework | Sensei ML Framework är ett enhetligt ramverk för maskininlärning i hela Adobe som utnyttjar data på Experience Platform för att möjliggöra för datavetare att utveckla maskininlärningsdrivna underrättelsetjänster på ett snabbare, skalbart och återanvändbart sätt. |
| Experience Data Model | Experience Data Model (XDM) är den standardiseringsinsats som Adobe leder för att definiera standardscheman som Profile och ExperienceEvent för Customer Experience Management. |
| JupyterLab | JupyterLab är ett webbaserat gränssnitt med öppen källkod för Project Jupyter och är nära integrerat med Experience Platform. |
| Recept | Ett recept är Adobes term för en modellspecifikation och är en behållare på den översta nivån som representerar maskininlärning, AI-algoritm eller en kombination av algoritmer, bearbetningslogik och konfiguration som krävs för att skapa och köra en tränad modell och därmed bidra till att lösa specifika affärsproblem. |
| Modell | En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende. |
| Utbildning | Utbildning är processen att lära sig mönster och insikter från märkta data. |
| Utbildad modell | En utbildad modell representerar den körbara utmatningen av en modellutbildningsprocess, där en uppsättning utbildningsdata tillämpades på modellinstansen. En utbildad modell behåller en referens till alla intelligenta webbtjänster som skapas utifrån den. Den tränade modellen är lämplig för bedömning och för att skapa en intelligent webbtjänst. Ändringar av en utbildad modell kan spåras som en ny version. |
| Poäng | Poängberäkning är processen att generera insikter från data med hjälp av en tränad modell. |
| Tjänst | En distribuerad tjänst visar en artificiell intelligens, maskininlärningsmodell eller avancerad algoritm via ett API så att den kan användas av andra tjänster eller program för att skapa intelligenta appar. |

I följande diagram visas det hierarkiska förhållandet mellan Recept, Models, Training Runs (Utbildningsprogram) och Scoring Runs (Resultatprov).

![](./images/home/recipe_hiearchy_ui.png)

## Understanding Data Science Workspace

Med Data Science Workspace kan era datavetare effektivisera den krångliga processen att hitta insikter i stora datamängder. Data Science Workspace bygger på ett gemensamt ramverk för maskininlärning och en gemensam runtime och ger avancerad arbetsflödeshantering, modellhantering och skalbarhet. Intelligenta tjänster stöder återanvändning av maskininlärningsrecept för att driva en mängd olika tillämpningar som skapats med Adobes produkter och lösningar.

### Åtkomst till data i ett steg

Data är hörnstenen i AI och maskininlärning.

Data Science Workspace är helt integrerat med Adobe Experience Platform, inklusive Data Lake, kundprofil i realtid och Unified Edge. Utforska alla era organisationsdata som lagras i Adobe Experience Platform samtidigt, tillsammans med gemensamma big data- och deep learning-bibliotek, som Spark ML och TensorFlow. Om du inte hittar det du behöver kan du importera egna datauppsättningar med XDM:s standardiserade schema.

### Fördefinierade maskininlärningsrecept

Data Science Workspace innehåller färdiga maskininlärningsrecept för vanliga affärsbehov, som försäljningsprognoser och avvikelseidentifiering, så att datavetare och utvecklare inte behöver börja från början. För närvarande erbjuds tre recept, [produktinköpsprognoser](./pre-built-recipes/product-purchase-prediction.md), [produktrekommendationer](./pre-built-recipes/product-recommendations.md)och [detaljhandel](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Om du vill kan du anpassa ett fördefinierat recept efter dina behov, importera ett recept eller börja från början och skapa ett eget recept. Men när du väl har utbildat och hyper-tune på ett recept behöver du inte utveckla en anpassad intelligent tjänst - bara några klick - och du är redo att skapa en riktad, personaliserad digital upplevelse.

### Arbetsflöde med fokus på datavetare

Oavsett vilken nivå ni har av datavetenskaplig expertis hjälper Data Science Workspace till att förenkla och snabba upp processen att hitta insikter i data och tillämpa dem på digitala upplevelser.

### Utforska data

Att hitta rätt data och förbereda dem är den mest arbetsintensiva delen av att bygga upp ett effektivt recept. Data Science Workspace och Adobe Experience Platform hjälper er att snabbare komma från data till insikter.

På Adobe Experience Platform centraliseras och lagras era data över flera kanaler i det standardiserade XDM-schemat, vilket gör det enklare att hitta, förstå och rensa data. Ett enda datalager som baseras på ett gemensamt schema kan spara oräkneliga timmars datautforskande och förberedelse.

När du bläddrar kan du använda R, Python eller Scala med den inbyggda Jupyter Notebook-värddatorn för att bläddra i katalogen med data på plattformen. Om du använder något av dessa språk kan du även använda Spark ML och TensorFlow. Börja från början eller använd någon av de mallar för bärbara datorer som finns för specifika affärsproblem.

Som en del av arbetsflödet för datautforskande kan du även importera nya data eller använda befintliga funktioner för att förbereda data.

### Redigering

Med Data Science Workspace bestämmer du hur du vill skapa recept.

- Spara tid genom att bläddra efter ett fördefinierat recept som passar dina affärsbehov och som du kan använda som det är eller konfigurera för att uppfylla dina specifika behov.
- Skapa ett helt nytt recept genom att använda redigeringsmiljön i Jupyter Notebook för att utveckla och registrera receptet.
- Ladda upp ett recept som skapats utanför Adobe Experience Platform till Data Science Workspace eller importera receptkod från ett arkiv, t.ex. Git, med den autentisering och integrering som finns mellan Git och Data Science Workspace.

### Experimentation

Data Science Workspace ger otrolig flexibilitet i experimenteringsprocessen. Börja med ditt recept. Skapa sedan en separat instans med samma huvudalgoritm i kombination med unika egenskaper, som till exempel avstämningsparametrar. Du kan skapa så många förekomster du behöver, utbilda och betygsätta varje förekomst så många gånger du vill. När du utbildar dem spårar Data Science Workspace recept, recept-instanser och tränade instanser, tillsammans med utvärderingsstatistik, så att du inte behöver göra det.

### Operationalisering

När du är nöjd med ditt recept är det bara några klick att skapa en intelligent tjänst. Ingen kodning krävs - du kan göra det själv utan att behöva registrera en utvecklare eller tekniker. Publicera slutligen den intelligenta tjänsten på Adobe IO så är den klar att användas av ert team för digitala upplevelser.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Kontinuerlig förbättring

Data Science Workspace spårar var intelligenta tjänster anropas och hur de fungerar. När data rullas in kan du utvärdera den intelligenta tjänstens exakthet för att stänga slingan och träna om recepten efter behov för att förbättra prestandan. Resultatet blir en kontinuerlig förbättring av kundens personalisering.

### Tillgång till nya funktioner och datauppsättningar

Datavetare kan dra nytta av nya tekniker och datauppsättningar så snart de är tillgängliga via Adobes tjänster. Genom de regelbundna uppdateringarna arbetar vi med att integrera datauppsättningar och tekniker i plattformen, så att du inte behöver göra det.

### Åtkomstkontroll i arbetsytan Datavetenskap

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor. Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md) .

>[!IMPORTANT] För att kunna använda arbetsytan Datavetenskap måste behörigheten Hantera datavetenskapen aktiveras.

I följande tabell visas effekterna av att ha den här behörigheten aktiverad eller inaktiverad:

| Behörighet | Aktiverad | Handikappade |
|---|---|---|
| Hantera arbetsytan Datavetenskap | Ger tillgång till alla tjänster i arbetsytan Datavetenskap. | API- och gränssnittsåtkomst till alla tjänster i Data Science Workspace är inaktiverat. Även om det är inaktiverat går det inte att dirigera till *modellerna* för datavetenskapen och *tjänstsidorna* . |

### Säkerhet och sinnesfrid

Att skydda era data är högsta prioritet för Adobe. Adobe skyddar era data med säkerhetsprocesser och kontroller som utvecklats för att hjälpa er att följa standarder, bestämmelser och certifieringar som godkänts i branschen.

Säkerhet är inbyggd i programvara och tjänster som en del av Adobe Secure Product Lifecycle.
Läs mer om Adobes datasäkerhet och programvarusäkerhet, regelefterlevnad med mera på säkerhetssidan på https://www.adobe.com/security.html.

### Stöd för sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje plattformsinstans har stöd för en produktionssandlåda och flera icke-produktionssandlådor, där var och en har ett eget bibliotek med plattformsresurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. Mer information om sandlådor finns i översikten över [sandlådor](../sandboxes/home.md).

För närvarande har Data Science Workspace några sandlådebegränsningar:

- Beräkningsresurser delas mellan sandlådan för produktion och icke-produktionssandlådor. Isolering för produktionssandlådor kommer att tillhandahållas i framtiden.
- Arbetsbelastningarna Scala/Spark och PySpark för både bärbara datorer och recept stöds för närvarande bara i produktionssandlådan. Stöd för icke-produktionssandlådor kommer att ges i framtiden.

## Data Science Workspace in action

Förutsättningar och insikter ger den information ni behöver för att leverera en personaliserad upplevelse till alla kunder som besöker er webbplats, kontaktar ert callcenter eller deltar i andra digitala upplevelser. Så här fungerar ditt dagliga arbete med Data Science Workspace.

### Definiera problemet

Allt börjar med ett affärsproblem. Ett onlinesamtal behöver till exempel en kontext som hjälper dem att få en negativ kunduppfattning att bli positiv.

Det finns mycket data om kunden. De har bläddrat på webbplatsen, lagt artiklar i varukorgen och till och med lagt beställningar. De kan ha fått e-post, använda kuponger eller kontaktat callcentret tidigare. Mottagaren måste sedan använda tillgängliga data om kunden och deras aktiviteter för att avgöra om det är troligt att kunden kommer att uppskatta och använda ett erbjudande.

![](./images/home/example_problem.png)

Vid kontakten mellan samtalscentret har kunden fortfarande två par skor i kundvagnen, men tog bort en skjorta. Med den här informationen kan den intelligenta tjänsten rekommendera att kundtjänstagenten erbjuder en kupong för 20 % rabatt på skor under samtalet. Om kunden använder kupongen läggs den informationen till i datauppsättningen och prognoserna blir ännu bättre nästa gång kunden ringer.

### Utforska och förbereda data

Beroende på vilket affärsproblem som har definierats vet du att receptet bör undersöka alla kundens webbtransaktioner, inklusive webbplatsbesök, sökningar, sidvisningar, klickade länkar, kundvagnsåtgärder, mottagna erbjudanden, e-postmeddelanden, interaktioner med callcenter osv.

En datavetare ägnar vanligtvis upp till 75 % av den tid som krävs för att skapa ett recept som utforskar och omvandlar data. Data kommer ofta från flera databaser och sparas i olika scheman - de måste kombineras och mappas innan de kan användas för att skapa ett recept.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Om du börjar från början eller konfigurerar ett befintligt recept börjar du sökningen efter data i en centraliserad och standardiserad datakatalog för organisationen, vilket gör sökningen betydligt enklare. Du kan till och med upptäcka att en annan datavetare i organisationen redan har identifierat en liknande datauppsättning och välja att finjustera den datauppsättningen i stället för att börja från början.
Alla data i Adobe Experience Platform följer ett standardiserat XDM-schema, vilket eliminerar behovet av att skapa en komplex modell för att koppla samman data eller få hjälp av en datatekniker.

Om du inte omedelbart hittar de data du behöver, men de finns utanför Adobe Experience Platform, är det en relativt enkel uppgift att importera ytterligare datauppsättningar, som också kommer att omvandlas till det standardiserade XDM-schemat.\
Du kan använda Jupyter-anteckningsbok för att förenkla förbearbetning av data, och kanske börja med en mall för en anteckningsbok eller en anteckningsbok som du har använt tidigare för att vara benägen att köpa.

<!-- databricks update-->
![](./images/home/notebook_templates.png)

### Skriv receptet

Om du redan har hittat ett recept som uppfyller alla dina behov kan du gå vidare till experimenterande. Eller så kan du ändra receptet lite eller skapa ett från början - och utnyttja redigeringsmiljön för arbetsytan Data Science i Jupyter Notebook. Genom att använda redigeringsmiljön kan du både använda arbetsflödet för utbildning i datavetenskap och betygssättning och konvertera receptet senare så att det kan lagras och återanvändas av andra i organisationen.

Du kan också importera ett recept till arbetsytan Datavetenskap och dra nytta av experimentarbetsflödena när du skapar din intelligenta tjänst.

### Experimentera med receptet

Med ett recept som innehåller dina huvudmaskininlärningsalgoritmer kan många recept skapas med ett enda recept. Dessa recept-instanser kallas för modeller. En modell kräver utbildning och utvärdering för att optimera dess driftseffektivitet och effektivitet, en process som vanligtvis består av en provperiod och ett fel.

![](./images/home/recipe_hiearchy_ui.png)

När du utbildar dina modeller genereras kurser och utvärderingar. Data Science Workspace håller reda på mätvärden för varje unik modell och deras utbildningar. Mätvärden som genereras genom experimenterande kommer att göra det möjligt för er att avgöra vilken utbildning som fungerar bäst.

![](./images/home/evaluation_metrics.png)

I [det här avsnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) finns självstudiekurser om hur du utbildar och utvärderar modeller i Data Science Workspace.

### Använda modellen

När du har valt det bäst utbildade receptet för att tillgodose dina affärsbehov kan du skapa en intelligent tjänst i Data Science Workspace utan hjälp från utvecklare. Det är bara några klick - ingen kodning behövs. En publicerad intelligent tjänst är tillgänglig för andra medlemmar i organisationen utan att modellen behöver återskapas.

En publicerad intelligent tjänst är konfigurerbar för att automatiskt utbilda sig själv emellanåt med nya data allt eftersom de blir tillgängliga. Detta garanterar att din tjänst är effektiv och effektiv även om tiden går.

## Nästa steg

Data Science Workspace hjälper till att effektivisera och förenkla arbetsflödet för datavetenskap, från datainsamling till algoritmer till intelligenta tjänster, för datavetare på alla kunskapsnivåer. Med de sofistikerade verktygen Data Science Workspace kan ni avsevärt korta tiden från data till insikter.

Och viktigast av allt är att Data Science Workspace förser datavetenskapen och algoritmisk optimeringsfunktionerna i Adobes ledande marknadsföringsplattform med uppgifter från datavetare i företag. För första gången kan företag ta med egna algoritmer till plattformen och dra nytta av Adobes kraftfulla maskininlärnings- och AI-funktioner för att leverera personaliserade kundupplevelser i stor skala.

I och med samgåendet mellan varumärkesexpertis och Adobes maskininlärning och AI-framsteg har företag möjlighet att få mer affärsvärde och varumärkeslojalitet genom att ge kunderna det de vill ha, innan de ber om det.

Om du vill ha mer information, t.ex. ett komplett arbetsflöde, kan du börja med att läsa [dokumentationen för arbetsytan Data Science Workspace](./walkthrough.md) .

## Ytterligare resurser

Följande video har utformats för att ge stöd för din förståelse av arbetsytan Data Science.

>[!VIDEO](https://images-tv.adobe.com/mpcv3/2fbf62c1-44ed-4162-8eed-f47ab8599701_1578435939.1920x1080at3000_h264.mp4)

