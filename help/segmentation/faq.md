---
title: Frågor och svar
description: Få svar på vanliga frågor om målgrupper och andra segmenteringsrelaterade koncept.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 81e1ce90b1778bb29c770e1468461949a1ea468c
workflow-type: tm+mt
source-wordcount: '3176'
ht-degree: 0%

---

# Frågor och svar

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa målgrupper genom segmentdefinitioner eller andra källor från ditt [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på Platform och är tillgängliga för alla Adobe-lösningar. Nedan följer en lista med vanliga frågor om målgrupper och segmentering.

## Målgruppsportal

I följande avsnitt listas frågor som rör Audience Portal.

### Har jag tillgång till Audience Portal och Audience Composition?

Audience Portal och Audience Composition är tillgängliga för alla Real-Time CDP Prime- och Ultimate-kunder (B2C, B2B och B2P Editions) och Journey Optimizer Select-, Prime-, Ultimate Starter- och Ultimate-kunder.

I nuläget stöds endast profilbaserade målgrupper. Stöd för kontobaserade målgrupper kommer att läggas till i en senare version.

### Stöds externt genererade förbyggda målgrupper med Audience Portal?

Ja, externt genererade färdiga målgrupper stöds med Audience Portal. Nu kan du importera en externt genererad publik via en CSV-fil. I framtiden kommer ni att kunna lägga till målgrupper via batchanslutningar eller direktuppspelningsbaserade källkopplingar.

### Vilka behörigheter behöver jag för att kunna överföra externt genererade målgrupper?

För att kunna överföra externt genererade målgrupper måste du ha behörigheterna Visa målgrupper/segment, Hantera målgrupper/segment, Visa datauppsättningar, Hantera datauppsättningar, Visa källor och Hantera källor. Det finns inga specifika rollbaserade kontroller som krävs för att överföra externt genererade målgrupper.

### Vad händer när jag överför en externt genererad publik?

När du överför en externt genererad publik skapas följande objekt:

- Datauppsättning
   - Datauppsättningen visas i datamängdslagret, och datauppsättningens namn är **samma** som namnet på den externt genererade målgrupp du överförde.
- Batchjobb
   - Ett batchjobb **automatiskt** körs när du överför en externt genererad publik. Det innebär att du gör det **not** måste vänta på att det dagliga segmenteringsjobbet ska köras för att den externt genererade publiken ska aktiveras.
- Ad hoc-schema
   - A **new** XDM-schemat skapas för användning med den externt genererade målgruppen. Fälten i det här XDM-schemat namnges för användning med den datauppsättning som också skapades.

### Vad består en externt genererad publik av och vad händer med dessa data när de importeras till Platform?

Under importen av det externa målgruppsarbetsflödet måste du ange vilken kolumn i CSV-filen som motsvarar **Primär identitet**. Ett exempel på en primär identitet är e-postadress, ECID eller ett organisationsspecifikt namnområde för en anpassad identitet.

Data som är associerade med den här primära identitetskolumnen på **endast** data som är kopplade till profilen. Om det inte finns några befintliga profiler som matchar data i den primära identitetskolumnen skapas en ny profil. Den här profilen är dock i princip en överbliven profil eftersom **no** attribut eller upplevelsehändelser är associerade med den här profilen.

Alla andra data inom den externt genererade målgruppen beaktas **nyttolastattribut**. Dessa attribut kan **endast** användas för personalisering och berikning under aktiveringen, och **not** kopplad till en profil. Dessa attribut lagras dock i datasjön.

Även om den externt genererade målgruppen kan refereras när målgrupper skapas med segmentbyggaren, kan enskilda profilattribut **inte** användas.

### Kan jag stämma av externt genererade målgruppsdata med en befintlig profil i Platform?

Ja, den externt genererade målgruppen sammanfogas med den befintliga profilen i plattformen om de primära identifierarna matchar. Det kan ta upp till 24 timmar att stämma av dessa data. Om det inte redan finns profildata skapas en ny profil när data hämtas.

### Kan jag använda en externt genererad publik för att bygga andra målgrupper?

Ja, alla externt genererade målgrupper visas i målgruppslagret och kan användas när målgrupper byggs inom [Segment Builder](./ui/segment-builder.md).

### Kan jag använda externt överförda attribut som en del av segmenteringen?

Nej, det kan du inte. Profilattribut är avsedda att vara långvariga attribut, medan externt genererade målgruppsdata som överförs bara innehåller kontextuella data som är kopplade till den externt genererade målgruppen.

Den externt genererade målgruppens kontextdata, eller anrikningsattribut, är **not** de är långvariga, eftersom deras livscykel är knuten till den överförda publiken. På grund av sin övergående karaktär är dessa anrikningsattribut därför **not** som kan användas vid segmentering.

Men när ni mappar era målgrupper till batch- eller filbaserade mål kan ni använda dessa externt genererade berikande attribut för att förstärka era målgrupper och ytterligare aktiveringar i senare led.

Om du vill veta mer om den här funktionen kan du läsa guiden på [aktivera målgruppsdata till exportmål för gruppprofiler](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Finns det någon specifik kopplingsregel för externt genererade målgrupper?

Den organisationsspecifika standardprincipen för sammanfogning tillämpas automatiskt när externt genererade målgrupper överförs. Du kan dock ändra den sammanfogningsprincip som tillämpas på den externt genererade målgruppen under importarbetsflödet.

### Var kan jag aktivera externt genererade målgrupper?

En externt genererad publik kan mappas till alla RTCDP-mål och kan användas i Adobe Journey Optimizer-kampanjer.

### Hur snart är externt genererade målgrupper klara för aktivering?

Om data från den externt genererade publiken aktiveras till ett direktuppspelningsmål är de tillgängliga inom två timmar.

Om data från den externt genererade publiken aktiveras för en batchdestination synkroniseras de med nästa 24-timmarssegmenteringsjobb.

### Kan jag ta bort en externt genererad publik?

För närvarande kan du bara inaktivera en externt genererad publik. I det här läget, profiler **kommer** förbli aktiva för användning i nedströmstillämpningar. Stöd för att ta bort externt genererade målgrupper läggs till i en senare version.

### Vad ska jag göra om jag av misstag laddade upp en externt genererad publik?

Om du av misstag har överfört en externt genererad publik och vill ta bort data, kan du rensa profilerna som är kopplade till målgruppen genom att överföra en CSV-fil med en rad och utan data.

### Hur länge varar externt genererade målgrupper?

Det aktuella utgångsdatumet för externt genererade målgrupper är **30 dagar**. Utgångsdatumet har valts för att minska mängden överflödiga data som lagras i organisationen.

När förfalloperioden för data har passerat är den tillhörande datauppsättningen fortfarande synlig i datamängdslagret, men du kommer att **not** kan aktivera målgruppen och profilantalet visas som noll.

### Vad representerar de olika livscykelstatusarna?

I följande diagram förklaras de olika livscykelstatusarna, vad de representerar, där målgrupper med den statusen kan användas samt påverkan på segmenteringsskyddsutkast.

| Läge | Definition | Synligt i Audience Portal? | Synligt i destinationer? | Påverkar segmenteringsgränser? | Påverkan på filbaserade målgrupper | Effekter på publikutvärderingen | Kan användas inom andra målgrupper? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Utkast | En publik i **Utkast** är en publik som fortfarande är under utveckling och ännu inte är redo att användas i andra tjänster. | Ja, men kan vara dold. | Nej | Ja | Kan importeras eller uppdateras under förfiningsprocessen. | Kan utvärderas för att få korrekta publiceringsvärden. | Ja, men rekommenderas inte. |
| Publicerad | En publik i **Publicerad** är en publik som är klar att användas i alla tjänster i senare led. | Ja | Ja | Ja | Kan importeras eller uppdateras. | Utvärderat med gruppbearbetning, direktuppspelning eller kantsegmentering. | Ja |
| Inaktiv | En publik i **Inaktiv** är en publik som för närvarande inte används. Den finns fortfarande i plattformen, men den kommer att **not** vara användbar tills den markeras som utkast eller publicerad. | Nej, men kan visas. | Nej | Nej | Uppdaterades inte längre. | Inte längre utvärderat eller uppdaterat av Platform. | Ja |
| Borttagen | En publik i **Borttagen** status är en målgrupp som har tagits bort. Det kan ta upp till några minuter innan data tas bort. | Nej | Nej | Nej | Underliggande data tas bort. | Ingen utvärdering eller körning av data utförs efter att borttagningen har slutförts. | Nej |
| Aktiv | Den här statusen har **inaktuell** och ersätts med **Publicerad** status. | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt | Ej tillämpligt |

### Hur interagerar Audience Portal och Audience Composition med Real-Time CDP Partner Data?

Målportalen och målgruppskompositionen samverkar med partnerdata på två sätt:

1. Om du importerar en lista över potentiella kunder som tillhandahållits av en partner med hjälp av klassen Prospect Profile och arbetsflödet behålls dessa potentiella kunder **separat** från att sammanfoga kundprofiler i profiltjänsten. Detta innebär att listor över potentiella kunder kommer att **not** visas i antingen Audience Portal eller Audience Composition för användning.
2. Om du använder attribut som tillhandahålls av partners för att berika **befintlig** förstahandsprofiler, dessa målgrupper som bygger på partnerdata **kommer** visas i både Audience Portal och Audience Composition för användning.

### Hur kan jag använda ytterligare attribut med mina målgrupper?

Med målgrupper finns det **två** olika typer av ytterligare attribut du kan lägga till - nyttolastattribut (kontextuella) och anrikningsattribut.

Nyttolastattribut är attribut som importeras som en del av CSV-överföringen för en externt genererad publik. Dessa attribut är **not** Ingår i kundprofilen i realtid, men kan användas som en del av en nedströmsdestination.

Enrichment-attribut är attribut som kommer från en datauppsättning och som förenas med en målgrupp i Audience Composition. Dessa attribut kan för närvarande bara användas i Adobe Journey Optimizer-kampanjer. Stöd för Adobe Journey Optimizer resor kommer snart, med stöd för nedströmsdestinationer i väntan på framtida releaser.

| Aktiveringskanal | Målgrupper från anpassad CSV-överföring | Målgrupper från Audience Composition |
| --- | --- | --- |
| Real-Time CDP Destinations | Både nyttolastattributen och målgrupperna kan aktiveras. | Bara målgruppen kan aktiveras. Attribut för berikning **inte** aktiveras. |
| Adobe Journey Optimizer Campaigns | Varken målgruppen eller nyttolastattributen kan aktiveras. | Både målgrupps- och anrikningsattributen kan aktiveras. |

## Målgruppslager

I följande avsnitt listas frågor som rör målgruppslager i målgruppsportalen.

### Behöver jag ytterligare behörigheter för att kunna använda funktioner för målgruppslager?

Nej, det gör du inte. Så länge du har redigeringsbehörighet för målgrupper kan du skapa, uppdatera och hantera dina mappar och taggar i Audience Portal. Mer information om behörighetshantering finns i [hantera behörighetshandbok](../access-control/ui/permissions.md).

### Finns det någon gräns för hur många mappar jag kan skapa?

Nej, det finns ingen gräns för hur många mappar du kan skapa. Mer information om mappar finns i [mållagersektion](./ui/overview.md#folders) i översikten över segmenteringstjänstens gränssnitt.

### Finns det någon gräns för hur många taggar som kan läggas till en viss målgrupp?

Nej, det finns ingen gräns för hur många taggar som kan läggas till en målgrupp. Mer information om taggar finns i [mållagersektion](./ui/overview.md#tags) i översikten över segmenteringstjänstens gränssnitt.

### Finns det någon gräns för hur många taggar jag kan skapa?

Nej, det finns ingen gräns för hur många taggar du kan skapa. Du kan dock skapa högst **100** kategorier som ska användas för taggarna. Mer information om tagghantering finns i [Hantera taggar, guide](../administrative-tags/ui/managing-tags.md).

### När jag söker efter en målgrupp efter namn eller tagg i en överordnad mapp, kan jag då söka i de relaterade undermapparna?

Nej, det här beteendet stöds inte. Du kan dock ändra målgruppslagervyn så att den tittar på **Alla målgrupper** söker du sedan i alla mappar. Mer information om hur du använder sökning i målgruppslager finns i [sökavsnitt](./ui/overview.md#search) i översikten över segmenteringstjänstens gränssnitt.

### Kan jag automatiskt tilldela en målgrupp till en mapp när den skapas?

Vid den här tidpunkten, nej. Den här funktionen kan dock vara tillgänglig i framtiden.

### Kan jag flytta flera målgrupper till en mapp samtidigt?

Vid den här tidpunkten, nej. Den här funktionen kan dock vara tillgänglig i framtiden.

## Målgruppssammansättning

I följande avsnitt listas frågor som rör Audience Composition.

### När ska jag använda Audience Composition i stället för Segment Builder?

Både Audience Composition och Segment Builder har en viktig roll när det gäller att skapa målgrupper i Platform.

Segment Builder är bättre för publiken **skapa** (för att skapa en helt ny publik), medan Audience Composition är bättre för publiken **kurser och personalisering** (för att skapa nya målgrupper baserat på en befintlig målgrupp).

I följande tabell visas skillnaden mellan de två tjänsterna:

| Segment Builder | Målgruppssammansättning |
| --------------- | -------------------- |
| <ul><li>Generering av målgrupper i ett enda steg</li><li>Skapar de grundläggande blocken av målgrupper från profil-, tidsserie- och multientitetsdata</li><li>Används för att skapa **en** publik</li></ul> | <ul><li>Målgruppsgenerering i flera steg, med hjälp av set-baserade operationer</li><li>Använder målgrupper som skapats av Segment Builder och tillämpar databerikande alternativ som rankningsprofilattribut och uppdelning i undermålgrupper</li><li>Används för att skapa **flera** målgrupper samtidigt</li></ul> |

Läs mer om Segment Builder i [Segment Builder Guide](./ui/segment-builder.md). Läs mer om Audience Composition [Guide för målgruppssammansättning](./ui/audience-composition.md).

### Kan jag använda externt genererade målgrupper i Audience Composition?

Vid den här tidpunkten, nej. Denna kapacitet bör dock vara tillgänglig inom den närmaste framtiden.

### Kan jag skicka målgrupper från Audience Composition till alla destinationer och kanaler längre fram i kedjan?

Vid den här tidpunkten, nej. För närvarande kan ni använda målgrupper från Audience Composition i Adobe Journey Optimizer Campaigns och Real-Time CDP destinationer. Adobe Journey Optimizer Journeys kommer att få stöd i en kommande version.

### Finns det några skyddsräcken för antalet kompositioner?

För tillfället kan du bara ha **10** publicerade kompositioner per sandlåda. Garantin planeras att utökas i en framtida version.

### Vilka är arbetsflödesgarantierna för Audience Composition?

Komponentplaceringen följer en hård struktur enligt följande:

1. Du **alltid** börja med [!UICONTROL Audience] -block för att välja din startaktivitet. Du kan ha högst **en** [!UICONTROL Audience] -block.
2. Du kan lägga till en [!UICONTROL Exclude] -block som följer efter [!UICONTROL Audience] -block.
3. Du kan lägga till en [!UICONTROL Enrich] -block som följer efter [!UICONTROL Exclude] -block. Du kan bara använda **en** [!UICONTROL Enrich] block per disposition.
4. Du kan lägga till en [!UICONTROL Rank] eller [!UICONTROL Split] -block. Du kan **endast** har ett av dessa block per komposition.
5. Du **alltid** end with a [!UICONTROL Save] blockera för att rädda er målgrupp.

Följande begränsningar (?) gäller när du använder dessa block:

- Delat block
   - Det här blocket stöder bara **Sträng** datatyper. Delningsblocket gör det **not** har stöd för datatypen date eller boolean.
   - Dessutom gör det här blocket **not** stödja anrikningsattribut.
- Exkludera block
   - Detta block gör **not** har stöd för datatypen date eller boolean.
- Rankningsblock
   - Detta block gör **not** stödja anrikningsattribut.

Läs mer om hur du använder Audience Composition [Användargränssnittsguide för målgruppskomposition](./ui/audience-composition.md).

### När sparas och utvärderas målgrupper som skapats med Audience Composition?

Publiken sparas automatiskt när de skapas i Audience Composition. Publiken skapas första gången som detta sparas automatiskt.

När målgruppen har skapats kan det ta upp till 24 timmar att utvärdera den.

### När kan jag använda den målgrupp jag skapat?

Publiken som skapas i Audience Composition kommer att **omedelbart** visas i Audience Portal. För att kunna använda programmet i Adobe Journey Optimizer måste du dock vänta minst 24 timmar efter utvärderingen.

### Är utvärderingsjobb synliga i övervakningsavsnittet?

För närvarande är utvärderingsjobb **not** visas i övervakningsgränssnittet.

### Kan jag använda en Audience Composition i en annan komposition?

Nej, målgrupper skapade med Audience Composition **inte** användas som indata i en annan målgruppssammansättning.

### Hur fungerar delning i Audience Composition?

Genom att dela målgrupper kan ni ytterligare dela upp er målgrupp i mindre grupper.

När grupper delas upp efter attribut sker ömsesidig exklusivitet mellan grupperna. Det innebär att om en post uppfyller villkoren för flera delade sökvägar tilldelas den **först** till vänster och **not** som tilldelats någon av de andra sökvägarna.

Vid uppdelning efter procent delas partitionerna **slumpmässigt** klart. Detta innebär att profilerna tilldelas slumpmässigt till varje bana. Delningen är **not** beständig så att profilen kan befinna sig i olika delar av gruppen vid varje utvärdering.

Mer information om det delade blocket finns i [Användargränssnittsguide för målgruppskomposition](./ui/audience-composition.md#split).

### Kan jag använda alla segmenteringstyper i arbetsflödet Målgruppskomposition?

Ja, alla segmenteringstyper ([gruppsegmentering, direktuppspelningssegmentering och kantsegmentering](./home.md#evaluate-segments)) stöds i arbetsflödet Audience Composition. Men eftersom kompositioner för närvarande bara körs en gång per dag, även om en målgrupp som är en direktuppspelnings- eller edge-utvärderad målgrupp inkluderas, kommer resultatet att baseras på målgruppsmedlemskap när kompositionen utfördes.

## Målgruppsmedlemskap

I följande avsnitt listas frågor som rör medlemskap för målgrupper.

### Hur kan jag bekräfta en profils medlemskap för en viss målgrupp?

Om du vill bekräfta en profils målgruppsmedlemskap går du till sidan med profilinformation för den profil du vill bekräfta. Välj **[!UICONTROL Attributes]**, följt av **[!UICONTROL View JSON]** och du kan bekräfta att `segmentMembership` -objektet innehåller målgruppens ID.

### Hur löser batchsegmentering profilmedlemskapet?

Målgrupper som utvärderas med batchsegmentering löses dagligen, och målgruppsmedlemskapsresultaten registreras i profilens `segmentMembership` -attribut. Profilsökningar genererar en ny version av profilen vid tidpunkten för sökningen, men det gör den **not** uppdatera gruppsegmenteringsresultaten.

När du gör ändringar i profilen, till exempel sammanfogar två profiler, innebär detta att dessa ändringar **kommer** visas i profilen vid sökning, men kommer att **not** återspeglas i `segmentMembership` tills segmentutvärderingsjobbet har körts igen.

Låt oss till exempel säga att du har skapat två ömsesidigt uteslutande målgrupper: målgrupp A är för människor som bor i Washington och målgrupp B är för människor som gör **not** bor i Washington. Det finns två profiler - profil 1 för en person som bor i Washington och profil 2 för en person som bor i Oregon.

När utvärderingsjobbet för gruppsegmentering körs går profil 1 till Audience A, medan profil 2 går till Audience B. Senare, men innan nästa dags utvärderingsjobb för gruppsegmentering körs, kommer en händelse som synkroniserar de två profilerna att gå in i Platform. Därför skapas en sammanfogad profil som innehåller profilerna 1 och 2.

Tills nästa utvärderingsjobb för gruppsegment körs kommer den nya sammanfogade profilen att ha ett målgruppsmedlemskap i **båda** profil 1 och profil 2. Det innebär att den blir medlem i **båda** Målgrupp A och målgrupp B, trots att dessa målgrupper har motsägande definitioner. För slutanvändaren är detta **exakt samma situation** som innan profilerna kopplades samman, eftersom det alltid var bara den enda berörda personen, och Platform gjorde precis **not** har tillräckligt med information för att koppla ihop de två profilerna.

Om du använder profilsökning för att hämta den nyligen skapade profilen och tittar på dess målgruppsmedlemskap visar det att den är medlem i **båda** Audience A och Audience B, trots att båda dessa målgrupper har motstridiga definitioner. När det dagliga utvärderingsjobbet för gruppsegmentering körs uppdateras målgruppsmedlemskapet för att återspegla det uppdaterade läget för profildata.

Om ni behöver en större målgruppsupplösning i realtid använder ni strömning eller kantsegmentering.

### Hur lång tid tar det att strömma data ska vara tillgängliga i arbetsflöden för gruppsegmentering?

Det kan ta upp till tre timmar innan strömmande data är tillgängliga i arbetsflöden för gruppsegmentering.

Om ett batchsegmenteringsjobb till exempel körs på 9:00, är det garanterat att det innehåller direktuppspelade indata **upp till** 6:00. Direktuppspelning av inkapslade data som har importerats efter 6.00 men före 20.00 **kan** ingår.

