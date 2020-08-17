---
keywords: Experience Platform;home;popular topics;offer management;Offer Management
solution: Experience Platform
title: Domänmodell för beslut om erbjudande
topic: overview
description: Avtalsbeslut är ett användbart fall av beslutstjänst där ni formaliserar och centralt hanterar de regler och prognoser som används för att engagera kunder med erbjudanden.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '2640'
ht-degree: 0%

---


# Översikt över domänmodellen för beslut om erbjudande

Att fatta beslut om erbjudanden är ett exempel på hur ni formaliserar och centralt hanterar de regler och prognoser som används för att engagera kunderna med erbjudanden. [!DNL Decisioning Service] Avtalsbeslut är en typ av _**innehållsbeslut**_. I detta fall kallas _**beslutsalternativen**_ _**erbjudanden**_ och karakteriseras som sådana av innehållet i dem. En introduktion till objektmodellen som används av [!DNL Decisioning Service]finns i Domänmodell för [beslutstjänst](experience-model.md).

Målet är att ge slutanvändaren&quot;bästa erbjudandet&quot; i alla kanaler baserat på kriterier för målinriktning, kostnader och frekvensbegränsningar samt föregående interaktioner över alla kanaler inklusive tidigare erbjudanden.

Precis som med alla beslutsärenden hanteras beslutsalternativen (erbjudandena) i en databas som delas av ett valfritt antal program. Erbjudandena kan skapas av olika avdelningar inom organisationen eller av partners, och dessa erbjudanden kan läggas till och tas bort varje dag.

Erbjudandena placeras visuellt i större upplevelser av det program som levererar upplevelsen. _**Placeringar**_, som ibland kallas fläckar eller kortplatser, är viktiga komponenter för att skapa en strategi. Utformningen av en strategi för erbjudanden börjar ofta med definitionen av dessa ersättningar. Ett erbjudande innehåller vanligtvis flera _**innehållsrepresentationer**_ så att det kan integreras korrekt i en mängd olika upplevelser, där varje erbjudande har olika dimensionella eller andra begränsningar och kräver olika medieformat.

Erbjudandena har ofta en koppling till fysiska varor eller tjänster och det finns en kostnadsberäkning. En organisation måste kunna begränsa de resurser som förbrukas av erbjudanden och måste därför kunna _**begränsa**_ det totala antalet gånger ett erbjudande kan föreslås.

Det förutspådda värdet av ett accepterat erbjudande till organisationen är optimeringskriterierna och står i strid med kostnaden för att göra ett erbjudande. Kostnad, sannolikhet för godkännande och förväntat värde används för att rangordna erbjudandena. Det bästa erbjudandet är det som har störst förväntad positiv effekt på målen för era erbjudandeaktiviteter.

I offertbeslutet beaktas de interaktioner som en slutanvändare hade, _**i många kanaler**_ och i många tillämpningar, vilket utnyttjar slutanvändarens profil- och upplevelsehändelsedata. Exempelvis kan en call center-applikation använda offertbeslut för att aktivera eller inaktivera ett erbjudande baserat på inköp och recensioner som slutanvändaren gjort. eller ett e-posthanteringsprogram kan förlita sig på att Offer Decisioning väljer Nästa bästa erbjudande i ett veckonyhetsbrev baserat på webbsidans webbhistorik.

Erbjudandena har andra intressanta egenskaper. Ofta finns det ett definierat _**schema**_ eller datum- och tidsintervall när erbjudandet är giltigt och när erbjudandet måste ogiltigförklaras.

Slutligen försämras det sätt på vilket ett erbjudande överklagas med den frekvens som det presenteras. Ett erbjudande som inte accepteras efter att ha föreslagits upprepade gånger är en förlorad möjlighet eftersom ett annat erbjudande kan ha presenterats. Av den anledningen måste slutanvändarens _**trötthet**_ hanteras.

## Fatta en överblick över beslutsstrategin

Det övergripande tillvägagångssättet är att begränsa urvalet av erbjudanden tills alla begränsningar är uppfyllda, sedan tillämpa rangordningsmodellen på de återstående alternativen och sedan optimera för flera aktiviteter med hjälp av begränsningar för begränsning (borttagning av dubbletter och undvikande av reservval).

