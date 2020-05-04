---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grunderna för schemakomposition
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Grunderna för schemakomposition

Det här dokumentet innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i Adobe Experience Platform. Allmän information om XDM och hur det används inom plattformen finns i [XDM-systemöversikten](../home.md).

## Scheman

Ett schema är en uppsättning regler som representerar och validerar datastrukturen och dataformatet. På en hög nivå ger scheman en abstrakt definition av ett objekt i verkligheten (till exempel en person) och ger en översikt över vilka data som ska inkluderas i varje instans av objektet (till exempel förnamn, efternamn, födelsedag o.s.v.).

Förutom att beskriva datastrukturen, tillämpar scheman begränsningar och förväntningar på data så att de kan valideras när de flyttas mellan olika system. Med dessa standarddefinitioner kan data tolkas på ett enhetligt sätt, oavsett ursprung, och behovet av översättning mellan olika program försvinner.

Experience Platform upprätthåller denna semantiska normalisering med hjälp av scheman. Scheman är standardmetoden för att beskriva data i Experience Platform, vilket gör att alla data som uppfyller scheman kan återanvändas utan konflikter i en organisation och till och med delas mellan flera organisationer.

### Relationstabeller jämfört med inbäddade objekt

När du arbetar med relationsdatabaser omfattar de bästa metoderna att normalisera data, eller att ta en enhet och dela upp den i separata delar som sedan visas i flera tabeller. För att kunna läsa data som helhet eller uppdatera enheten måste läs- och skrivåtgärder utföras i många enskilda tabeller med JOIN.

Genom att använda inbäddade objekt kan XDM-scheman representera komplexa data direkt och lagra dem i självständiga dokument med hierarkisk struktur. En av de största fördelarna med den här strukturen är att den gör det möjligt att fråga efter data utan att behöva rekonstruera enheten med dyrbara kopplingar till flera deformerade tabeller.

### Scheman och big data

Moderna digitala system genererar enorma mängder beteendesignaler (transaktionsdata, webbloggar, internet med mera). Dessa stora data ger fantastiska möjligheter att optimera upplevelser, men är svåra att använda på grund av datans storlek och variation. För att få ut mer av uppgifterna måste datastrukturen, formatet och definitionerna standardiseras så att de kan behandlas enhetligt och effektivt.

Scheman löser detta problem genom att data kan integreras från flera källor, standardiseras med gemensamma strukturer och definitioner och delas mellan olika lösningar. Detta gör att efterföljande processer och tjänster kan besvara alla typer av frågor som ställs om data, vilket innebär att man kan gå ifrån den traditionella metoden med datamodellering där alla frågor som ställs om data är kända i förväg och data är modellerade för att uppfylla dessa förväntningar.

### Schemabaserade arbetsflöden i Experience Platform

Standardisering är ett nyckelbegrepp bakom Experience Platform. XDM, som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera standardscheman för kundupplevelsehantering.

Infrastrukturen som Experience Platform bygger på, som kallas XDM-system, underlättar schemabaserade arbetsflöden och innehåller schemaregister, schemaredigerare, schemadata och tjänstkonsumtionsmönster. Mer information finns i [XDM-systemöversikten](../home.md) .

## Planera ditt schema

Det första steget i att skapa ett schema är att fastställa konceptet, eller det verkliga objektet, som du försöker fånga inom schemat. När du har identifierat det koncept du försöker beskriva kan du börja planera ditt schema genom att tänka på saker som datatyp, potentiella identitetsfält och hur schemat kan utvecklas i framtiden.

### Databeteenden i Experience Platform

Data som är avsedda att användas i Experience Platform är grupperade i två beteendetyper:

* **Postdata**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsseriedata**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats **klass**, som tilldelas ett schema när det skapas för första gången. XDM-klasser beskrivs mer ingående senare i det här dokumentet.

Både schema för post- och tidsserier innehåller en karta över identiteter (`xdm:identityMap`). Det här fältet innehåller identitetsbeteckningen för ett ämne, som har ritats från fält markerade som &quot;Identitet&quot; enligt beskrivningen i nästa avsnitt.

### Identitet

Scheman används för att importera data till Experience Platform. Dessa data kan användas för flera tjänster för att skapa en enda, enhetlig vy av en enskild enhet. Därför är det viktigt att tänka på scheman för att tänka på&quot;Identitet&quot; och vilka fält som kan användas för att identifiera ett ämne oavsett varifrån data kommer.

