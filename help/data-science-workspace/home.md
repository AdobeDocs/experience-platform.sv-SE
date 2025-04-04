---
keywords: Experience Platform;home;Data Science Workspace;populära ämnen;datavetenskap;datavetenskap
solution: Experience Platform
title: Data Science Workspace Overview
description: Den här guiden ger en översikt över de viktigaste begreppen för Data Science Workspace i Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 0%

---

# Data Science Workspace - översikt

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att frigöra insikter från dina data. [!DNL Data Science Workspace] är integrerat i Adobe Experience Platform och hjälper dig att göra förutsägelser med ditt innehåll och dina dataresurser över alla Adobe-lösningar.

Datavetare på alla kunskapsnivåer hittar sofistikerade, lättanvända verktyg som stöder snabb utveckling, utbildning och anpassning av maskininlärningsrecepten - alla fördelarna med AI-tekniken, utan komplexiteten.

Med [!DNL Data Science Workspace] kan datavetare enkelt skapa API:er för intelligenta tjänster - som drivs av maskininlärning. Dessa tjänster fungerar tillsammans med andra Adobe-tjänster, inklusive Adobe Target och Adobe Analytics Cloud, för att hjälpa er att automatisera personaliserade, målinriktade digitala upplevelser i webben, datorer och mobilappar.

Den här guiden ger en översikt över de viktigaste begreppen som rör [!DNL Data Science Workspace].

## Introduktion

Dagens företag sätter hög prioritet på att ta fram big data för prognoser och insikter som hjälper dem att personalisera kundupplevelser och leverera mer värde till kunder - och till företaget.
Lika viktigt som det är kan det vara en hög kostnad att gå från data till insikter. Det kräver ofta kunniga datavetare som bedriver intensiv och tidsödande dataforskning för att utveckla maskininlärningsmodeller, eller recept, som driver intelligenta tjänster. Processen är lång, tekniken är komplex och kvalificerade datavetare kan vara svåra att hitta.

Med [!DNL Data Science Workspace] kan du med Adobe Experience Platform ta fram upplevelsefokuserad AI i hela företaget och effektivisera och snabba upp data-till-insikter-till-kod med:
- Ett ramverk för maskininlärning och körning
- Integrerad åtkomst till data som lagras i Adobe Experience Platform
- Ett enhetligt dataschema byggt på [!DNL Experience Data Model] (XDM)
- Den datorkraft som krävs för maskininlärning/AI och hantering av stora datamängder
- Färdiga maskininlärningsrecept som snabbar upp övergången till AI-baserade upplevelser
- Förenklad framställning, återanvändning och modifiering av recept för datavetare med olika kunskapsnivåer
- Intelligent publicering och delning av tjänster med bara några klick - utan utvecklare - och övervakning och omskolning för kontinuerlig optimering av personaliserade kundupplevelser

Datavetare på alla kunskapsnivåer kommer att få insikter snabbare och effektivare digitala upplevelser.

## Komma igång

Innan du går in på informationen för [!DNL Data Science Workspace], här följer en kort sammanfattning av nyckeltermerna:

| Villkor | Definition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | Med [!DNL Data Science Workspace] i [!DNL Experience Platform] kan kunder skapa maskininlärningsmodeller med hjälp av data för [!DNL Experience Platform] och Adobe Solutions för att generera intelligenta insikter och prognoser som väver sevärda digitala upplevelser för slutanvändarna. |
| Artificiell intelligens | Artificiell intelligens är en teori om och utveckling av datorsystem som kan utföra uppgifter som normalt kräver mänsklig omvärldsbevakning, t.ex. visuell uppfattning, taligenkänning, beslutsfattande och översättning mellan språk. |
| Maskininlärning | Maskininlärning är det studieområde som gör det möjligt för datorer att lära sig utan att programmeras explicit. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework är ett enhetligt maskininlärningsramverk i Adobe som utnyttjar data på [!DNL Experience Platform] för att möjliggöra för datavetare att utveckla maskininlärningsdrivna underrättelsetjänster på ett snabbare, skalbart och återanvändbart sätt. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) är den standardiseringsinsats som Adobe leder för att definiera standardscheman som [!DNL Profile] och [!DNL ExperienceEvent] för Customer Experience Management. |
| [!DNL JupyterLab] | [!DNL JupyterLab] är ett webbaserat gränssnitt med öppen källkod för Project Jupyter och är nära integrerat i [!DNL Experience Platform]. |
| Recept | Ett recept är en Adobe-term för en modellspecifikation och är en behållare på den översta nivån som representerar maskininlärning, AI-algoritm eller en kombination av algoritmer, bearbetningslogik och konfiguration som krävs för att skapa och köra en tränad modell och därmed bidra till att lösa specifika affärsproblem. |
| Modell | En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende. |
| Utbildning | Utbildning är processen att lära sig mönster och insikter från märkta data. |
| Utbildad modell | En utbildad modell representerar den körbara utmatningen av en modellutbildningsprocess, där en uppsättning utbildningsdata tillämpades på modellinstansen. En tränad modell behåller en referens till alla intelligenta webbtjänster som skapas utifrån den. Den tränade modellen är lämplig för bedömning och för att skapa en intelligent webbtjänst. Ändringar av en utbildad modell kan spåras som en ny version. |
| Poäng | Poängberäkning är processen att generera insikter från data med hjälp av en tränad modell. |
| Tjänst | En distribuerad tjänst visar en artificiell intelligens, maskininlärningsmodell eller avancerad algoritm via ett API så att den kan användas av andra tjänster eller program för att skapa intelligenta appar. |

