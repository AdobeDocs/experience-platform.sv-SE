---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;enum;mixin;fältgrupp;fältgrupper;mixins;datatyp;datatyp;datatyp;datatyp;primär identitet;primär identitet;XDM-individuell profil;XDM-fält;enum datatyp;Experience event;XDM ExperienceEvent;experienceEvent;XDM ExperienceEvent;schema;design;klass;klass;klasser;klasser;datatyp;datatyp;datatyp;datatyp;datatyp;scheman;scheman;identityMap;identity map;identity map;schema design;map;union schema;union
solution: Experience Platform
title: Grundläggande om schemakomposition
topic-legacy: overview
description: Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 9786b810d7b203300db49637039dc034a70f95a7
workflow-type: tm+mt
source-wordcount: '3616'
ht-degree: 0%

---

# Grunderna för schemakomposition

Det här dokumentet innehåller en introduktion till [!DNL Experience Data Model]-scheman (XDM) och de byggstenar, principer och bästa metoderna för att komponera scheman som ska användas i Adobe Experience Platform. Allmän information om XDM och hur det används i [!DNL Platform] finns i [XDM-systemöversikt](../home.md).

## Scheman

Ett schema är en uppsättning regler som representerar och validerar datastrukturen och dataformatet. På en hög nivå ger scheman en abstrakt definition av ett objekt i verkligheten (till exempel en person) och ger en översikt över vilka data som ska inkluderas i varje instans av objektet (till exempel förnamn, efternamn, födelsedag o.s.v.).

Förutom att beskriva datastrukturen, tillämpar scheman begränsningar och förväntningar på data så att de kan valideras när de flyttas mellan olika system. Med dessa standarddefinitioner kan data tolkas på ett enhetligt sätt, oavsett ursprung, och behovet av översättning mellan olika program försvinner.

[!DNL Experience Platform] underhåller denna semantiska normalisering med hjälp av scheman. Scheman är standardsättet att beskriva data i [!DNL Experience Platform], vilket gör att alla data som överensstämmer med scheman kan återanvändas i en organisation utan konflikter, eller till och med delas mellan flera organisationer.