| Strategisk komponent | Realiserat som |
| --- | --- |
| Beslutsverksamhet | Erbjudandeaktiviteter |
| Beslutsalternativ | Erbjud med innehållsrepresentationer |
| Reservalternativ | Reserverbjudande med innehållsrepresentationer |
| Finite set of Decision options | Erbjud lager (alias erbjudandebibliotek) |
| Aktuella kategorier | Erbjud filter baserat på taggar och erbjudandeidentifierare |
| Beslutsresultat | Ett erbjudande per aktivitet, för flera aktiviteter samtidigt |
| Beslutsresultat | Förväntad upplevelsehändelse med referens till erbjudandet, t.ex. `eventType='opened'` |
| Beslutsalgoritm | Intern tjänstlogik, parametriserad |
| Begränsningar | Placeringsbegränsningar, kalenderbegränsningar, begränsningar för global appning och begränsning per användare, begränsningar för borttagning av dubbletter |
| Beslutsregler | Villkor |
| Modell för *förväntat verktyg* | Prioritet eller prioritet |

Det totala antalet erbjudanden i optionsförteckningen är vanligtvis ganska stort (i storleksordningen 10 000) och varje erbjudandeaktivitet kan fokuseras på erbjudanden som hör till en annan kategori (ämne). Med beslutsstrategin för erbjudandet kan ett erbjudandefilter bifogas till en erbjudandeaktivitet. Ytterligare begränsningar kommer att utvärderas när beslutet begärs.
I följande avsnitt beskrivs komponenterna för domänen för beslut om erbjudande i detalj.

## Allmänna erbjudanden