I följande diagram visas det hierarkiska förhållandet mellan Recept, Models, Training Runs (Utbildningsprogram) och Scoring Runs (Resultatprov).

![](./images/home/recipe_hiearchy_ui.png)

## Förstå [!DNL Data Science Workspace]

Med [!DNL Data Science Workspace] kan dina datavetare effektivisera den krångliga processen att hitta insikter i stora datamängder. [!DNL Data Science Workspace] bygger på ett gemensamt maskininlärningsramverk och en gemensam körningsmiljö och levererar avancerad arbetsflödeshantering, modellhantering och skalbarhet. Intelligenta tjänster stöder återanvändning av maskininlärningsrecept för att driva en mängd olika tillämpningar som skapats med Adobe produkter och lösningar.

### Åtkomst till data i ett steg

Data är hörnstenen i AI och maskininlärning.

[!DNL Data Science Workspace] är helt integrerat med Adobe Experience Platform, inklusive Data Lake, [!DNL Real-Time Customer Profile] och [!DNL Unified Edge]. Utforska alla era organisationsdata som lagras i Adobe Experience Platform samtidigt, tillsammans med gemensamma big data- och deep learning-bibliotek, som [!DNL Spark] ML och [!DNL TensorFlow]. Om du inte hittar det du behöver kan du importera egna datauppsättningar med XDM:s standardiserade schema.

### Fördefinierade maskininlärningsrecept

