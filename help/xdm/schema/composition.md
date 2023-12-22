---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;enum;mixin;fältgrupp;fältgrupper;mixins;datatyp;datatyp;datatyp;datatyp;primär identitet;primär identitet;XDM-individuell profil;XDM-fält;enum datatyp;Experience event;XDM ExperienceEvent;experienceEvent;XDM ExperienceEvent;schema;design;klass;klass;klasser;klasser;datatyp;datatyp;datatyp;datatyp;datatyp;scheman;scheman;identityMap;identity map;identity map;schema design;map;union schema;union
solution: Experience Platform
title: Grundläggande om schemakomposition
description: Lär dig mer om XDM-scheman (Experience Data Model) och byggstenarna, principerna och de bästa sätten att komponera scheman i Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '4187'
ht-degree: 0%

---

# Grunderna för schemakomposition

Lär dig mer om XDM-scheman (Experience Data Model) och byggstenarna, principerna och de bästa sätten att komponera scheman i Adobe Experience Platform. Allmän information om XDM och hur det används i [!DNL Platform], se [XDM - systemöversikt](../home.md).

## Scheman {#understanding-schemas}

Ett schema är en uppsättning regler som representerar och validerar datastrukturen och dataformatet. På en hög nivå ger scheman en abstrakt definition av ett objekt i verkligheten (till exempel en person) och ger en översikt över vilka data som ska inkluderas i varje instans av objektet (till exempel förnamn, efternamn, födelsedag o.s.v.).

Förutom att beskriva datastrukturen, tillämpar scheman begränsningar och förväntningar på data så att de kan valideras när de flyttas mellan olika system. Med dessa standarddefinitioner kan data tolkas på ett enhetligt sätt, oavsett ursprung, och behovet av översättning mellan olika program försvinner.

Experience Platform underhåller denna semantiska normalisering med hjälp av scheman. Scheman är standardmetoden för att beskriva data i Experience Platform, vilket gör att alla data som överensstämmer med scheman kan återanvändas i en organisation utan konflikter, eller till och med delas mellan flera organisationer.

