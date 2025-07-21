---
title: Frågor och svar
description: Få svar på vanliga frågor om målgrupper och andra segmenteringsrelaterade koncept.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 721024192b54fcbab11b483cc26fa84151bb61a7
workflow-type: tm+mt
source-wordcount: '4821'
ht-degree: 0%

---

# Vanliga frågor och svar

Adobe Experience Platform [!DNL Segmentation Service] innehåller ett användargränssnitt och RESTful API som gör att du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper konfigureras och underhålls centralt på Experience Platform och är tillgängliga via alla Adobe-lösningar. Nedan följer en lista med vanliga frågor om målgrupper och segmentering.

## Målgruppsportal

I följande avsnitt listas frågor som rör Audience Portal.

### Har jag tillgång till Audience Portal och Audience Composition?

Audience Portal och Audience Composition är tillgängliga för alla Real-Time CDP Prime- och Ultimate-kunder (B2C, B2B och B2P Editions) samt för Journey Optimizer Select-, Prime-, Ultimate Starter- och Ultimate-kunder.

I nuläget stöds endast profilbaserade målgrupper. Stöd för kontobaserade målgrupper kommer att läggas till i en senare version.

### Stöds externt genererade förbyggda målgrupper med Audience Portal?

Ja, externt genererade färdiga målgrupper stöds med Audience Portal. Nu kan du importera en externt genererad publik via en CSV-fil. I framtiden kommer ni att kunna lägga till målgrupper via batchanslutningar eller direktuppspelningsbaserade källkopplingar.

### Vilka behörigheter behöver jag för att kunna överföra externt genererade målgrupper?

För att kunna överföra externt genererade målgrupper måste du ha behörigheterna Visa segment, Hantera segment och Importera målgrupper. Det finns inga specifika rollbaserade kontroller som krävs för att överföra externt genererade målgrupper.

### Vad händer när jag överför en externt genererad publik?

När du överför en externt genererad publik skapas en datauppsättning som är synlig i datamängdslagret. Namnet på datauppsättningen blir **detsamma** som namnet på den externt genererade målgruppen som du överförde.

### Vad består en externt genererad publik av och vad händer med dessa data när de importeras till Experience Platform?

Under arbetsflödet för att importera externa målgrupper måste du ange vilken kolumn i CSV-filen som motsvarar **Primär identitet**. Ett exempel på en primär identitet är e-postadress, ECID eller ett organisationsspecifikt namnområde för en anpassad identitet.

Data som är associerade med den här primära identitetskolumnen är de **enda** data som är kopplade till profilen. Om det inte finns några befintliga profiler som matchar data i den primära identitetskolumnen skapas en ny profil. Den här profilen är emellertid i princip en överbliven profil eftersom **inga**-attribut eller upplevelsehändelser är associerade med den här profilen.

Alla andra data inom den externt genererade målgruppen betraktas som **nyttolastattribut**. Dessa attribut kan **endast** användas för personalisering och berikning under aktivering, och är **inte** kopplade till en profil. Dessa attribut lagras dock i datasjön.

Även om den externt genererade målgruppen kan refereras när målgrupper skapas med segmentbyggaren, kan enskilda profilattribut **inte** användas.

### Kan jag stämma av externt genererade målgruppsdata med en befintlig profil i Experience Platform?

Ja, den externt genererade målgruppen sammanfogas med den befintliga profilen i Experience Platform om de primära identifierarna matchar. Det kan ta upp till 24 timmar att stämma av dessa data. Om det inte redan finns profildata skapas en ny profil när data hämtas.

### Hur respekteras inställningarna för kundsamtycke för externt genererade målgrupper som importeras till Audience Portal?{#consent}

När kunddata hämtas från flera kanaler kan identitetssammanfogning och sammanfogningsprinciper göra att dessa data kan samlas i en enda kundprofil i realtid. Information om kundernas samtycke lagras och utvärderas på profilnivå.

Destinationer i senare led kontrollerar varje profil för att se om de godkänner informationen innan de aktiveras. Varje profils godkännandeinformation jämförs med medgivandekraven för en viss destination. Om profilen inte uppfyller kraven skickas den profilen inte till något mål.