[!DNL Data Science Workspace] innehåller färdiga maskininlärningsrecept för vanliga affärsbehov, som försäljningsprognoser och avvikelseidentifiering, så att datavetare och utvecklare inte behöver börja från början. För närvarande erbjuds tre recept, [produktinköpsförutsägelse](./pre-built-recipes/product-purchase-prediction.md), [produktrekommendationer](./pre-built-recipes/product-recommendations.md) och [detaljhandelsförsäljning](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Om du vill kan du anpassa ett fördefinierat recept efter dina behov, importera ett recept eller börja från början och skapa ett eget recept. Men när du väl har utbildat och hyper-tune på ett recept behöver du inte utveckla en anpassad intelligent tjänst - bara några klick - och du är redo att skapa en riktad, personaliserad digital upplevelse.

### Arbetsflöde med fokus på datavetare

Oavsett din nivå av datavetenskap hjälper [!DNL Data Science Workspace] till att förenkla och snabba upp processen att hitta insikter i data och tillämpa dem på digitala upplevelser.

### Utforska data

Att hitta rätt data och förbereda dem är den mest arbetsintensiva delen av att bygga upp ett effektivt recept. [!DNL Data Science Workspace] och Adobe Experience Platform hjälper dig att komma från data till insikter snabbare.

På Adobe Experience Platform centraliseras och lagras data i XDM:s standardiserade schema, så det blir enklare att hitta, förstå och rensa data. Ett enda datalager som baseras på ett gemensamt schema kan spara oräkneliga timmars datautforskande och förberedelse.

När du bläddrar kan du använda R, [!DNL Python] eller Scala med den integrerade värddatorn [!DNL Jupyter Notebook] för att bläddra i datakatalogen på [!DNL Experience Platform]. Om du använder något av dessa språk kan du även utnyttja [!DNL Spark] ML och TensorFlow. Börja från början eller använd någon av de mallar för bärbara datorer som medföljer för specifika affärsproblem.

Som en del av arbetsflödet för datautforskande kan du även importera nya data eller använda befintliga funktioner för att förbereda data.

### Redigering

Med [!DNL Data Science Workspace] bestämmer du hur du vill skapa recept.

- Spara tid genom att bläddra efter ett fördefinierat recept som passar dina affärsbehov och som du kan använda som det är eller konfigurera för att uppfylla dina specifika behov.
- Skapa ett helt nytt recept genom att använda redigeringsmiljön i Jupyter Notebook för att utveckla och registrera receptet.
- Överför ett recept som har skapats utanför Adobe Experience Platform till [!DNL Data Science Workspace] eller importera receptkod från en databas, till exempel [!DNL Git], med hjälp av den autentisering och integrering som är tillgänglig mellan [!DNL Git] och [!DNL Data Science Workspace].

### Experimentation

Data Science Workspace ger otrolig flexibilitet i experimenteringsprocessen. Börja med ditt recept. Skapa sedan en separat instans med samma huvudalgoritm i kombination med unika egenskaper, som till exempel avstämningsparametrar. Du kan skapa så många förekomster du behöver, utbilda och betygsätta varje förekomst så många gånger du vill. När du utbildar dem spårar [!DNL Data Science Workspace] recept, recept-instanser och tränade instanser, tillsammans med utvärderingsmått, så du behöver inte det.

### Operationalisering

När du är nöjd med ditt recept är det bara några klick att skapa en intelligent tjänst. Ingen kodning krävs - du kan göra det själv utan att behöva registrera en utvecklare eller tekniker. Publicera slutligen den intelligenta tjänsten på Adobe IO så är den klar att användas av ert team för digitala upplevelser.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Kontinuerlig förbättring

[!DNL Data Science Workspace] spårar var intelligenta tjänster anropas och hur de fungerar. När data rullas in kan du utvärdera den intelligenta tjänstens exakthet för att stänga slingan och träna om recepten efter behov för att förbättra prestandan. Resultatet blir en kontinuerlig förbättring av kundens personalisering.

### Tillgång till nya funktioner och datauppsättningar

Datavetare kan dra nytta av nya tekniker och datauppsättningar så snart de är tillgängliga via Adobes tjänster. Genom de regelbundna uppdateringarna arbetar vi med att integrera datauppsättningar och tekniker i plattformen, så att du inte behöver göra det.

### Säkerhet och sinnesro

Att skydda era data är högsta prioritet för Adobe. Adobe skyddar era data med säkerhetsprocesser och kontroller som utvecklats för att hjälpa er att följa standarder, bestämmelser och certifieringar som godkänts av branschen.

Säkerhet är inbyggd i programvara och tjänster som en del av Adobe Secure Product Lifecycle.
Läs mer om Adobe datasäkerhet och programvarusäkerhet, regelefterlevnad med mera på säkerhetssidan på https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] in action

Förutsättningar och insikter ger den information ni behöver för att leverera en personaliserad upplevelse till alla kunder som besöker er webbplats, kontaktar ert callcenter eller deltar i andra digitala upplevelser. Så här fungerar ditt dagliga arbete med [!DNL Data Science Workspace].

### Definiera problemet

Allt börjar med ett affärsproblem. Ett onlinesamtal behöver till exempel en kontext som hjälper dem att få en negativ kunduppfattning att bli positiv.

Det finns mycket data om kunden. De har besökt webbplatsen, lagt artiklar i varukorgen och till och med lagt beställningar. De kan ha fått e-post, använda kuponger eller kontaktat callcentret tidigare. Mottagaren måste sedan använda tillgängliga data om kunden och deras aktiviteter för att avgöra om det är troligt att kunden kommer att uppskatta och använda ett erbjudande.

![](./images/home/example_problem.png)

Vid kontakten mellan samtalscentret har kunden fortfarande två par skor i kundvagnen, men tog bort en skjorta. Med den här informationen kan den intelligenta tjänsten rekommendera att kundtjänstagenten erbjuder en kupong för 20 % rabatt på skor under samtalet. Om kunden använder kupongen läggs den informationen till i datauppsättningen och prognoserna blir ännu bättre nästa gång kunden ringer.

### Utforska och förbereda data

Beroende på vilket affärsproblem som har definierats vet du att receptet bör undersöka alla kundens webbtransaktioner, inklusive webbplatsbesök, sökningar, sidvisningar, klickade länkar, kundvagnsåtgärder, mottagna erbjudanden, e-postmeddelanden, interaktioner med callcenter osv.