Allmänna erbjudanden, som också kallas personaliserade erbjudanden, är alternativen som är central för beslutsprocesserna för erbjudandet. De har attribut som namn och status. Statusattributet anger om enheten är redo att inkluderas i listan över aktiva godkända erbjudanden. Allmänna erbjudanden har flera begränsningar. Mer information om detta finns i ‎ Begränsningar [nedan](#offer-constraints).

## Innehåll i erbjudanden

### Erbjudandeplaceringar

Placeringar definierar innehållsbegränsningar och används med en aktivitet för att ange var nästa bästa upplevelse ska levereras. Detta minskar ytterligare antalet alternativ som kan övervägas och är en annan begränsning som aktiviteten medför. Detta kallas placeringsbegränsning. Endast alternativ som har innehåll som uppfyller en placeringsbegränsning, till exempel erbjudanden, kommer att beaktas. Detta utvärderas i de tidiga faserna av beslutsstrategin. När alternativobjekt ändrar placeringsbegränsningarna för varje aktivitet omprövas och alternativet kan beaktas eller tas bort för en eller flera aktiviteter.

Det är inte företagets ansvar [!DNL Decisioning Service] att formalisera de komplexa detaljerna i innehållsberoenden. Istället kommer varje kund att identifiera listan över placeringar i alla kanaler och ge dessa placeringar unika identifierare och namn. Genom att referera till en viss placering försäkrar designern att det angivna innehållet passar in på placeringen.

När innehållet har utvecklats kommer erbjudandemarknadsföraren och innehållsdesignern att helt enkelt (måste) komma överens om ett&quot;underförstått kontrakt&quot; som står bakom namnet&quot;Home Page Hero Image&quot; eller&quot;Service Call Opening Script&quot;. Den första kan överenskommas som en bild med bredden 600 px och höjden 350 px och den senare kan begränsa innehållet till text i två språkvarianter som inte är längre än 50 ord i tre eller fyra meningar med semantisk struktur. Placering som inte lagrar hela innebörden av det dolda kontraktet.

### Erbjudanderepresentationer

För att ett erbjudande ska kunna presenteras på rätt sätt i de olika parametrarna för placeringarna i era kanaler måste olika representationer av det erbjudandet skapas. Innehållet som är kopplat till erbjudanden grupperas efter placeringar. Varje erbjudande kan ha en eller flera representationer där var och en av representationerna refererar till en av de definierade placeringarna. Varje representation i ett erbjudande måste ha en annan placering. Ju fler utfästelser ett erbjudande har desto fler möjligheter finns att använda erbjudandet i olika placeringssammanhang.

En placering begränsar vilken typ av innehållsobjekt som kan läggas till i representationen.

## Reserverbjudanden

Reserverbjudanden är beslutsalternativ som inte har ytterligare begränsningar förutom placeringsreglerna. Reserverbjudanden har innehållsrepresentationer som är kopplade till placeringar, precis som alla andra erbjudanden.

Reserverbjudanden anges i aktiviteter för att indikera en livskraftig innehållsupplevelse när kombinerade begränsningar diskvalificerar alla begränsade alternativ. Eftersom det inte är beroende av körningssammanhanget eller profilen, kan placeringsbegränsningen kontrolleras i förväg när aktiviteten sätts samman. Med hjälp av reserverbjudanden finns det alltid ett svar på frågan: Vilket är för närvarande det bästa erbjudandet?

## Villkor

### Kalenderbegränsningar

I beslutsdomänen för erbjudanden har erbjudandena en giltighetsperiod. Det innebär att erbjudandet inte kan föreslås innan dess startdatum och starttid har passerat och inte kan föreslås längre efter slutdatumet och sluttiden har passerat. Erbjudandeentiteten har en enkel struktur som definierar dessa kalenderbegränsningar.

Utgångna erbjudanden tas regelbundet bort från listan över aktuella alternativ. Men kalenderfiltret tillämpas direkt när beslutet begärs så att begränsningarna tillämpas med precision.

### Begränsningar

Erbjudandena kan ha en valfri begränsning. Det består av två värden:

- Det globala begränsningsvärdet begränsar hur ofta ett erbjudande kan föreslås i hela profiluppsättningen (målgrupp).

- Anfangen per profil och avgör hur ofta erbjudandet kan föreslås för samma profil.

### Dupliceringsbegränsningar

När ett beslut begärs kan kunden begära förslag för flera aktiviteter samtidigt. Detta är ett typiskt scenario vid innehållsbeslut. Varje aktivitet bidrar till ett eller flera innehållsalternativ för den övergripande upplevelsen. På grund av dispositionsaspekten måste beslut skiljas åt mellan aktiviteter för att undvika dubblering - såvida inte aktiviteterna var och en väljer en av de osammanhängande delarna av det totala optionsinventeringen. Ett högt rankat alternativ kommer sannolikt att rangordnas högt i alla verksamheter och det skulle vara en dålig erfarenhet om alla aktiviteter föreslog samma alternativ. Å andra sidan, om ett leveranssystem vill veta vad nästa bästa konvertering är i alla kanaler och det inte finns någon begränsning, kan det vara ok att föreslå samma alternativ för olika aktiviteter.

Dupliceringsbegränsningar skrivs för närvarande inte in i affärsobjektdatabasen. I stället är deduplicering standardstrategi vid körning. En begärandeparameter kan åsidosätta standardbeteendet för att förhindra borttagning av dubbletter.

### [!DNL Profile] begränsningar - regler för behörighet

Till dags dato har de villkor som diskuterats varit tillämpliga oavsett vem som har valt erbjudandet. Experience Decision stöder också ett användningsexempel där personalisering av erbjudanden baseras på kundens rekordhändelser och tidsseriehändelser. Regler utvärderas per profil för att avgöra om ett erbjudande kvalificerar eller måste ignoreras för den användaren. För att göra det kan en berättiganderegel kopplas till varje erbjudande. Förutom profil- och upplevelsehändelser för en slutanvändare beaktas kontextdata i realtid i berättiganderegeln. Dessa data tillhandahålls av leveranstjänsten och kan ha en form av data som inte är relaterade till en profil som lagernivåer, väderförhållanden och flygscheman.

Det är viktigt att skilja mellan målinriktning och segmenteringsregler samt mellan regler för behörighet och prioritering för beslut. För målgruppsanpassning är en uppsättning profiler utdata (målgruppsval) för kvalificering. En uppsättning alternativ (tillåtna erbjudanden) är resultatet av utvärderingen.

## Erbjud samlingar

Lagret är den övergripande poolen med alternativ som beaktas för beslut. Lagret kan delas upp ytterligare i kategorier eller samlingar. En uppsättning alternativ representeras av en gemensam tagg som dessa alternativ har. Filter används för att testa om erbjudanden tillhör en viss kategori, eller mer specifikt, delar samma tagg eller taggar.

### Taggar

Taggar är ett sätt att uttrycka att en grupp med alternativ tillhör en kategori.

Ett alternativ kan ha mer än en tagg och kan därför finnas i flera kategorier samtidigt. Kategorier kan också överlappa eller innehålla andra kategorier. När en kategori &quot;S&quot; definieras av erbjudanden som har taggen &quot;A&quot; och kategorin &quot;R&quot; definieras av alternativ med både taggen &quot;A&quot; och &quot;B&quot;, kommer &quot;S&quot; att vara en överordnad kategori till &quot;R&quot;.

### Filter

Filter används för att definiera villkor för en uppsättning alternativ som tillhör en kategori. Man kan tänka på filter som frågor mot lagret med allmänna erbjudanden. Det finns två grundläggande sätt att skapa ett filter: genom att ange att ett erbjudande har en eller flera taggar och genom att välja erbjudandeuppsättningen explicit. Den tidigare metoden kan konfigureras för att ange att ett erbjudande i samlingen måste ha alla angivna taggar eller att ett alternativ kvalificerar sig när det har minst en av de angivna taggarna.

När alternativ placeras explicit i en samling ignoreras deras tagguppsättning för den samlingen.

## Erbjudandeaktiviteter

Aktiviteter som konfigurerar och styr beslutsprocessen. Beslutsstrategin är för närvarande i första hand förbestämd, men framtida versioner av domänmodellen för beslut om erbjudanden gör det möjligt att välja modeller, ytterligare regler och begränsningar.

En upplevelse kan sammanställas med många aktiviteter samtidigt. För närvarande kan upp till 30 aktiviteter hanteras i en enda beslutsbegäran. Om fler än 30 aktiviteter eller kortplatser i en upplevelse måste fyllas med innehåll, kan flera begäranden göras för samma profil. När verksamheter ingår i samma beslutsbegäran kommer dock dubbla erbjudandeförslag att tas bort bland dessa verksamheter.

Om aktiviteter definieras på ett sätt som de väljer bland osammanhängande erbjudanden gör det liten skillnad om aktiviteter kombineras i samma begäran eller delas upp i separata förfrågningar. Nätverks- och svarstidsbegränsningar kan dock kräva att aktiviteter kombineras i samma begäran. Eftersom olika förfrågningar kan dirigeras till olika tjänstnoder kan samma profildata behöva hämtas till olika noder. Detta minskar den effektiva IO-bandbredden som är tillgänglig för andra begäranden.

Aktiviteter används för att infoga innehåll i en upplevelse. För att göra det lättare (inte för att säkerställa) att innehållsobjekten&quot;passar&quot; korrekt refererar en aktivitet till en enda placering. Observera att en placering inte alltid är en konkret plats/plats, utan snarare en abstraktion av dessa platser/platser. På en webbsida med ett rutnät med rutor kan till exempel varje platta styras av samma placering, förutsatt att de har samma form och storlek och kan innehålla liknande innehåll. En enskild platta levereras dock vanligtvis genom sin egen aktivitet.

I följande bild visas hur affärsföretagen är sinsemellan besläktade:

![](./images/figure-10.png)

När klienter skapar och länkar objektdiagrammet för beslut finns det vanligtvis tre olika arbetsflöden. Dessa är följande:

- Konfigurera stödentiteter som taggar och placeringar. Dessa enheter används för att strukturera, filtrera och gruppera andra enheter. De används också för att ge viss samordning mellan det andra och tredje arbetsflödet. Det här arbetsflödet utgör en del förarbete, men vid en given tidpunkt kan du göra finjusteringar av inställningarna. Taggar är relativt enkla, men placeringar kräver lite mer planering. Företaget måste åtminstone inventera alla platser där ett beslut presenteras.

- Skapa erbjudanden med olika representationer och affärsregler (begränsningar). Detta centrala arbetsflöde ger de alternativ bland vilka vi behöver välja de bästa. Taggarna i det första arbetsflödet används för att kategorisera erbjudanden och placeringarna används för att ange vilka alternativ som kan presenteras och var.

   - Det här arbetsflödet definierar även absoluta begränsningar för erbjudandena. De är absoluta eftersom de alltid kommer att tillämpas och inte bara påverkar rangordningen av ett antal erbjudanden. När till exempel en kalenderbegränsning är inställd tvingas erbjudandet att aldrig väljas före det angivna startdatumet/den angivna starttiden och aldrig efter slutdatumet/sluttiden. Begränsningarna som kommer att anges i det här arbetsflödet är [kalenderbegränsningar](#calendar-constraints), [begränsningar](#capping-constraints) för [begränsning och](#profile-constraints---eligibility-rules)behörighetskrav. Ett delarbetsflöde här är definitionen av ytterligare regler som avgör vem som är berättigad att ta emot ett visst erbjudande.

      - Samtidigt som begränsningar skapas för ett erbjudande väljs dess representationer. Det här arbetsflödet förutsätter att innehållet redan har skapats någonstans och helt enkelt överförs till och väljs från innehållsdatabasen. Här kommer placeringarna från det första arbetsflödet att spelas upp. Ett erbjudande kan välja praktik och associera innehållet under den [placeringen](#offer-placements).

      - Det sista steget i det här arbetsflödet är att skapa lämpliga reserverbjudanden. Ett reserverbjudande är i princip som ett allmänt erbjudande utan begränsningar.

- Det sista arbetsflödet handlar om att skapa aktiviteter. Detta steg behöver dock inte nödvändigtvis inträffa sekventiellt efter arbetsflödet för att skapa erbjudanden. Båda processerna är pågående och samtidiga. Verksamheter används för att begränsa omfattningen av alternativen efter ämne och plats där besluten presenteras. En aktivitet refererar till en [samling](#offer-collections) och en placering. Det måste också ange ett [reserverbjudande](#fallback-offers) som används i de fall där ett kvalificerande erbjudande inte kan fastställas.