När en extern målgrupp hämtas till Audience Portal förenas de med befintliga profiler med hjälp av ett primärt ID som e-post eller ECID. Till följd av detta kommer de befintliga reglerna för samtycke att gälla under hela aktiveringen.

Observera att du **inte** ska inkludera medgivandeinformation med en externt genererad publik, eftersom nyttolastvariablerna **inte** lagras i profilarkivet utan i datasjön. I stället **måste** använda en Adobe Experience Platform-inmatningskanal där profildata importeras.

### Kan jag använda en externt genererad publik för att bygga andra målgrupper?

Ja, alla externt genererade målgrupper visas i målgruppslagret och kan användas när målgrupper skapas i [Segment Builder](./ui/segment-builder.md).

### Hur ofta utvärderas externt genererade målgrupper?

Externt genererade målgrupper utvärderas **endast** under importen. Eftersom de associerade attributen för de här importerande målgrupperna är icke-varaktiga och **inte** är en del av profilarkivet, är den enda gången en externt genererad målgrupp uppdateras om den befintliga målgruppen uppdateras manuellt.

### Kan jag använda externt överförda attribut som en del av segmenteringen?

Nej, det kan du inte. Profilattribut är avsedda att vara långvariga attribut, medan externt genererade målgruppsdata som överförs bara innehåller kontextuella data som är kopplade till den externt genererade målgruppen.

Den externt genererade målgruppens kontextuella data, eller anrikningsattribut, är **inte** varaktiga, eftersom deras livscykel är knuten till den överförda målgruppen. På grund av dess övergående karaktär är därför dessa anrikningsattribut **inte** tillgängliga för segmentering.

Men när ni mappar era målgrupper till batch- eller filbaserade mål kan ni använda dessa externt genererade berikande attribut för att förstärka era målgrupper och ytterligare aktiveringar i senare led.