Nyckelfält kan markeras som Identitet om du vill ha hjälp med den här processen. När data matas in infogas uppgifterna i dessa fält i &quot;Identitetsdiagram&quot; för den personen. Diagramdata kan sedan nås av kundprofilen [i](../../profile/home.md) realtid och andra Experience Platform-tjänster för att ge en sammanslagen bild av varje enskild kund.

Fält som vanligen markeras som&quot;Identitet&quot; är: e-postadress, telefonnummer, [Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/en/id-service/using/home.html), CRM ID eller andra unika ID-fält. Du bör också ta hänsyn till unika identifierare som är specifika för din organisation, eftersom de även kan vara bra&quot;identitetsfält&quot;.

Det är viktigt att tänka på kundens identiteter under schemaplaneringsfasen för att säkerställa att data samlas ihop för att skapa en så robust profil som möjligt. Se översikten över [](../../identity-service/home.md) identitetstjänsten för att få veta mer om hur identitetsinformation kan hjälpa er att leverera digitala upplevelser till era kunder.

### Principer för schemautveckling {#evolution}

I takt med att de digitala upplevelserna utvecklas måste även de scheman som används för att representera dem finnas kvar. Ett väldesignat schema kan därför anpassas och utvecklas efter behov, utan att det medför destruktiva ändringar i tidigare versioner av schemat.

Eftersom bakåtkompatibilitet är avgörande för schemautvecklingen, tillämpar Experience Platform en rent additiv versionsprincip för att säkerställa att eventuella ändringar av schemat endast resulterar i icke-förstörande uppdateringar och ändringar. Med andra ord stöds inte **brytningsändringar.**

| Ändringar som stöds | Brytande ändringar (stöds inte) |
|------------------------------------|---------------------------------|
| <ul><li>Lägga till nya fält i ett befintligt schema</li><li>Göra ett obligatoriskt fält valfritt</li></ul> | <ul><li>Tar bort tidigare definierade fält</li><li>Nya obligatoriska fält</li><li>Byta namn på eller definiera om befintliga fält</li><li>Ta bort eller begränsa fältvärden som tidigare stöds</li><li>Flytta attribut till en annan plats i trädet</li></ul> |

>[!NOTE] Om ett schema ännu inte har använts för att importera data till Experience Platform kan du införa en brytningsändring i det schemat. När schemat har använts i Platform måste det dock följa den additiva versionsprincipen.

### Scheman och datainhämtning

För att kunna importera data till Experience Platform måste en datauppsättning först skapas. Datauppsättningar är byggstenarna för dataomvandling och spårning för [katalogtjänsten](../../catalog/home.md), och representerar vanligtvis tabeller eller filer som innehåller inkapslade data. Alla datauppsättningar baseras på befintliga XDM-scheman, som innehåller begränsningar för vad de inmatade data ska innehålla och hur de ska struktureras. Mer information finns i översikten om [Adobe Experience Platform Data Ingmit](../../ingestion/home.md) .

## Bygga block i ett schema

Experience Platform använder en dispositionsmetod där standardbyggstenar kombineras för att skapa scheman. Den här metoden främjar återanvändbarheten av befintliga komponenter och driver standardiseringen i hela branschen för att stödja leverantörsscheman och komponenter i Platform.

Scheman består av följande formel:

**Class + Mixin&amp;ast; = XDM-schema**

&amp;ast;Ett schema består av en klass och _noll eller flera_ blandningar. Det innebär att du kan komponera ett datamängdsschema utan att använda blandningar alls.

### Klass

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