En datavetare ägnar vanligtvis upp till 75 % av den tid som krävs för att skapa ett recept som utforskar och omvandlar data. Data kommer ofta från flera databaser och sparas i olika scheman - de måste kombineras och mappas innan de kan användas för att skapa ett recept.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Om du börjar från början eller konfigurerar ett befintligt recept börjar du sökningen efter data i en centraliserad och standardiserad datakatalog för organisationen, vilket gör sökningen betydligt enklare. Du kan till och med upptäcka att en annan datavetare i organisationen redan har identifierat en liknande datauppsättning och välja att finjustera den datauppsättningen i stället för att börja från början.
Alla data i Adobe Experience Platform följer ett standardiserat XDM-schema, vilket eliminerar behovet av att skapa en komplex modell för att koppla samman data eller få hjälp av en datatekniker.

Om du inte omedelbart hittar de data du behöver, men de finns utanför Adobe Experience Platform, är det en relativt enkel uppgift att importera ytterligare datauppsättningar, som också omvandlas till ett standardiserat XDM-schema.\
Du kan använda [!DNL Jupyter Notebook] för att förenkla förbearbetning av data. Du kan eventuellt börja med en mall för anteckningsbok eller en anteckningsbok som du tidigare har använt för benägenhet att köpa.

![](./images/home/notebook_templates-new.png)

### Skriv receptet

Om du redan har hittat ett recept som uppfyller alla dina behov kan du gå vidare till experimenterande. Eller så kan du ändra receptet lite eller skapa ett från början - utnyttja [!DNL Data Science Workspace]-redigeringsmiljön i [!DNL Jupyter Notebook]. Genom att använda redigeringsmiljön kan du både använda arbetsflödet för utbildning och poängsättning i [!DNL Data Science Workspace] och konvertera receptet senare så att det kan lagras och återanvändas av andra i organisationen.

Du kan även importera ett recept till [!DNL Data Science Workspace] och dra nytta av experimentarbetsflödena när du skapar din intelligenta tjänst.

### Experimentera med receptet

Med ett recept som innehåller dina huvudmaskininlärningsalgoritmer kan många recept skapas med ett enda recept. Dessa recept-instanser kallas för modeller. En modell kräver utbildning och utvärdering för att optimera dess driftseffektivitet och effektivitet, en process som vanligtvis består av en provperiod och ett fel.

![](./images/home/recipe_hiearchy_ui.png)

När du utbildar dina modeller genereras kurser och utvärderingar. [!DNL Data Science Workspace] håller reda på utvärderingsstatistik för varje unik modell och deras utbildning körs. Mätvärden som genereras genom experimenterande kommer att göra det möjligt för er att avgöra vilken utbildning som fungerar bäst.

![](./images/home/evaluation_metrics.png)

Besök [API](./models-recipes/train-evaluate-model-api.md)- eller [användargränssnittet](./models-recipes/train-evaluate-model-ui.md)-självstudiekursen om hur du utbildar och utvärderar modeller i [!DNL Data Science Workspace].

### Operationalisera modellen

När du har valt det bäst utbildade receptet för att tillgodose dina affärsbehov kan du skapa en intelligent tjänst i [!DNL Data Science Workspace] utan hjälp från utvecklare. Det är bara några klick - ingen kodning behövs. En publicerad intelligent tjänst är tillgänglig för andra medlemmar i organisationen utan att modellen behöver återskapas.

En publicerad intelligent tjänst är konfigurerbar för att automatiskt utbilda sig själv emellanåt med nya data allt eftersom de blir tillgängliga. Detta garanterar att din tjänst är effektiv och effektiv även om tiden går.

## Nästa steg

[!DNL Data Science Workspace] hjälper till att effektivisera och förenkla arbetsflödet för datavetenskap, från datainsamling till algoritmer till intelligenta tjänster för datavetare på alla kunskapsnivåer. Med de sofistikerade verktygen i [!DNL Data Science Workspace] kan du avsevärt korta tiden från data till insikter.

Viktigast av allt är att [!DNL Data Science Workspace] förser datavetenskapen och algoritmisk optimeringsfunktionerna i Adobe ledande marknadsföringsplattform med data från företag. För första gången kan företag ta med egna algoritmer till plattformen och dra nytta av Adobe kraftfulla maskininlärnings- och AI-funktioner för att leverera personaliserade kundupplevelser i stor skala.

I och med samgåendet mellan varumärkesexpertis och Adobe maskininlärning och AI-processer har företag möjlighet att öka affärsvärdet och varumärkeslojaliteten genom att ge kunderna det de vill ha, innan de ber om det.

Om du vill ha mer information, t.ex. ett komplett arbetsflöde, kan du börja med att läsa [Data Science Workspace-dokumentationen ](./walkthrough.md).

## Ytterligare resurser

Följande video har utformats för att ge stöd för din förståelse av [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)