Om du vill veta mer om den här funktionen kan du läsa guiden om att [aktivera målgruppsdata för exportmål för gruppprofiler](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Finns det någon specifik kopplingsregel för externt genererade målgrupper?

Den organisationsspecifika standardprincipen för sammanfogning tillämpas automatiskt när externt genererade målgrupper överförs. Du kan dock ändra den sammanfogningsprincip som tillämpas på den externt genererade målgruppen under importarbetsflödet.

### Var kan jag aktivera externt genererade målgrupper?

En externt genererad målgrupp kan mappas till vilken destination som helst och kan användas i Adobe Journey Optimizer kampanjer och resor.

### Kan jag ta bort en externt genererad publik?

Ja! Externt genererade målgrupper kan tas bort i Audience Portal.

### Vad ska jag göra om jag av misstag laddade upp en externt genererad publik?

Om du av misstag har överfört en externt genererad publik och vill ta bort data, kan du rensa profilerna som är kopplade till målgruppen genom att överföra en CSV-fil med en rad och utan data.

### Hur länge varar externt genererade målgrupper?

Aktuell datagräns för externt genererade målgrupper är **30 dagar**. Utgångsdatumet har valts för att minska mängden överflödiga data som lagras i organisationen.

När dataförfalloperioden har passerat är den associerade datauppsättningen fortfarande synlig i datamängdslagret, men du **inte** kan aktivera målgruppen och profilantalet visas som noll.

### Finns det ett maximalt antal externt genererade målgrupper jag kan importera?

Det finns ingen gräns för hur många externt genererade målgrupper du kan importera. Observera dock att de importerade målgrupperna **do** räknas av mot den totala målgruppsgränsen.

### Hur interagerar Audience Portal och Audience Composition med Real-Time CDP Partner Data?

Målportalen och målgruppskompositionen samverkar med partnerdata på två sätt:

1. Om du importerar en lista med potentiella kunder som tillhandahållits av en partner med hjälp av klassen Prospect Profile och arbetsflödet behålls de potentiella kunderna **separat** från sammanfogningen av kundprofiler i profiltjänsten. Detta innebär att listor med potentiella kunder **inte** visas i antingen Audience Portal eller Audience Composition för användning.
2. Om du använder attribut som tillhandahålls av partners för att berika **befintliga** förstapartsprofiler, kommer dessa målgrupper som berikas av partnerdata **att** visas i både Audience Portal och Audience Composition för användning.

### Hur kan jag använda ytterligare attribut med mina målgrupper?

För målgrupper finns det **två** olika typer av ytterligare attribut som du kan lägga till - nyttolastattribut (sammanhangsberoende) och anrikningsattribut.

Nyttolastattribut är attribut som importeras som en del av CSV-överföringen för en externt genererad publik. De här attributen är **inte** inkapslade i kundprofilen i realtid, men kan användas som en del av ett nedladdat mål.

Enrichment-attribut är attribut som kommer från en datauppsättning och som förenas med en målgrupp i Audience Composition. Dessa attribut kan för närvarande bara användas i Adobe Journey Optimizer-kampanjer. Stöd för Adobe Journey Optimizer resor kommer snart, med stöd för nedströmsdestinationer i väntan på framtida releaser.

| Aktiveringskanal | Målgrupper från anpassad CSV-överföring | Målgrupper från Audience Composition |
| --- | --- | --- |
| Real-Time CDP Destinations | Både nyttolastattributen och målgrupperna kan aktiveras. | Bara målgruppen kan aktiveras. Det går inte att aktivera anrikningsattributen ****. |
| Adobe Journey Optimizer Campaigns | Varken målgruppen eller nyttolastattributen kan aktiveras. | Både målgrupps- och anrikningsattributen kan aktiveras. |

## Livscykeltillstånd {#lifecycle-states}

I följande avsnitt listas frågor som rör livscykeltillstånd och livscykelstatushantering i Audience Portal.

### Vad representerar de olika livscykelstatusarna?

I följande diagram förklaras de olika livscykelstatusarna, vad de representerar, där målgrupper med den statusen kan användas samt påverkan på segmenteringsskyddsutkast.

| Läge | Definition | Synligt i Audience Portal? | Synligt i destinationer? | Påverkar segmenteringsgränser? | Påverkan på filbaserade målgrupper | Effekter på publikutvärderingen | Kan användas inom andra målgrupper? | Redigerbar |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Utkast | En målgrupp i läget **Utkast** är en målgrupp som fortfarande är under utveckling och ännu inte är redo att användas i andra tjänster. | Ja, men kan vara dold. | Nej | Ja | Kan importeras eller uppdateras under förfiningsprocessen. | Utvärderad för korrekt publiceringsantal. | Ja, men rekommenderas inte. | Ja |
| Publicerad | En målgrupp i läget **Publicerad** är en målgrupp som är klar att användas för alla tjänster längre fram i kedjan. | Ja | Ja | Ja | Kan importeras eller uppdateras. | Utvärderat med gruppbearbetning, direktuppspelning eller kantsegmentering. | Ja | Ja |
| Inaktiv | En målgrupp i läget **Inaktiv** är en målgrupp som för närvarande inte används. Den finns fortfarande i Experience Platform, men den kommer **inte** att vara användbar förrän den markeras som utkast eller publicerad. | Nej, men kan visas. | Nej | Nej | Uppdaterades inte längre. | Inte längre utvärderat eller uppdaterat av Experience Platform. | Nej | Ja |
| Borttagen | En målgrupp i läget **Borttagen** är en målgrupp som har tagits bort. Det kan ta upp till några minuter innan data tas bort. | Nej | Nej | Nej | Underliggande data tas bort. | Ingen utvärdering eller körning av data utförs efter att borttagningen har slutförts. | Nej | Nej |

### I vilka lägen kan jag redigera mina målgrupper i?

Publiker kan redigeras i följande livscykelsteg:

- **Utkast**: Om en målgrupp redigeras i utkastläget förblir den i utkastläget såvida den inte uttryckligen publiceras.
- **Publicerad**: Om en målgrupp redigeras i det publicerade läget förblir den publicerad och målgruppen uppdateras automatiskt.
- **Inaktiv**: Om en målgrupp redigeras i inaktivt läge förblir den inaktiv. Detta innebär att det inte kommer att utvärderas eller uppdateras. Om ni behöver uppdatera målgruppen måste ni publicera målgruppen.

När en målgrupp har tagits bort kan den **inte** redigeras.

### Vilka livscykeltillstånd kan jag flytta en målgrupp till?

Möjliga livscykeltillstånd som en målgrupp kan flyttas till beror på målgruppens aktuella tillstånd.

![Ett diagram som visar vilka övergångar för livscykeltillstånd som är tillgängliga för målgrupper.](./images/faq/lifecycle-state-transition.png)

Om målgruppen är i utkastläget kan du antingen publicera eller ta bort den om målgruppen inte har några beroenden.

Om målgruppen är i publicerat läge kan du antingen inaktivera eller ta bort den om målgruppen inte har några beroenden.

Om publiken är i inaktivt läge kan du antingen publicera om eller ta bort den om publiken inte har några beroenden.

### Finns det några kavattar för målgrupper i vissa livscykeltillstånd?

Publikationer i det publicerade läget kan bara flyttas till ett annat läge om publiken **inte** har några beroenden. Det innebär att om målgruppen används i en tjänst längre fram i kedjan kan den inte inaktiveras eller tas bort.

Om en målgrupp som utvärderas med batchsegmentering publiceras på nytt, vilket innebär att en målgrupp går från inaktiv till publicerad, kommer målgruppen att uppdatera **efter** det dagliga batchjobbet. När det publiceras på nytt första gången blir profilerna och data **samma** som när målgruppen blev inaktiv.

### Hur sätter jag en publik i utkastläget?

Vilken metod som ska användas för att sätta en målgrupp i utkastläget beror på målgruppens ursprung.

För målgrupper som har skapats med Segment Builder kan du ange målgruppen till utkastläget genom att välja [!UICONTROL Save as draft] i Segment Builder.

För målgrupper som skapats i Audience Composition sparas målgrupperna automatiskt som ett utkast tills de publiceras.

För externa målgrupper publiceras målgrupper automatiskt.

När en målgrupp har publicerats kan du **inte** ändra tillbaka den ursprungliga målgruppen till utkastläget. Om du kopierar målgruppen kommer den kopierade målgruppen att vara i utkastläget.

### Hur sätter jag en publik i det publicerade läget?

För målgrupper som har skapats med Segment Builder eller Audience Composition kan du ange målgruppen till publicerat läge genom att välja [!UICONTROL Publish] i deras respektive användargränssnitt.

Externa målgrupper anges automatiskt till publicerade.

### Hur sätter jag en publik i det inaktiva läget?

Du kan försätta en publicerad publik i inaktivt läge genom att öppna snabbåtgärdsmenyn i Audience Portal och välja [!UICONTROL Deactivate].

### Hur återpublicerar jag en publik?

>[!NOTE]
>
>Det ompublicerade läget är samma som det publicerade läget för målgruppsbeteenden.

Du kan publicera en målgrupp på nytt genom att välja en målgrupp som är inaktiv, öppna snabbåtgärdsmenyn på Audience Portal och välja [!UICONTROL Publish].

### Hur placerar jag en målgrupp i borttaget läge?

>[!IMPORTANT]
>
>Du kan bara ta bort målgrupper som **inte** används i efterföljande aktiveringar. Dessutom kan du inte ta bort en målgrupp som refereras till av en annan målgrupp. Om du inte kan ta bort din målgrupp kontrollerar du att du **inte** använder den i någon underordnad tjänst eller som en byggsten för en annan målgrupp.

Du kan försätta en målgrupp i borttagningsläget genom att öppna snabbåtgärdsmenyn i målportalen och välja [!UICONTROL Delete].

### Finns det några kavattar för övergångar i livscykeltillstånd?

Ja, det finns en del kavajer att vara medveten om när ni använder målgrupper i tjänster längre fram i kedjan som Adobe Journey Optimizer eller icke-kundbaserade målgrupper som kontobaserade målgrupper.

För närvarande **måste** kontrollera manuellt om målgruppen används längre fram i Adobe Journey Optimizer, eftersom den här statusen för närvarande inte kontrolleras automatiskt.

Dessutom **måste** kontrollera manuellt om målgruppen används som en komponent i en kontobaserad målgrupp, eftersom den här statusen inte kontrolleras automatiskt för närvarande.

### Vad händer när jag kopierar en publik? {#copy}

När du kopierar en målgrupp är den nya målgruppen i utkastläget och behåller samma mappar, taggar och etiketter som tillämpades på den ursprungliga målgruppen.

### Påverkar användningen av en målgrupp som underordnad målgrupp övergångar i livscykeln?

>[!NOTE]
>
>En överordnad målgrupp är en målgrupp som **använder** till som ett beroende för målgruppen.
>
>En underordnad målgrupp är en målgrupp som **används som** ett beroende för målgruppen.

Ja, att använda en målgrupp som underordnad målgrupp påverkar vilka livscykelsteg som den underordnade och överordnade målgruppen kan genomföra.

För att en underordnad publik ska kunna flyttas till det publicerade läget måste alla dess överordnade målgrupp **vara i publicerat läge.**. Överordnade målgrupper kan antingen publiceras innan den underordnade målgruppen publiceras eller, om användaren bekräftar det, kan publiceras automatiskt när den underordnade målgruppen publiceras.

För att den överordnade målgruppen ska kunna flyttas till det inaktiva eller borttagna läget måste alla dess underordnade målgrupper **inaktiveras eller tas bort**.

### Kan jag hänvisa till en målgrupp som befinner sig i ett annat livscykeltillstånd?

Ja! Om målgruppen för närvarande är i utkastläget kan du referera till målgrupper i antingen utkastläget eller publiceringsläget. Om du vill publicera den här målgruppen **måste** publicera de andra överordnade målgrupperna.

## Målgruppslager

I följande avsnitt listas frågor som rör målgruppslager i målgruppsportalen.

### Behöver jag ytterligare behörigheter för att kunna använda funktioner för målgruppslager?

Nej, det gör du inte. Så länge du har redigeringsbehörighet för målgrupper kan du skapa, uppdatera och hantera dina mappar och taggar i Audience Portal. Mer information om hur du hanterar behörigheter finns i [handboken om att hantera behörigheter](../access-control/ui/permissions.md).

### Finns det någon gräns för hur många mappar jag kan skapa?

Nej, det finns ingen gräns för hur många mappar du kan skapa. Mer information om mappar finns i [målgruppslageravsnittet](./ui/audience-portal.md#folders) i översikten över segmenteringstjänstens användargränssnitt.

### Finns det någon gräns för hur många taggar som kan läggas till en viss målgrupp?

Nej, det finns ingen gräns för hur många taggar som kan läggas till en målgrupp. Mer information om taggar finns i [målgruppslageravsnittet](./ui/audience-portal.md#tags) i översikten över användargränssnittet för segmenteringstjänsten.

### Finns det någon gräns för hur många taggar jag kan skapa?

Nej, det finns ingen gräns för hur många taggar du kan skapa. Du kan dock skapa högst **100** kategorier som ska användas för taggarna. Mer information om tagghantering finns i handboken [Hantera taggar](../administrative-tags/ui/managing-tags.md).

### När jag söker efter en målgrupp efter namn eller tagg i en överordnad mapp, kan jag då söka i de relaterade undermapparna?

Nej, det här beteendet stöds inte. Du kan dock ändra målgruppslagervyn så att den tittar på **Alla målgrupper** och sedan söka i alla mappar. Mer information om hur du använder sökning i målgruppslager finns i [sökavsnittet](./ui/audience-portal.md#search) i översikten över användargränssnittet för segmenteringstjänsten.

### Kan jag automatiskt tilldela en målgrupp till en mapp när den skapas?

Vid den här tidpunkten, nej. Den här funktionen kan dock vara tillgänglig i framtiden.

### Kan jag flytta flera målgrupper till en mapp samtidigt?

Vid den här tidpunkten, nej. Den här funktionen kan dock vara tillgänglig i framtiden.

## Målgruppssammansättning

I följande avsnitt listas frågor som rör Audience Composition.

### När ska jag använda Audience Composition i stället för Segment Builder?

Både Audience Composition och Segment Builder har en viktig roll när det gäller att skapa målgrupper i Experience Platform.

Segment Builder passar bättre för målgruppen **creation** (för att skapa en målgrupp från grunden), medan Audience Composition är bättre lämpat för målgruppen **kuration och personalisering** (för att skapa nya målgrupper baserat på en befintlig målgrupp).

I följande tabell visas skillnaden mellan de två tjänsterna:

| Segment Builder | Målgruppssammansättning |
| --------------- | -------------------- |
| <ul><li>Generering av målgrupper i ett enda steg</li><li>Skapar de grundläggande blocken av målgrupper från profil-, tidsserie- och multientitetsdata</li><li>Används för att skapa **en**-målgrupp</li></ul> | <ul><li>Målgruppsgenerering i flera steg, med hjälp av set-baserade operationer</li><li>Använder målgrupper som skapats av Segment Builder och tillämpar databerikande alternativ som rankningsprofilattribut och uppdelning i undermålgrupper</li><li>Används för att skapa **flera** målgrupper samtidigt</li></ul> |

Mer information om segmentbyggaren finns i guiden [Segment Builder](./ui/segment-builder.md). Mer information om Audience Composition finns i guiden [Audience Composition](./ui/audience-composition.md).

### Kan jag använda externt genererade målgrupper i Audience Composition?

Vid den här tidpunkten, nej. Denna kapacitet bör dock vara tillgänglig inom den närmaste framtiden.

### Kan jag skicka målgrupper från Audience Composition till alla destinationer och kanaler längre fram i kedjan?

Vid den här tidpunkten, nej. För närvarande kan ni använda målgrupper från Audience Composition i Adobe Journey Optimizer Campaigns och Real-Time CDP destinationer. Adobe Journey Optimizer Journeys kommer att få stöd i en kommande version.

### Finns det några skyddsräcken för antalet kompositioner?

För närvarande kan du bara ha **10** publicerade kompositioner per sandlåda. Garantin planeras att utökas i en framtida version.

### Vilka är arbetsflödesgarantierna för Audience Composition?

Komponentplaceringen följer en hård struktur enligt följande:

1. Du **alltid** börjar med blocket [!UICONTROL Audience] för att välja din startaktivitet. Du kan ha högst **ett** [!UICONTROL Audience] block.
2. Du kan också lägga till ett [!UICONTROL Exclude]-block som följer efter [!UICONTROL Audience]-blocket.
3. Du kan också lägga till ett [!UICONTROL Enrich]-block som följer efter [!UICONTROL Exclude]-blocket. Du kan bara använda **ett** [!UICONTROL Enrich]-block per disposition.
4. Du kan också lägga till ett [!UICONTROL Rank]- eller [!UICONTROL Split]-block. Du kan **bara** ha ett av dessa block per disposition.
5. Du **alltid** slutar med ett [!UICONTROL Save]-block för att spara din publik.

Dessutom gäller följande begränsningar när du använder dessa block:

- Delat block
   - Det här blocket har bara stöd för datatyperna **String**. Delningsblocket stöder **inte** datatypen date eller boolean.
   - Det här blocket har dessutom **inte** stöd för anrikningsattribut.
- Exkludera block
   - Det här blocket stöder **inte** datatypen date eller boolean.
- Rankningsblock
   - Det här blocket stöder **inte** anrikningsattribut.

Mer information om hur du använder Audience Composition finns i handboken [Audience Composition UI](./ui/audience-composition.md).

### När sparas och utvärderas målgrupper som skapats med Audience Composition?

Publiken sparas automatiskt när de skapas i Audience Composition. Publiken skapas första gången som detta sparas automatiskt.

När publikens komposition har skapats kan det ta upp till 48 timmar innan den kan utvärderas och aktiveras för användning i underordnade tjänster som en Real-Time CDP-destination eller en Adobe Journey Optimizer-kanal.

### När kan jag använda den målgrupp jag skapat?

Publiken som skapas i Audience Composition **visas omedelbart** i Audience Portal. För att kunna använda programmet i tjänster som Adobe Journey Optimizer längre fram i kedjan måste du dock vänta minst 24 timmar efter utvärderingen.

### Är utvärderingsjobb synliga i övervakningsavsnittet?

För närvarande visas utvärderingsjobb **inte** i övervakningsgränssnittet.

### Kan jag använda en Audience Composition i en annan komposition?

Nej, målgrupper som skapats med målgruppsdisposition **kan inte** användas som indata i en annan målgruppsdisposition.

### Hur fungerar delning i Audience Composition?

Genom att dela målgrupper kan ni ytterligare dela upp er målgrupp i mindre grupper.

När grupper delas upp efter attribut sker ömsesidig exklusivitet mellan grupperna. Det innebär att om en post uppfyller villkoren för flera delade sökvägar tilldelas den **första**-sökvägen från vänster och **inte** till någon av de andra sökvägarna.

Vid uppdelning efter procent är delningarna **slumpmässigt** klara. Detta innebär att profilerna tilldelas slumpmässigt till varje bana.

Mer information om det delade blocket finns i handboken [Målgruppsdisposition](./ui/audience-composition.md#split).

### Kan jag använda alla segmenteringstyper i arbetsflödet Målgruppskomposition?

Ja, alla segmenteringstyper ([gruppsegmentering, direktuppspelningssegmentering och kantsegmentering](./home.md#evaluate-segments)) stöds i arbetsflödet för målgruppskomposition. Men eftersom kompositioner för närvarande bara körs en gång per dag, även om en målgrupp som är en direktuppspelnings- eller edge-utvärderad målgrupp inkluderas, kommer resultatet att baseras på målgruppsmedlemskap när kompositionen utfördes.

## Målgruppsmedlemskap

I följande avsnitt listas frågor som rör medlemskap för målgrupper.

### Hur kan jag bekräfta en profils medlemskap för en viss målgrupp?

Om du vill bekräfta en profils målgruppsmedlemskap går du till sidan med profilinformation för den profil du vill bekräfta. Välj **[!UICONTROL Attributes]**, följt av **[!UICONTROL View JSON]**, så kan du bekräfta att objektet `segmentMembership` innehåller målgruppens ID.

### Kan målgruppsmedlemskapet växla mellan idealiskt och faktiskt medlemskap?

Ja, målgruppsmedlemskapet kan avvika från det idealiska och det faktiska medlemskapet om en målgrupp utvärderas med hjälp av direktuppspelningssegmentering **och** som målgruppen baseras på en målgrupp som utvärderats med batchsegmentering.

Om till exempel Audience A är baserad på Audience B och Audience B utvärderas med batchsegmentering, eftersom Audience B bara uppdateras var 24:e timme, kommer Audience A att gå längre bort från de faktiska data som synkroniseras om med Audience B-uppdateringarna.

## Gruppsegmentering {#batch-segmentation}

I följande avsnitt visas frågor som rör gruppsegmentering.

### Hur löser batchsegmentering profilmedlemskapet?

Publiker som utvärderats med batchsegmentering löses dagligen, med målgruppsmedlemskapsresultaten registrerade i profilens `segmentMembership`-attribut. Profilsökningar genererar en ny version av profilen vid tidpunkten för sökningen, men uppdaterar **inte** gruppsegmenteringsresultaten.

Detta innebär att när ändringar görs i profilen, som att slå samman två profiler, visas dessa ändringar **i** i profilen när de slås upp, men **inte** återspeglas i attributet `segmentMembership` förrän segmentutvärderingsjobbet har körts igen.

Låt oss till exempel säga att du har skapat två ömsesidigt uteslutande målgrupper: Audience A är till för personer som bor i Washington och Audience B är till för personer som **inte** bor i Washington. Det finns två profiler - profil 1 för en person som bor i Washington och profil 2 för en person som bor i Oregon.

När utvärderingsjobbet för gruppsegmentering körs går profil 1 till Audience A, medan profil 2 går till Audience B. Senare, men innan nästa dags utvärderingsjobb för gruppsegmentering körs, kommer en händelse som synkroniserar de två profilerna att gå in i Experience Platform. Därför skapas en sammanfogad profil som innehåller profilerna 1 och 2.

Tills nästa utvärderingsjobb för gruppsegment körs, kommer den nya sammanfogade profilen att ha ett målgruppsmedlemskap i **både** och profil 2. Detta innebär att den kommer att vara medlem i **både** och Audience B, trots att dessa målgrupper har motstridiga definitioner. För slutanvändaren är detta **exakt samma situation** som innan profilerna anslöts, eftersom det alltid bara var den enda berörda personen, och Experience Platform har **inte** bara haft tillräckligt med information för att koppla ihop de två profilerna.

Om du använder profilsökning för att hämta den nyligen skapade profilen och tittar på dess målgruppsmedlemskap, kommer det att visa att den är medlem i **både** och Publikens A och Publikens B, trots att båda dessa målgrupper har motsägande definitioner. När det dagliga utvärderingsjobbet för gruppsegmentering körs uppdateras målgruppsmedlemskapet för att återspegla det uppdaterade läget för profildata.

Om ni behöver en större målgruppsupplösning i realtid använder ni strömning eller kantsegmentering.

### Hur lång tid tar det att strömma data ska vara tillgängliga i arbetsflöden för gruppsegmentering?

Det kan ta upp till tre timmar innan strömmande data är tillgängliga i arbetsflöden för gruppsegmentering.

Om ett batchsegmenteringsjobb till exempel körs vid 9:0, är det garanterat att det innehåller direktuppspelade indata **fram till** 6:0. Direktuppspelning av inkapslade data som har importerats efter 6.0 men före 20.00 **inkluderas.**

## Edge segmentering {#edge-segmentation}

I följande avsnitt visas frågor om kantsegmentering.

### Hur lång tid tar det innan en segmentdefinition är tillgänglig på Edge Network?

Det tar upp till en timme innan en segmentdefinition är tillgänglig på Edge Network.

## Direktuppspelningssegmentering {#streaming-segmentation}

I följande avsnitt visas frågor om direktuppspelningssegmentering.

### Händer direktuppspelad segmentering&quot;utan kvalificering&quot; också i realtid?

I de flesta fall sker icke-kvalificering av direktuppspelad segmentering i realtid. Direktuppspelningssegment som använder segment av segment saknar dock **inte** behörighet i realtid, utan kvalificerar sig inte efter 24 timmar.

### Vilka data fungerar direktuppspelningssegmentering på?

Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Data som hämtas in med hjälp av en batchbaserad källa utvärderas nightly, även om de kvalificerar för direktuppspelningssegmentering. Händelser som direktuppspelas i systemet med en tidsstämpel som är äldre än 24 timmar kommer att bearbetas i det efterföljande batchjobbet.

### Hur definieras segment som grupp- eller direktuppspelningssegmentering?

En segmentdefinition definieras som grupp-, direktuppspelnings- eller kantsegmentering baserat på en kombination av frågetyp och händelsehistorikens varaktighet. En lista över vilka segment som ska utvärderas som en definition av ett direktuppspelat segment finns i avsnittet [frågetyper för direktuppspelningssegmentering](#query-types).

Observera att om en segmentdefinition innehåller **både** och `inSegment` uttryck och en direkt enkel händelsekedja, kan den inte kvalificera för direktuppspelningssegmentering. Om du vill att den här segmentdefinitionen ska vara giltig för direktuppspelningssegmentering, bör du göra den direkta single-event-kedjan till ett eget segment.

### Varför ökar antalet&quot;totalt kvalificerade&quot; segment medan antalet under&quot;Senaste X dagarna&quot; är noll i avsnittet med segmentdefinitionsdetaljer?

Antalet kvalificerade segment baseras på det dagliga segmenteringsjobbet, som omfattar målgrupper som är kvalificerade för både batch- och direktuppspelningssegment. Detta värde visas för både grupp- och direktuppspelningssegment.

Talet under de senaste X dagarna **endast** innehåller målgrupper som är kvalificerade för direktuppspelningssegmentering, och **endast** ökar om du har direktuppspelade data i systemet och det räknas mot den direktuppspelningsdefinitionen. Det här värdet visas **endast** för direktuppspelningssegment. Därför kan det här värdet **** visas som 0 för gruppsegment.

Om du ser att talet under&quot;De senaste X dagarna&quot; är noll och linjediagrammet också visar noll, har du **inte** direktuppspelat några profiler i systemet som skulle kvalificera för det segmentet.

### Hur lång tid tar det innan en segmentdefinition är tillgänglig?

Det tar upp till en timme innan en segmentdefinition är tillgänglig.

### Finns det några begränsningar för de data som strömmas in?

När du använder kanter- eller direktuppspelningssegmentering måste du se till att händelserna för varje profil är utspridda. Om för många händelser direktuppspelas inom samma sekund, kommer Experience Platform att behandla dessa händelser som robotgenererade data och de kommer att ignoreras. Som bästa praxis bör du ha **minst** fem sekunder mellan händelsedata för att säkerställa att data används på rätt sätt.