XDM-scheman är idealiska för att lagra enorma mängder komplexa data i ett självständigt format. Se avsnitten om [inbäddade objekt](#embedded) och [big data](#big-data) i bilagan till det här dokumentet för mer information om hur XDM gör detta.

### Schemabaserade arbetsflöden i [!DNL Experience Platform]

Standardisering är ett nyckelbegrepp bakom [!DNL Experience Platform]. XDM, som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera standardscheman för kundupplevelsehantering.

Infrastrukturen som [!DNL Experience Platform] byggs på, kallas [!DNL XDM System], underlättar schemabaserade arbetsflöden och innehåller mönstren [!DNL Schema Registry], [!DNL Schema Editor], schema-metadata och tjänstförbrukning. Mer information finns i [XDM System overview](../home.md).

Det finns flera viktiga fördelar med att skapa och använda scheman i [!DNL Experience Platform]. För det första möjliggör scheman bättre datastyrning och minimering av data, vilket är särskilt viktigt med sekretessbestämmelser. För det andra gör det möjligt att bygga scheman med Adobe standardkomponenter för körklara insikter och använda AI/ML-tjänster med minimala anpassningar. Slutligen tillhandahåller scheman infrastruktur för datautbytesinsikter och effektiv samordning.

## Planera ditt schema

Det första steget i att skapa ett schema är att fastställa konceptet, eller det verkliga objektet, som du försöker fånga inom schemat. När du har identifierat det koncept du försöker beskriva kan du börja planera ditt schema genom att tänka på saker som datatyp, potentiella identitetsfält och hur schemat kan utvecklas i framtiden.

### Databeteenden i [!DNL Experience Platform]

Data som är avsedda att användas i [!DNL Experience Platform] är grupperade i två beteendetyper:

* **Postdata**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsseriedata**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskrivs mer ingående senare i det här dokumentet.

Både post- och tidsseriescheman innehåller en karta över identiteter (`xdm:identityMap`). Det här fältet innehåller identitetsbeteckningen för ett ämne, som har ritats från fält markerade som &quot;Identitet&quot; enligt beskrivningen i nästa avsnitt.

### [!UICONTROL Identity] {#identity}

Scheman används för att importera data till [!DNL Experience Platform]. Dessa data kan användas för flera tjänster för att skapa en enda, enhetlig vy av en enskild enhet. Därför är det viktigt att tänka på scheman när det gäller kundidentiteter och vilka fält som kan användas för att identifiera ett ämne oavsett varifrån data kommer.

Nyckelfält i dina scheman kan markeras som identiteter för att underlätta med den här processen. När data har matats in infogas data i dessa fält i &quot;[!UICONTROL Identity Graph]&quot; för den personen. Diagramdata kan sedan nås av [[!DNL Real-time Customer Profile]](../../profile/home.md) och andra [!DNL Experience Platform]-tjänster för att ge en sammanslagen vy över varje enskild kund.

Fält som vanligen markeras som &quot;[!UICONTROL Identity]&quot; är: e-postadress, telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-ID eller andra unika ID-fält. Du bör också ta hänsyn till unika identifierare som är specifika för din organisation, eftersom de kan vara bra [!UICONTROL Identity]-fält också.

Det är viktigt att tänka på kundens identiteter under schemaplaneringsfasen för att säkerställa att data samlas ihop för att skapa en så robust profil som möjligt. Se översikten på [Adobe Experience Platform Identity Service](../../identity-service/home.md) om du vill veta mer om hur identitetsinformation kan hjälpa dig att leverera digitala upplevelser till dina kunder.

#### `identityMap` {#identityMap}

`identityMap` är ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Det här fältet kan användas för att ange identitetsinformation för dina scheman, i stället för att definiera identitetsvärden inom strukturen för själva schemat.

Den största nackdelen med att använda `identityMap` är att identiteter bäddas in i data och blir mindre synliga som ett resultat av detta. Om du importerar rådata bör du definiera enskilda identitetsfält i den faktiska schemastrukturen i stället.

Identitetskartor kan dock vara särskilt användbara om du samlar in data från källor som lagrar identiteter tillsammans, till exempel [!DNL Airship] eller Adobe Audience Manager. Dessutom krävs identitetskartor om du använder [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

Ett exempel på en enkel identitetskarta skulle se ut så här:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Som exemplet ovan visar representerar varje nyckel i `identityMap`-objektet ett identitetsnamnutrymme. Värdet för varje nyckel är en array med objekt som representerar identitetsvärdena (`id`) för respektive namnutrymme. I [!DNL Identity Service]-dokumentationen finns en [lista över standardnamnutrymmen för identiteter](../../identity-service/troubleshooting-guide.md#standard-namespaces) som känns igen av Adobe-program.

>[!NOTE]
>
>Ett booleskt värde för om värdet är en primär identitet (`primary`) kan också anges för varje identitetsvärde. Primära identiteter behöver bara anges för scheman som är avsedda att användas i [!DNL Real-time Customer Profile]. Mer information finns i avsnittet om [unionsscheman](#union).

### Principer för schemautveckling {#evolution}

I takt med att de digitala upplevelserna utvecklas måste även de scheman som används för att representera dem finnas kvar. Ett väldesignat schema kan därför anpassas och utvecklas efter behov, utan att det medför destruktiva ändringar i tidigare versioner av schemat.

Eftersom bakåtkompatibilitet är avgörande för schemautvecklingen, tillämpar [!DNL Experience Platform] en rent additiv versionsprincip för att säkerställa att eventuella ändringar av schemat endast resulterar i icke-förstörande uppdateringar och ändringar. Det går alltså inte att använda **brytningsändringar.**

>[!NOTE]
>
>Om ett schema ännu inte har använts för att importera data till [!DNL Experience Platform] och inte har aktiverats för användning i kundprofilen i realtid, kan du införa en brytningsändring i det schemat. När schemat har använts i [!DNL Platform] måste det dock följa den additiva versionsprincipen.

I följande tabell visas vilka ändringar som stöds vid redigering av scheman, fältgrupper och datatyper:

| Ändringar som stöds | Brytande ändringar (stöds inte) |
| --- | --- |
| <ul><li>Lägga till nya fält i resursen</li><li>Göra ett obligatoriskt fält valfritt</li><li>Ändra resursens visningsnamn och beskrivning</li></ul> | <ul><li>Tar bort tidigare definierade fält</li><li>Nya obligatoriska fält</li><li>Byta namn på eller definiera om befintliga fält</li><li>Ta bort eller begränsa fältvärden som tidigare stöds</li><li>Flytta attribut till en annan plats i trädet</li></ul> |

### Scheman och datainhämtning

Om du vill importera data till [!DNL Experience Platform] måste du först skapa en datauppsättning. Datauppsättningar är byggstenarna för dataomvandling och spårning för [[!DNL Catalog Service]](../../catalog/home.md), och representerar vanligtvis tabeller eller filer som innehåller inkapslade data. Alla datauppsättningar baseras på befintliga XDM-scheman, som innehåller begränsningar för vad de inmatade data ska innehålla och hur de ska struktureras. Mer information finns i översikten på [Adobe Experience Platform datainmatning](../../ingestion/home.md).

## Bygga block i ett schema

[!DNL Experience Platform] använder en dispositionsmetod där standardbyggstenar kombineras för att skapa scheman. Den här metoden främjar återanvändbarheten av befintliga komponenter och driver standardiseringen i hela branschen för att stödja leverantörsscheman och komponenter i [!DNL Platform].

Scheman består av följande formel:

**Klass + schemafältgrupp&amp;ast; = XDM-schema**

&amp;ast;Ett schema består av en klass och noll eller flera schemafältgrupper. Det innebär att du kan skapa ett datauppsättningsschema utan att använda fältgrupper alls.

### Klass {#class}

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

En schemaklass avgör vilka fältgrupper som kan användas i schemat. Detta beskrivs mer ingående i [nästa avsnitt](#field-group).

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för XDM. Två av dessa klasser, [!DNL XDM Individual Profile] och [!DNL XDM ExperienceEvent], krävs för nästan alla plattformsprocesser längre fram i kedjan. Dessutom kan du skapa egna klasser som beskriver mer specifika användningsfall för organisationen. Anpassade klasser definieras av en organisation när det inte finns några Adobe-definierade huvudklasser tillgängliga som beskriver ett unikt användningsfall.

I följande skärmbild visas hur klasser visas i användargränssnittet för plattformen. Eftersom exempelschemat som visas inte innehåller några fältgrupper, kommer alla fält som visas att anges av schemaklassen ([!UICONTROL XDM Individual Profile]).

![](../images/schema-composition/class.png)

Den senaste listan över tillgängliga standard-XDM-klasser finns i [den officiella XDM-databasen](https://github.com/adobe/xdm/tree/master/components/classes). Du kan också läsa guiden [utforska XDM-komponenter](../ui/explore.md) om du hellre vill se resurser i användargränssnittet.

### Fältgrupp {#field-group}

En fältgrupp är en återanvändbar komponent som definierar ett eller flera fält som implementerar vissa funktioner, som personlig information, hotellinställningar eller adress. Fältgrupper är avsedda att ingå i ett schema som implementerar en kompatibel klass.

Fältgrupper definierar vilka klasser de är kompatibla med baserat på beteendet hos de data de representerar (post- eller tidsserie). Det innebär att inte alla fältgrupper är tillgängliga för användning med alla klasser.

[!DNL Experience Platform] innehåller många standardfältgrupper för Adobe, samtidigt som leverantörer kan definiera fältgrupper för sina användare, och enskilda användare kan definiera fältgrupper för sina egna specifika koncept.

Om du till exempel vill hämta information som [!UICONTROL First Name] och [!UICONTROL Home Address] för ditt [!UICONTROL Loyalty Members]-schema, kan du använda standardfältgrupper som definierar de vanliga begreppen. Begrepp som är specifika för mindre vanliga användningsområden (till exempel &quot;[!UICONTROL Loyalty Program Level]&quot;) har ofta ingen fördefinierad fältgrupp. I det här fallet måste du definiera en egen fältgrupp för att kunna hämta informationen.

Kom ihåg att scheman består av fältgrupper som är &quot;noll eller fler&quot;, vilket innebär att du kan skapa ett giltigt schema utan att använda några fältgrupper alls.

I följande skärmbild visas hur fältgrupper representeras i användargränssnittet för plattformen. En enda fältgrupp ([!UICONTROL Demographic Details]) läggs till i ett schema i det här exemplet, som innehåller en gruppering av fält till schemats struktur.

![](../images/schema-composition/field-group.png)

Den senaste listan över tillgängliga standardfältgrupper i XDM finns i [den officiella XDM-databasen](https://github.com/adobe/xdm/tree/master/components/mixins). Du kan också läsa guiden [utforska XDM-komponenter](../ui/explore.md) om du hellre vill se resurser i användargränssnittet.

### Datatyp {#data-type}

Datatyper används som referensfälttyper i klasser eller scheman på samma sätt som grundläggande litteralfält. Den största skillnaden är att datatyper kan definiera flera underfält. En datatyp liknar en fältgrupp och möjliggör konsekvent användning av en flerfältsstruktur, men har större flexibilitet än en fältgrupp eftersom en datatyp kan inkluderas var som helst i ett schema genom att lägga till den som&quot;datatyp&quot; för ett fält.

[!DNL Experience Platform] innehåller ett antal vanliga datatyper som en del av programmet  [!DNL Schema Registry] som stöder användning av standardmönster för att beskriva vanliga datastrukturer. Detta förklaras mer ingående i [!DNL Schema Registry]-självstudiekurserna, där det blir tydligare när du går igenom stegen för att definiera datatyper.

I följande skärmbild visas hur datatyperna visas i användargränssnittet för plattformen. Ett av fälten som anges av fältgruppen [!UICONTROL Demographic Details] använder datatypen [!UICONTROL Person name], vilket anges av texten efter lodtecknet (`|`) bredvid fältets namn. Den här särskilda datatypen innehåller flera delfält som relaterar till namnet på en enskild person, en konstruktion som kan återanvändas för andra fält där en persons namn måste hämtas.

![](../images/schema-composition/data-type.png)

Den senaste listan över tillgängliga XDM-standarddatatyper finns i [den officiella XDM-databasen](https://github.com/adobe/xdm/tree/master/components/datatypes). Du kan också läsa guiden [utforska XDM-komponenter](../ui/explore.md) om du hellre vill se resurser i användargränssnittet.

### Fält

Ett fält är den mest grundläggande byggstenen i ett schema. Fält innehåller begränsningar för vilken typ av data de kan innehålla genom att definiera en viss datatyp. Dessa grundläggande datatyper definierar ett enskilt fält, medan de [datatyper](#data-type) som tidigare nämnts gör att du kan definiera flera underfält och återanvända samma flerfältsstruktur i olika scheman. Förutom att definiera ett fälts&quot;datatyp&quot; som en av de datatyper som definieras i registret stöder [!DNL Experience Platform] grundläggande skalära typer som:

* Sträng
* Heltal
* Dubbel
* Boolean
* Array
* Objekt

>[!TIP]
>
>I [bilagan](#objects-v-freeform) finns information om för- och nackdelar med att använda frihandsfält över objekttypsfält.

Giltiga intervall för dessa skalära typer kan begränsas ytterligare till vissa mönster, format, minimum/maximum eller fördefinierade värden. Med dessa begränsningar kan en mängd mer specifika fälttyper visas, bland annat:

* Enum
* Lång
* Kort
* Byte
* Datum
* Datum-tid
* Mappa

>[!NOTE]
>
>Fälttypen &quot;map&quot; tillåter nyckelvärdepar, inklusive flera värden för en enskild nyckel. Kartor kan bara definieras på systemnivå, vilket innebär att du kan stöta på en karta i ett bransch- eller leverantörsdefinierat schema, men den är inte tillgänglig för användning i fält som du definierar. Utvecklarhandboken för [API:t för schematabeller](../api/getting-started.md) innehåller mer information om hur du definierar fälttyper.

Vissa dataåtgärder som används av underordnade tjänster och program tillämpar begränsningar för specifika fälttyper. De tjänster som påverkas är bland annat följande:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Innan du skapar ett schema för användning i underordnade tjänster bör du läsa lämplig dokumentation för dessa tjänster för att bättre förstå fältkraven och begränsningarna för de dataåtgärder som schemat är avsett för.

### XDM-fält

Förutom grundläggande fält och möjligheten att definiera egna datatyper tillhandahåller XDM en standarduppsättning med fält och datatyper som är implicit förstådda av [!DNL Experience Platform]-tjänster och ger större enhetlighet när de används i alla [!DNL Platform]-komponenter.

Dessa fält, till exempel&quot;Förnamn&quot; och&quot;E-postadress&quot;, innehåller tillägg utöver de grundläggande skalära fälttyperna och anger [!DNL Platform] att alla fält som delar samma XDM-datatyp fungerar på samma sätt. Detta beteende kan betraktas som tillförlitligt oavsett varifrån data kommer eller i vilken [!DNL Platform]-tjänst data används.

En fullständig lista över tillgängliga XDM-fält finns i [XDM-fältordlistan](field-dictionary.md). Vi rekommenderar att du använder XDM-fält och datatyper där det är möjligt för att stödja konsekvens och standardisering i [!DNL Experience Platform].

## Kompositionsexempel

Scheman representerar format och struktur för data som ska importeras till [!DNL Platform], och som byggs med en kompositionsmodell. Som tidigare nämnts består dessa scheman av en klass och noll eller flera fältgrupper som är kompatibla med den klassen.

Ett schema som beskriver inköp som görs i en butik kan till exempel kallas &quot;[!UICONTROL Store Transactions]&quot;. Schemat implementerar klassen [!DNL XDM ExperienceEvent] kombinerat med standardfältgruppen [!UICONTROL Commerce] och en användardefinierad fältgrupp [!UICONTROL Product Info].

Ett annat schema som spårar webbplatstrafiken kan kallas [!UICONTROL Web Visits]. Den implementerar även klassen [!DNL XDM ExperienceEvent], men den här gången kombineras standardfältgruppen [!UICONTROL Web].

Diagrammet nedan visar dessa scheman och fälten från varje fältgrupp. Den innehåller också två scheman baserade på klassen [!DNL XDM Individual Profile], inklusive schemat [!UICONTROL Loyalty Members] som nämndes tidigare i den här guiden.

![](../images/schema-composition/composition.png)

### Sammanslutning {#union}

Med [!DNL Experience Platform] kan du skapa scheman för särskilda användningsfall, men du kan även se en &quot;union&quot; av scheman för en viss klasstyp. I föregående diagram visas två scheman baserade på klassen XDM ExperienceEvent och två scheman baserade på klassen [!DNL XDM Individual Profile]. Unionen, som visas nedan, samlar fälten för alla scheman som delar samma klass ([!DNL XDM ExperienceEvent] respektive [!DNL XDM Individual Profile]).

![](../images/schema-composition/union.png)

Genom att aktivera ett schema för användning med [!DNL Real-time Customer Profile] inkluderas det i unionen för den klasstypen. [!DNL Profile] ger robusta, centraliserade profiler av kundattribut samt ett tidsstämplat konto för varje händelse som kunden har haft i alla system som är integrerade med  [!DNL Platform]. [!DNL Profile] använder unionsvyn för att representera dessa data och ge en helhetsbild av varje enskild kund.

Mer information om hur du arbetar med [!DNL Profile] finns i [Kundprofilöversikt i realtid](../../profile/home.md).

## Mappa datafiler till XDM-scheman

Alla datafiler som är inkapslade i [!DNL Experience Platform] måste överensstämma med strukturen i ett XDM-schema. Mer information om hur du formaterar datafiler enligt XDM-hierarkier (inklusive exempelfiler) finns i dokumentet om [ETL-omformningar](../../etl/transformations.md). Allmän information om hur du importerar datafiler till [!DNL Experience Platform] finns i [översikten över gruppöverföring](../../ingestion/batch-ingestion/overview.md).

## Scheman för externa segment

Om du överför segment från externa system till plattformen måste du använda följande komponenter för att hämta dem i dina scheman:

* [[!UICONTROL Segment definition] klass](../classes/segment-definition.md): Använd den här standardklassen för att hämta nyckelattribut för en extern segmentdefinition.
* [[!UICONTROL Segment Membership Details] fältgrupp](../field-groups/profile/segmentation.md): Lägg till den här fältgruppen i ditt  [!UICONTROL XDM Individual Profile] schema för att associera kundprofiler med specifika segment.

## Nästa steg

Nu när du förstår grunderna i schemakomposition kan du börja utforska och skapa scheman med [!DNL Schema Registry].

Om du vill granska strukturen för de två grundläggande XDM-klasserna och deras vanliga kompatibla fältgrupper, se följande referensdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] används för att komma åt [!DNL Schema Library] i Adobe Experience Platform och innehåller ett användargränssnitt och RESTful API som alla tillgängliga biblioteksresurser kan nås från. [!DNL Schema Library] innehåller branschresurser som definieras av Adobe, leverantörsresurser som definieras av [!DNL Experience Platform] partners och klasser, fältgrupper, datatyper och scheman som har disponerats av medlemmar i din organisation.

Om du vill börja skapa schemat med hjälp av användargränssnittet följer du med självstudiekursen [Schemaredigeraren](../tutorials/create-schema-ui.md) för att skapa schemat &quot;Loyalty Members&quot; som nämns i hela dokumentet.

Börja med att läsa utvecklarhandboken för [!DNL Schema Registry] API:t för schematabeller](../api/getting-started.md) för att börja använda API:t [. När du har läst utvecklarhandboken följer du de steg som beskrivs i självstudiekursen om att [skapa ett schema med API:t för schemaregister](../tutorials/create-schema-api.md).

## Bilaga

Följande avsnitt innehåller ytterligare information om principerna för schemakomposition.

### Relationstabeller jämfört med inbäddade objekt {#embedded}

När du arbetar med relationsdatabaser omfattar de bästa metoderna att normalisera data, eller att ta en enhet och dela upp den i separata delar som sedan visas i flera tabeller. För att kunna läsa data som helhet eller uppdatera enheten måste läs- och skrivåtgärder utföras i många enskilda tabeller med JOIN.

Genom att använda inbäddade objekt kan XDM-scheman representera komplexa data direkt och lagra dem i självständiga dokument med en hierarkisk struktur. En av de största fördelarna med den här strukturen är att den gör det möjligt att fråga efter data utan att behöva rekonstruera enheten med dyrbara kopplingar till flera deformerade tabeller. Det finns inga hårda begränsningar för hur många nivåer din schemahierarki kan vara.

### Scheman och big data {#big-data}

Moderna digitala system genererar enorma mängder beteendesignaler (transaktionsdata, webbloggar, internet med mera). Dessa stora data ger fantastiska möjligheter att optimera upplevelser, men är svåra att använda på grund av datans storlek och variation. För att få ut mer av uppgifterna måste datastrukturen, formatet och definitionerna standardiseras så att de kan behandlas enhetligt och effektivt.

Scheman löser detta problem genom att data kan integreras från flera källor, standardiseras med gemensamma strukturer och definitioner och delas mellan olika lösningar. Detta gör att efterföljande processer och tjänster kan besvara alla typer av frågor som ställs om data, vilket innebär att man kan gå ifrån den traditionella metoden med datamodellering där alla frågor som ställs om data är kända i förväg och data är modellerade för att uppfylla dessa förväntningar.

### Objekt jämfört med frihandsfält {#objects-v-freeform}

Det finns några viktiga faktorer att tänka på när du väljer objekt framför frihandsfält när du utformar scheman:

| Objekt | Frihandsfält |
| --- | --- |
| Ökar kapsling | Mindre eller ingen kapsling |
| Skapar logiska fältgrupperingar | Fält placeras på ad hoc-platser |

{style=&quot;table-layout:auto&quot;}

#### Objekt

Fördelarna och nackdelarna med att använda objekt över frihandsfält visas nedan.

**Yrkesverksamma**:

* Objekt används bäst när du vill skapa en logisk gruppering av vissa fält.
* Objekten organiserar schemat på ett mer strukturerat sätt.
* Objekt kan indirekt bidra till att skapa en bra menystruktur i segmentbyggargränssnittet. De grupperade fälten i schemat återspeglas direkt i mappstrukturen som finns i gränssnittet i Segment Builder.

**Kon**:

* Fält blir mer kapslade.
* När du använder [Adobe Experience Platform Query Service](../../query-service/home.md) måste längre referenssträngar anges för frågefält som är kapslade i objekt.

#### Frihandsfält

Fördelarna och nackdelarna med att använda frihandsfält över objekt visas nedan.

**Yrkesverksamma**:

* Frihandsfält skapas direkt under schemats rotobjekt (`_tenantId`), vilket ökar synligheten.
* Referenssträngar för frihandsfält brukar vara kortare när frågetjänsten används.

**Kon**:

* Platsen för friformsfält i schemat är ad för sig, vilket innebär att de visas i alfabetisk ordning i schemaredigeraren. Detta kan göra att scheman blir mindre strukturerade och liknande friformsfält kan hamna långt åtskilda beroende på deras namn.