En klass avgör också vilka mixiner som är berättigade att användas i schemat. Detta diskuteras mer ingående i [avsnittet med](#mixin) blandningar som följer.

Det finns standardklasser i varje integrering av Experience Platform, så kallade branschklasser. Branschklasser är allmänt vedertagna branschstandarder som gäller ett brett urval av användningsområden. Exempel på branschklasser är XDM Individual Profile och XDM ExperienceEvent-klasser från Adobe.

Experience Platform tillåter också&quot;leverantörsklasser&quot;, som är klasser som definieras av Experience Platform-partners och som görs tillgängliga för alla kunder som använder den leverantörstjänsten eller -tillämpningen inom Platform.

Det finns också klasser som används för att beskriva mer specifika användningsfall för enskilda organisationer inom plattformen, så kallade&quot;kundklasser&quot;. Kundklasser definieras av en organisation när det inte finns några bransch- eller leverantörsklasser tillgängliga som beskriver ett unikt användningsfall.

Ett schema som till exempel representerar medlemmar i ett lojalitetsprogram beskriver postdata om en individ och kan därför baseras på klassen XDM Individual Profile, en standardbranschklass som definierats av Adobe.

### Mixa {#mixin}

En mixin är en återanvändbar komponent som definierar ett eller flera fält som implementerar vissa funktioner, som personlig information, hotellinställningar eller adress. Mixer är avsedda att ingå i ett schema som implementerar en kompatibel klass.

Blandningar definierar vilka klasser de är kompatibla med utifrån beteendet hos de data de representerar (post- eller tidsserier). Det innebär att inte alla blandningar finns tillgängliga för användning med alla klasser.

Mixer har samma omfång och definition som klasser: det finns branschblandningar, leverantörsmixiner och kundmixar som definieras av enskilda organisationer som använder Platform. Experience Platform innehåller många branschstandardblandningar och gör det även möjligt för leverantörer att definiera mixiner för sina användare, och för enskilda användare att definiera mixiner för sina egna specifika koncept.

Om du till exempel vill ta med information som Förnamn och Hemadress för ditt schema&quot;Förmånsmedlemmar&quot;, kan du använda standardblandningar som definierar de vanliga begreppen. Begrepp som är specifika för mindre vanliga användningsområden (t.ex.&quot;Loyalty Program Level&quot;) har ofta ingen fördefinierad blandning. I så fall måste du definiera en egen blandning för att kunna hämta in den här informationen.

Kom ihåg att scheman består av &quot;noll eller flera&quot;-blandningar, vilket innebär att du kan skapa ett giltigt schema utan att använda några mixiner alls.

### Datatyp {#data-type}

Datatyper används som referensfälttyper i klasser eller scheman på samma sätt som grundläggande litteralfält. Den största skillnaden är att datatyper kan definiera flera underfält. En datatyp liknar en blandning, men har större flexibilitet än en blandning eftersom en datatyp kan inkluderas var som helst i ett schema genom att lägga till den som&quot;datatyp&quot; för ett fält.

Experience Platform tillhandahåller ett antal vanliga datatyper som en del av schemaregistret som stöder användningen av standardmönster för att beskriva vanliga datastrukturer. Detta förklaras mer ingående i självstudiekurserna för schemaregister, där det blir tydligare när du går igenom stegen för att definiera datatyper.

### Fält

Ett fält är den mest grundläggande byggstenen i ett schema. Fält innehåller begränsningar för vilken typ av data de kan innehålla genom att definiera en viss datatyp. Dessa grundläggande datatyper definierar ett enda fält, medan de [datatyper](#data-type) som tidigare nämnts gör det möjligt att definiera flera delfält och återanvända samma flerfältsstruktur i olika scheman. Förutom att definiera ett fälts&quot;datatyp&quot; som en av de datatyper som definieras i registret, stöder Experience Platform grundläggande skalära typer som:

* Sträng
* Heltal
* Siffra
* Boolean
* Array
* Objekt

Giltiga intervall för dessa skalära typer kan begränsas ytterligare till vissa mönster, format, minimum/maximum eller fördefinierade värden. Med dessa begränsningar kan en mängd mer specifika fälttyper visas, bland annat:

* Enum
* Lång
* Kort
* Byte
* Datum
* Datum-tid
* Karta

>[!NOTE] Fälttypen &quot;map&quot; tillåter nyckelvärdepar, inklusive flera värden för en enskild nyckel. Kartor kan bara definieras på systemnivå, vilket innebär att du kan stöta på en karta i ett bransch- eller leverantörsdefinierat schema, men den är inte tillgänglig för användning i fält som du definierar. Utvecklarhandboken för [schemaregister-API:t](../api/getting-started.md) innehåller mer information om hur du definierar fälttyper.

Vissa dataåtgärder som används av underordnade tjänster och program tillämpar begränsningar för specifika fälttyper. De tjänster som påverkas är bland annat följande:

* [Kundprofil i realtid](../../profile/home.md)
* [Identitetstjänst](../../identity-service/home.md)
* [Segmentering](../../segmentation/home.md)
* [Frågetjänst](../../query-service/home.md)
* [Datavetenskapens arbetsyta](../../data-science-workspace/home.md)

Innan du skapar ett schema för användning i underordnade tjänster bör du läsa lämplig dokumentation för dessa tjänster för att bättre förstå fältkraven och begränsningarna för de dataåtgärder som schemat är avsett för.

### XDM-fält

Förutom grundläggande fält och möjligheten att definiera egna datatyper tillhandahåller XDM en standarduppsättning med fält och datatyper som är implicit förstådda av Experience Platform-tjänster och som ger större enhetlighet när de används i olika plattformskomponenter.

Dessa fält, till exempel&quot;Förnamn&quot; och&quot;E-postadress&quot;, innehåller nya konnoteringar utöver de grundläggande skalära fälttyperna, vilket innebär att alla fält som delar samma XDM-datatyp fungerar på samma sätt. Detta beteende kan betraktas som tillförlitligt oavsett varifrån data kommer eller i vilken plattformstjänst data används.

En fullständig lista över tillgängliga XDM-fält finns i [XDM-fältordlistan](field-dictionary.md) . Vi rekommenderar att du använder XDM-fält och datatyper där det är möjligt för att stödja enhetlighet och standardisering i hela Experience Platform.

## Kompositionsexempel

Scheman representerar format och struktur för data som ska hämtas till plattformen och byggs med en kompositionsmodell. Som tidigare nämnts består dessa scheman av en klass och noll eller flera blandningar som är kompatibla med den klassen.

Ett schema som beskriver inköp som görs i en butik kan till exempel kallas&quot;Butikstransaktioner&quot;. Schemat implementerar klassen XDM ExperienceEvent i kombination med den vanliga Commerce-mixin och en användardefinierad Product Info-mixin.

Ett annat schema som spårar webbplatstrafiken kan kallas &quot;Web Visits&quot;. Den implementerar även klassen XDM ExperienceEvent, men den här gången kombineras standardwebbmixen.

Diagrammet nedan visar dessa scheman och fälten från varje blandning. Den innehåller också två scheman baserade på klassen XDM Individual Profile, inklusive schemat &quot;Loyalty Members&quot; som nämndes tidigare i den här guiden.

![](../images/schema-composition/composition.png)

### Union {#union}

Med Experience Platform kan ni sammanställa scheman för särskilda användningsfall, men ni kan också se en &quot;union&quot; av scheman för en viss klasstyp. I det föregående diagrammet visas två scheman baserade på klassen XDM ExperienceEvent och två scheman baserade på klassen XDM Individual Profile. Unionen, som visas nedan, samlar fälten för alla scheman som delar samma klass (XDM ExperienceEvent respektive XDM Individual Profile).

![](../images/schema-composition/union.png)

Genom att aktivera ett schema för användning med kundprofilen i realtid, inkluderas det i unionen för den typen av klass. Profilen ger robusta, centraliserade profiler av kundattribut samt ett tidsstämplat konto för varje händelse som kunden har haft i alla system som är integrerade med plattformen. Profilen använder unionsvyn för att representera dessa data och ge en helhetsbild av varje enskild kund.

Mer information om hur du arbetar med profil finns i [Kundprofilöversikt](../../profile/home.md)i realtid.

## Mappa datafiler till XDM-scheman

Alla datafiler som hämtas till Experience Platform måste överensstämma med strukturen i ett XDM-schema. Mer information om hur du formaterar datafiler så att de överensstämmer med XDM-hierarkier (inklusive exempelfiler) finns i dokumentet om ETL- [omformningar](../../etl/transformations.md). Allmän information om hur du importerar datafiler till Experience Platform finns i översikten över [batchöverföring](../../ingestion/batch-ingestion/overview.md).

## Nästa steg

Nu när du förstår grunderna i schemakomposition kan du börja skapa scheman med schemaregistret.

Schemaregistret används för att komma åt schemabiblioteket i Adobe Experience Platform och innehåller ett användargränssnitt och RESTful API från vilket alla tillgängliga biblioteksresurser är tillgängliga. Schemabiblioteket innehåller branschresurser som definierats av Adobe, leverantörsresurser som definierats av Experience Platform-partners samt klasser, mixins, datatyper och scheman som har skapats av medlemmar i organisationen.

Om du vill börja skapa schemat med hjälp av användargränssnittet följer du med [schemaredigerarens självstudiekurs](../tutorials/create-schema-ui.md) för att skapa det schema för lojalitetsmedlemmar som omnämns i hela dokumentet.

Börja med att läsa utvecklarhandboken för API:t för [schematabeller](../api/getting-started.md)för att börja använda API:t för schemataregistret. När du har läst utvecklarhandboken följer du de steg som beskrivs i självstudiekursen om hur du [skapar ett schema med API:t](../tutorials/create-schema-api.md)för schemaregister.