XDM-scheman är idealiska för att lagra enorma mängder komplexa data i ett självständigt format. Se avsnitten om [inbäddade objekt](#embedded) och [big data](#big-data) i bilagan till det här dokumentet om du vill ha mer information om hur XDM gör detta.

### Schemabaserade arbetsflöden i Experience Platform {#schema-based-workflows}

Standardisering är ett nyckelbegrepp bakom Experience Platform. XDM, som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera standardscheman för kundupplevelsehantering.

Den infrastruktur som Experience Platform bygger på, känd som [!DNL XDM System], underlättar schemabaserade arbetsflöden och innehåller [!DNL Schema Registry], [!DNL Schema Editor], schemadata och tjänstekonsumtionsmönster. Se [XDM - systemöversikt](../home.md) för mer information.

Det finns flera fördelar med att använda scheman i Experience Platform. För det första möjliggör scheman bättre datastyrning och minimering av data, vilket är särskilt viktigt med sekretessbestämmelser. För det andra gör det möjligt att bygga scheman med Adobe standardkomponenter för körklara insikter och använda AI/ML-tjänster med minimala anpassningar. Slutligen tillhandahåller scheman infrastruktur för datautbytesinsikter och effektiv samordning.

## Planera ditt schema {#planning}

Det första steget i att skapa ett schema är att fastställa konceptet, eller det verkliga objektet, som du försöker fånga inom schemat. När du har identifierat konceptet som du försöker beskriva börjar du planera ditt schema genom att tänka på saker som datatypen, potentiella identitetsfält och hur schemat kan utvecklas i framtiden.

### Databeteenden i Experience Platform {#data-behaviors}

Data som är avsedda att användas i Experience Platform är grupperade i två beteendetyper:

* **Registrera data**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsseriedata**: Ger en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett postämne.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskrivs mer ingående senare i det här dokumentet.

Scheman för både post- och tidsserier innehåller en karta över identiteter (`xdm:identityMap`). Det här fältet innehåller identitetsbeteckningen för ett ämne, som har ritats från fält som markerats som &quot;Identitet&quot; enligt beskrivningen i nästa avsnitt.

### [!UICONTROL Identity] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identiteter i scheman"
>abstract="Identiteter är nyckelfält i ett schema som kan användas för att identifiera ett ämne, till exempel en e-postadress eller ett marknadsförings-ID. Dessa fält används för att skapa identitetsdiagrammet för varje enskild person och för att skapa kundprofiler. Mer information om identiteter i scheman finns i dokumentationen."

Scheman används för inmatning av data i Experience Platform. Dessa data kan användas för flera tjänster för att skapa en enda, enhetlig vy av en enskild enhet. Därför är det viktigt att tänka på vilka fält som kan användas för att identifiera ett ämne när du utformar scheman för kundidentiteter, oavsett varifrån uppgifterna kommer.

Nyckelfält i dina scheman kan markeras som identiteter för att underlätta med den här processen. När data har matats in infogas uppgifterna i dessa fält i[!UICONTROL Identity Graph]&quot; för den där individen. Diagramdata kan sedan nås av [[!DNL Real-Time Customer Profile]](../../profile/home.md) och andra Experience Platform-tjänster för att ge en enhetlig bild av varje enskild kund.

Fält som vanligen markeras som &quot;[!UICONTROL Identity]&quot; inkludera: e-postadress, telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-ID eller andra unika ID-fält. Överväg alla unika identifierare som är specifika för din organisation, eftersom de kan vara bra[!UICONTROL Identity]även fält.

Det är viktigt att tänka på kundens identiteter under schemaplaneringsfasen för att säkerställa att data samlas ihop för att skapa den mest robusta profilen som är möjlig. Mer information om hur identitetsinformation kan hjälpa er att leverera digitala upplevelser till era kunder finns i [Översikt över identitetstjänsten](../../identity-service/home.md). Läs dokumentet om god praxis för datamodellering för [tips om hur du använder identiteter när du skapar ett schema](./best-practices.md#data-validation-fields).

Det finns två sätt att skicka identitetsdata till plattformen:

1. Lägga till identitetsbeskrivningar till enskilda fält, antingen via [Gränssnittet för schemaredigeraren](../ui/fields/identity.md) eller med [API för schemaregister](../api/descriptors.md#create)
1. Använda [`identityMap` fält](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` är ett mappningsfält som beskriver de olika identitetsvärdena för en individ, tillsammans med deras associerade namnutrymmen. Det här fältet kan användas för att ange identitetsinformation för dina scheman, i stället för att definiera identitetsvärden inom strukturen för själva schemat.

Den största nackdelen med att använda `identityMap` är att identiteter blir inbäddade i data och därmed blir mindre synliga. Om du importerar rådata bör du definiera enskilda identitetsfält i den faktiska schemastrukturen i stället.

>[!NOTE]
>
>Ett schema som använder `identityMap` kan användas som ett källschema i en relation, men kan inte användas som ett referensschema. Detta beror på att alla referensscheman måste ha en synlig identitet som kan mappas i ett referensfält i källschemat. Se användargränssnittets guide på [relationer](../tutorials/relationship-ui.md) Mer information om kraven för käll- och referensscheman.

Identitetskartor kan dock vara användbara om det finns ett varierande antal identiteter för ett schema, eller om du samlar in data från källor som lagrar identiteter tillsammans (till exempel [!DNL Airship] eller Adobe Audience Manager). Dessutom krävs identitetskartor om du använder [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/).

Ett exempel på en enkel identitetskarta skulle se ut så här:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Som visas i exemplet ovan finns varje tangent i `identityMap` -objektet representerar ett identitetsnamnutrymme. Värdet för varje nyckel är en array med objekt som representerar identitetsvärdena (`id`) för respektive namnutrymme. Se [!DNL Identity Service] dokumentation för [lista med vanliga ID-namnutrymmen](../../identity-service/troubleshooting-guide.md#standard-namespaces) känns igen av Adobe.

>[!NOTE]
>
>Ett booleskt värde för om värdet är en primär identitet (`primary`) kan också anges för varje identitetsvärde. Du behöver bara ange primära identiteter för scheman som ska användas i [!DNL Real-Time Customer Profile]. Se avsnittet om [unionsscheman](#union) för mer information.

### Principer för schemautveckling {#evolution}

I takt med att de digitala upplevelserna utvecklas måste även de scheman som används för att representera dem finnas kvar. Ett väldesignat schema kan därför anpassas och utvecklas efter behov, utan att det medför destruktiva ändringar i tidigare versioner av schemat.

Eftersom det är viktigt att bibehålla bakåtkompatibiliteten för att kunna utveckla scheman tillämpar Experience Platform en rent additiv versionsprincip. Denna princip säkerställer att alla ändringar av schemat endast resulterar i icke-förstörande uppdateringar och ändringar. Med andra ord: **brytningsändringar stöds inte.**

>[!NOTE]
>
>Du kan bara göra en brytningsändring i ett schema om det ännu inte har använts för att importera data till Experience Platform och inte har aktiverats för användning i kundprofilen i realtid. När schemat har använts i [!DNL Platform]måste den följa den additiva versionsprincipen.

I följande tabell visas vilka ändringar som stöds vid redigering av scheman, fältgrupper och datatyper:

| Ändringar som stöds | Brytande ändringar (stöds inte) |
| --- | --- |
| <ul><li>Lägga till nya fält i resursen</li><li>Göra ett obligatoriskt fält valfritt</li><li>Nya obligatoriska fält*</li><li>Ändra resursens visningsnamn och beskrivning</li><li>Aktiverar schemats deltagande i profilen</li></ul> | <ul><li>Tar bort tidigare definierade fält</li><li>Byta namn på eller definiera om befintliga fält</li><li>Ta bort eller begränsa fältvärden som tidigare stöds</li><li>Flytta befintliga fält till en annan plats i trädet</li><li>Tar bort schemat</li><li>Inaktivera schemat från att delta i profilen</li></ul> |

\**Se avsnittet nedan för viktig information [ställa in nya obligatoriska fält](#post-ingestion-required-fields).*

### Obligatoriska fält

Enskilda schemafält kan vara [markerat som obligatoriskt](../ui/fields/required.md), vilket innebär att alla kapslade poster måste innehålla data i dessa fält för att validera. Om du till exempel anger ett schemats primära identitetsfält som obligatoriskt kan du se till att alla inkapslade poster deltar i kundprofilen i realtid. Om du anger ett tidsstämpelfält som obligatoriskt ser du dessutom till att alla händelser i tidsserien bevaras kronologiskt.

>[!IMPORTANT]
>
>Oavsett om ett schemafält krävs eller inte accepterar inte plattformen `null` eller tomma värden för inkapslade fält. Om det inte finns något värde för ett visst fält i en post eller händelse, ska nyckeln för det fältet uteslutas från inmatningsnyttolasten.

#### Ange fält som obligatoriska efter intag {#post-ingestion-required-fields}

Om ett fält har använts för att importera data och inte ursprungligen ställdes in som nödvändigt, kan det fältet ha ett null-värde för vissa poster. Om du anger det här fältet som obligatoriskt för postinmatning måste alla framtida poster innehålla ett värde för det här fältet, även om historiska poster kan vara null.

Tänk på följande när du ställer in ett tidigare valfritt fält efter behov:

1. Om du frågar efter historiska data och skriver resultaten i en ny datamängd, kommer vissa rader att misslyckas eftersom de innehåller null-värden för det obligatoriska fältet.
1. Om fältet deltar i [Kundprofil i realtid](../../profile/home.md) och du exporterar data innan du ställer in dem efter behov, kan det vara null för vissa profiler.
1. Du kan använda API:t för schemaregister för att visa en tidsstämplad ändringslogg för alla XDM-resurser i plattformen, inklusive nya obligatoriska fält. Se guiden på [slutpunkt för granskningslogg](../api/audit-log.md) för mer information.

### Scheman och datainmatning

För att kunna importera data till Experience Platform måste en datauppsättning först skapas. Datauppsättningar är byggstenarna för dataomvandling och -spårning för [[!DNL Catalog Service]](../../catalog/home.md)och representerar vanligtvis tabeller eller filer som innehåller inkapslade data. Alla datauppsättningar baseras på befintliga XDM-scheman, som innehåller begränsningar för vad de inmatade data ska innehålla och hur de ska struktureras. Se översikten på [Adobe Experience Platform datainmatning](../../ingestion/home.md) för mer information.

## Bygga block i ett schema {#schema-building-blocks}

Experience Platform använder en dispositionsmetod där standardbyggstenar kombineras för att skapa scheman. Den här metoden främjar återanvändbarheten av befintliga komponenter och driver standardisering i hela branschen för att stödja leverantörsscheman och komponenter i [!DNL Platform].

Scheman består av följande formel:

**Klass + schemafältgrupp; = XDM-schema**

&amp;ast;Ett schema består av en klass och noll eller flera schemafältgrupper. Det innebär att du kan skapa ett datauppsättningsschema utan att använda fältgrupper alls.

### Klass {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Klass"
>abstract="Alla scheman baseras på en enda klass. Klassen definierar schemats beteende och de gemensamma egenskaper som alla scheman baserade på den klassen måste innehålla. Läs dokumentationen om du vill veta mer om hur klasser är inblandade i schemakomposition."

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat kommer att innehålla (post- eller tidsserie). Förutom detta beskriver klasser det minsta antalet gemensamma egenskaper som alla scheman baserade på den klassen behöver innehålla och tillhandahåller ett sätt för att sammanfoga flera kompatibla datamängder.

En schemaklass avgör vilka fältgrupper som är berättigade att användas i schemat. Detta diskuteras mer ingående i [nästa avsnitt](#field-group).

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för XDM. Två av dessa klasser, [!DNL XDM Individual Profile] och [!DNL XDM ExperienceEvent]krävs för nästan alla plattformsprocesser längre fram i kedjan. Dessutom kan du skapa egna klasser som beskriver mer specifika användningsfall för organisationen. Anpassade klasser definieras av en organisation när det inte finns några Adobe-definierade huvudklasser tillgängliga som beskriver ett unikt användningsfall.

I följande skärmbild visas hur klasser visas i användargränssnittet för plattformen. Eftersom exempelschemat som visas inte innehåller några fältgrupper, kommer alla fält som visas att tillhandahållas av schemaklassen ([!UICONTROL XDM Individual Profile]).

![The [!UICONTROL XDM Individual Profile] i Schemaredigeraren.](../images/schema-composition/class.png)

Den senaste listan över tillgängliga standard-XDM-klasser finns i [officiell XDM-databas](https://github.com/adobe/xdm/tree/master/components/classes). Du kan även läsa guiden på [utforska XDM-komponenter](../ui/explore.md) om du föredrar att visa resurser i användargränssnittet.

### Fältgrupp {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Fältgrupp"
>abstract="Fältgrupper är återanvändbara komponenter som gör att du kan utöka scheman med ytterligare attribut. De flesta fältgrupper är bara kompatibla med vissa klasser. Du kan använda standardfältgrupper som definieras av Adobe eller definiera egna fältgrupper manuellt. Läs dokumentationen om du vill veta mer om hur fältgrupper är inblandade i schemakomposition."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Obligatorisk fältgrupp"
>abstract="Den här fältgruppen krävs av källan som du använder. Du kan därför inte ta bort den från ditt schema."

En fältgrupp är en återanvändbar komponent som definierar ett eller flera fält som implementerar vissa funktioner, som personlig information, hotellinställningar eller adress. Fältgrupper är avsedda att ingå i ett schema som implementerar en kompatibel klass.

Fältgrupper definierar vilken eller vilka klasser de är kompatibla med, baserat på beteendet för de data de representerar (post- eller tidsserie). Det innebär att inte alla fältgrupper är tillgängliga för användning med alla klasser.

Experience Platform innehåller många standardfältgrupper i Adobe samtidigt som leverantörer kan definiera fältgrupper för sina användare, och enskilda användare kan definiera fältgrupper för sina egna specifika koncept.

Om du till exempel vill hämta information som &quot;[!UICONTROL First Name]och &quot;[!UICONTROL Home Address]&quot; för dina &quot;[!UICONTROL Loyalty Members]&quot;schema, du skulle kunna använda standardfältgrupper som definierar dessa vanliga begrepp. Begrepp som är mer specifika för din organisation (t.ex. kundens kundlojalitetsprogram eller produktattribut) som kanske inte omfattas av standardfältgrupper. I det här fallet måste du definiera en egen fältgrupp för att kunna hämta informationen.

>[!NOTE]
>
>Du rekommenderas att använda standardfältgrupper när det är möjligt i dina scheman, eftersom dessa fält tolkas implicit av Experience Platform-tjänster och ger större enhetlighet när de används i alla [!DNL Platform] -komponenter.
>
>Fält som tillhandahålls av standardkomponenter (till exempel&quot;Förnamn&quot; och&quot;E-postadress&quot;) innehåller tillagda konnoteringar utöver de grundläggande skalära fälttyperna. De säger [!DNL Platform] att fält som delar samma datatyp fungerar på samma sätt. Detta beteende kan betraktas som tillförlitligt oavsett varifrån data kommer eller i vilket [!DNL Platform] den tjänst som data används i.

Kom ihåg att scheman består av fältgrupper som är &quot;noll eller fler&quot;, vilket innebär att du kan skapa ett giltigt schema utan att använda några fältgrupper alls.

I följande skärmbild visas hur fältgrupper representeras i användargränssnittet för plattformen. En enda fältgrupp ([!UICONTROL Demographic Details]) läggs till i ett schema i det här exemplet, som innehåller en gruppering av fält till schemats struktur.

![Schemaredigeraren med [!UICONTROL Demographic Details] fältgrupp markerad i ett exempelschema.](../images/schema-composition/field-group.png)

Den senaste listan över tillgängliga standardfältgrupper i XDM finns i [officiell XDM-databas](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Du kan även läsa guiden på [utforska XDM-komponenter](../ui/explore.md) om du föredrar att visa resurser i användargränssnittet.

### Datatyp {#data-type}

Datatyper används som referensfälttyper i klasser eller scheman på samma sätt som grundläggande litteralfält. Den största skillnaden är att datatyper kan definiera flera delfält på samma sätt som fältgrupper. Den största skillnaden mellan dem är att datatyper kan inkluderas var som helst i ett schema genom att lägga till den som&quot;datatyp&quot; för ett fält. Fältgrupper är bara kompatibla med vissa klasser, men datatyper kan inkluderas i alla överordnade klasser eller fältgrupper.

>[!NOTE]
>
>Om ett fält definieras som en viss datatyp kan du inte skapa samma fält med en annan datatyp i ett annat schema. Begränsningen gäller för hela organisationens klientorganisation.

Experience Platform tillhandahåller ett antal vanliga datatyper som en del av [!DNL Schema Registry] som stöder användning av standardmönster för att beskriva vanliga datastrukturer. Detta förklaras mer ingående i [Självstudiekurser för schemaregister](../tutorials/create-schema-api.md) och blir tydligare när du går igenom stegen för att definiera datatyper.

I följande skärmbild visas hur datatyperna visas i användargränssnittet för plattformen. Ett av fälten i [!UICONTROL Demographic Details] fältgruppen använder &quot;[!UICONTROL Object]&quot;, datatyp, enligt texten efter lodstreck (`|`) bredvid fältets namn. Den här särskilda datatypen innehåller flera delfält som relaterar till namnet på en enskild person, en konstruktion som kan återanvändas för andra fält där en persons namn måste hämtas.

![Ett diagram i Schemaredigeraren för en enskild person med objektet Fullständigt namn och attributen markerade.](../images/schema-composition/data-type.png)

Den senaste listan över tillgängliga XDM-standarddatatyper finns i [officiell XDM-databas](https://github.com/adobe/xdm/tree/master/components/datatypes). Du kan även läsa guiden på [utforska XDM-komponenter](../ui/explore.md) om du föredrar att visa resurser i användargränssnittet.

### Fält {#field}

Ett fält är den mest grundläggande byggstenen i ett schema. Fält innehåller begränsningar för vilken typ av data de kan innehålla genom att definiera en viss datatyp. Dessa grundläggande datatyper definierar ett enda fält, medan [datatyper](#data-type) kan du definiera flera delfält och återanvända samma struktur med flera fält i olika scheman. Förutom att definiera ett fälts&quot;datatyp&quot; som en av de datatyper som definieras i registret, stöder Experience Platform grundläggande skalära typer som:

* Sträng
* Heltal
* Dubbel
* Boolean
* Array
* Objekt

>[!TIP]
>
>Se [appendix](#objects-v-freeform) om du vill ha information om fördelar och nackdelar med att använda frihandsfält över objekttypsfält.

Giltiga intervall för dessa skalära typer kan begränsas ytterligare till vissa mönster, format, minimum/maximum eller fördefinierade värden. Med dessa begränsningar kan en mängd mer specifika fälttyper visas, bland annat:

* Enum
* Lång
* Kort
* Byte
* Datum
* Datum-tid
* Karta

>[!NOTE]
>
>Fälttypen &quot;map&quot; tillåter nyckelvärdepar, inklusive flera värden för en enskild nyckel. Kartor finns i standard-XDM-klasser och fältgrupper, men du kan också definiera anpassade kartor med API:t för schemaregister. Se självstudiekursen om [definiera egna fält](../tutorials/custom-fields-api.md#custom-maps) för mer information.

## Kompositionsexempel {#composition-example}

Scheman byggs med hjälp av en kompositionsmodell och representerar formatet och strukturen för de data som ska infogas i [!DNL Platform]. Som tidigare nämnts består dessa scheman av en klass och noll eller flera fältgrupper som är kompatibla med den klassen.

Ett schema som beskriver inköp som görs i en butik kan till exempel kallas[!UICONTROL Store Transactions]&quot;. Schemat implementerar [!DNL XDM ExperienceEvent] klass kombinerad med standard [!UICONTROL Commerce] fältgrupp och en användardefinierad [!UICONTROL Product Info] fältgrupp.

Ett annat schema som spårar webbplatstrafiken kan kallas[!UICONTROL Web Visits]&quot;. Den implementerar även [!DNL XDM ExperienceEvent] -klassen, men den här tiden kombinerar standarden [!UICONTROL Web] fältgrupp.

Diagrammet nedan visar dessa scheman och fälten från varje fältgrupp. Den innehåller även två scheman baserade på [!DNL XDM Individual Profile] -klass, inklusive[!UICONTROL Loyalty Members]schemat som nämndes tidigare i den här guiden.

![Ett flödesdiagram över fyra scheman och de fältgrupper som bidrar till dem.](../images/schema-composition/composition.png)

### Sammanslutning {#union}

Med Experience Platform kan du skapa scheman för olika användningsområden, men du kan även se en &quot;union&quot; av scheman för en viss klasstyp. I föregående diagram visas två scheman baserade på klassen XDM ExperienceEvent och två scheman baserade på [!DNL XDM Individual Profile] klassen. Unionen, som visas nedan, samlar fälten för alla scheman som delar samma klass ([!DNL XDM ExperienceEvent] och [!DNL XDM Individual Profile]).

![Ett unionsschemaflödesdiagram som visar fälten som de består av.](../images/schema-composition/union.png)

Genom att aktivera ett schema för användning med [!DNL Real-Time Customer Profile], ingår det i unionen för den typen av klass. [!DNL Profile] ger robusta, centraliserade profiler av kundattribut och en tidsstämplad översikt över alla händelser som kunden har haft i alla system som är integrerade med [!DNL Platform]. [!DNL Profile] använder unionsvyn för att representera dessa data och ge en helhetsbild av varje enskild kund.

Mer information om hur du arbetar med [!DNL Profile], se [Översikt över kundprofiler i realtid](../../profile/home.md).

## Mappa datafiler till XDM-scheman {#mapping-datafiles}

Alla datafiler som importeras till Experience Platform måste överensstämma med strukturen i ett XDM-schema. Mer information om hur du formaterar datafiler enligt XDM-hierarkier (inklusive exempelfiler) finns i dokumentet om [exempel på ETL-omformningar](../../etl/transformations.md). Allmän information om hur du importerar datafiler till Experience Platform finns i [batchvis hantering - översikt](../../ingestion/batch-ingestion/overview.md).

## Scheman för externa målgrupper

Om du samlar målgrupper från externa system i Platform måste du använda följande komponenter för att fånga dem i dina scheman:

* [[!UICONTROL Segment definition] class](../classes/segment-definition.md): Använd den här standardklassen för att hämta nyckelattribut för en extern segmentdefinition.
* [[!UICONTROL Segment Membership Details] fältgrupp](../field-groups/profile/segmentation.md): Lägg till den här fältgruppen i din [!UICONTROL XDM Individual Profile] schema för att associera kundprofiler med specifika målgrupper.

## Nästa steg

Nu när du förstår grunderna i schemakomposition kan du börja utforska och skapa scheman med [!DNL Schema Registry].

Om du vill granska strukturen för de två grundläggande XDM-klasserna och deras vanliga kompatibla fältgrupper, se följande referensdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

The [!DNL Schema Registry] används för att komma åt [!DNL Schema Library] i Adobe Experience Platform och tillhandahåller ett användargränssnitt och RESTful API från vilket alla tillgängliga biblioteksresurser är tillgängliga. The [!DNL Schema Library] innehåller branschresurser som definieras av Adobe, leverantörsresurser som definieras av Experience Platform partners, och klasser, fältgrupper, datatyper och scheman som har disponerats av medlemmar i din organisation.

För att börja komponera schemat med användargränssnittet följer du med [Schemaredigeraren, genomgång](../tutorials/create-schema-ui.md) att skapa schemat &quot;Lojalitetsmedlemmar&quot; som omnämns i hela det här dokumentet.

Börja använda [!DNL Schema Registry] API, börja med att läsa [Utvecklarhandbok för API för schematabell](../api/getting-started.md). När du har läst utvecklarhandboken följer du de steg som beskrivs i självstudiekursen om [skapa ett schema med API:t för schemaregister](../tutorials/create-schema-api.md).

## Bilaga

Följande avsnitt innehåller ytterligare information om principerna för schemakomposition.

### Relationstabeller jämfört med inbäddade objekt {#embedded}

När du arbetar med relationsdatabaser omfattar de effektivaste strategierna att normalisera data eller att ta en enhet och dela upp den i separata delar som sedan visas i flera tabeller. Om du vill läsa data som helhet eller uppdatera entiteten måste läs- och skrivåtgärder utföras för många enskilda tabeller med JOIN.

Genom att använda inbäddade objekt kan XDM-scheman representera komplexa data direkt och lagra dem i självständiga dokument med en hierarkisk struktur. En av de största fördelarna med den här strukturen är att den gör det möjligt att fråga efter data utan att behöva rekonstruera enheten med dyrbara kopplingar till flera deformerade tabeller. Det finns inga hårda begränsningar för hur många nivåer din schemahierarki kan vara.

### Scheman och big data {#big-data}

Moderna digitala system genererar enorma mängder beteendesignaler (transaktionsdata, webbloggar, internet med mera). Dessa stora data ger fantastiska möjligheter att optimera upplevelser, men är svåra att använda på grund av datans storlek och variation. För att få ut mer av informationen måste dess struktur, format och definitioner standardiseras så att de kan behandlas på ett konsekvent och effektivt sätt.

Scheman löser detta problem genom att data kan integreras från flera källor, standardiseras med gemensamma strukturer och definitioner och delas mellan olika lösningar. Detta gör att efterföljande processer och tjänster kan besvara alla typer av frågor som ställs om data. Det går längre än till traditionell datamodellering där alla frågor som ska ställas om data är kända i förväg och data är modellerade för att uppfylla dessa förväntningar.

### Objekt jämfört med frihandsfält {#objects-v-freeform}

Det finns några viktiga faktorer att tänka på när du väljer objekt framför frihandsfält när du utformar scheman:

| Objekt | Frihandsfält |
| --- | --- |
| Ökar kapsling | Mindre eller ingen kapsling |
| Skapar logiska fältgrupperingar | Fält placeras på ad hoc-platser |

{style="table-layout:auto"}

#### Objekt

Fördelarna och nackdelarna med att använda objekt över frihandsfält visas nedan.

**Proffs**:

* Objekt används bäst när du vill skapa en logisk gruppering av vissa fält.
* Objekten organiserar schemat på ett mer strukturerat sätt.
* Objekt kan indirekt bidra till att skapa en bra menystruktur i segmentbyggargränssnittet. De grupperade fälten i schemat återspeglas direkt i mappstrukturen som finns i gränssnittet i Segment Builder.

**Kon**:

* Fält blir mer kapslade.
* När du använder [Adobe Experience Platform Query Service](../../query-service/home.md)måste längre referenssträngar anges för frågefält som är kapslade i objekt.

#### Frihandsfält

Fördelarna och nackdelarna med att använda frihandsfält över objekt visas nedan.

**Proffs**:

* Frihandsfält skapas direkt under schemats rotobjekt (`_tenantId`), vilket ökar synligheten.
* Referenssträngar för frihandsfält brukar vara kortare när frågetjänsten används.

**Kon**:

* Platsen för friformsfält i schemat är ad för sig, vilket innebär att de visas i alfabetisk ordning i schemaredigeraren. Detta kan göra att scheman blir mindre strukturerade och liknande friformsfält kan hamna långt åtskilda beroende på deras namn.
