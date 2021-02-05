---
keywords: Experience Platform;hem;populära ämnen;schema;schema;enum;primär identitet;primär identitet;enskild XDM-profil;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM ExperienceEvent;schema design;best practices
solution: Experience Platform
title: Bästa praxis för datamodellering
topic: overview
description: Detta dokument innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 1%

---


# Bästa tillvägagångssätt för datamodellering

[!DNL Experience Data Model] (XDM) är det centrala ramverket som standardiserar kundupplevelsedata genom att tillhandahålla gemensamma strukturer och definitioner för användning i Adobe Experience Platform-tjänster längre fram i kedjan. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som gör att ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

Eftersom XDM är extremt mångsidigt och anpassningsbart efter design är det därför viktigt att följa bästa praxis för datamodellering när du utformar dina scheman. Det här dokumentet beskriver de viktigaste beslut och överväganden du måste ta när du mappar kundupplevelsedata till XDM.

## Komma igång

Innan du läser den här guiden bör du läsa igenom [XDM System overview](../home.md) för att få en introduktion till XDM på hög nivå och dess roll i Experience Platform.

Den här guiden fokuserar dessutom enbart på viktiga aspekter när det gäller schemadesign. Vi rekommenderar därför starkt att du hänvisar till [grunderna för schemakomposition](./composition.md) för detaljerade förklaringar av de enskilda schemaelementen som omnämns i den här guiden.

## Sammanfattning av bästa praxis

Den rekommenderade metoden för att utforma din datamodell för användning i Experience Platform kan sammanfattas på följande sätt:

1. Förstå användningsexemplen för era data.
1. Identifiera de primära datakällor som ska hämtas till [!DNL Platform] för att hantera dessa användningsfall.
1. Identifiera eventuella sekundära datakällor som också kan vara av intresse. Om till exempel bara en affärsenhet i organisationen för närvarande är intresserad av att portera sina data till [!DNL Platform], kan en liknande affärsenhet också vara intresserad av att portera liknande data i framtiden. Med dessa sekundära källor blir datamodellen standardiserad i hela organisationen.
1. Skapa ett högnivådiagram över entitetsrelationer (ERD) för de datakällor som har identifierats.
1. Konvertera högnivåundervisningen till ett [!DNL Platform]-centrerat undervisningsavsnitt (inklusive profiler, Experience Events och sökentiteter).

Stegen för att identifiera de datakällor som krävs för att du ska kunna använda ditt företag varierar från organisation till organisation. Medan resten av avsnitten i detta dokument fokuserar på de senare stegen för att organisera och konstruera en ERD efter att datakällorna har identifierats, kan förklaringarna av diagrammets olika komponenter ge dig underlag för dina beslut om vilken av datakällorna som ska migreras till [!DNL Platform].

## Skapa en högnivå av ERD

När du har bestämt vilka datakällor du vill hämta till [!DNL Platform] kan du skapa en högnivå av ERD som hjälp vid mappningen av dina data till XDM-scheman.

Exemplet nedan representerar en förenklad ERD för ett företag som vill hämta data till [!DNL Platform]. Bilden visar de viktigaste enheterna som bör sorteras i XDM-klasser, inklusive kundkonton, hotell, adresser och flera vanliga e-handelshändelser.

![](../images/best-practices/erd.png)

## Sortera entiteter i profil-, uppslags- och händelsekategorier

När du har skapat en ERD för att identifiera de enheter som du vill hämta till [!DNL Platform] måste dessa enheter sorteras i profil-, uppslags- och händelsekategorier:

| Kategori | Beskrivning |
| --- | --- |
| Profilenheter | Profilenheter representerar attribut som relaterar till en enskild person, vanligtvis en kund. Enheter som tillhör den här kategorin ska representeras av scheman baserade på klassen **[!DNL XDM Individual Profile]**. |
| Sök enheter | Sökentiteter representerar begrepp som kan relatera till en enskild person, men som inte kan användas direkt för att identifiera den enskilda personen. Enheter som tillhör den här kategorin ska representeras av scheman baserade på **anpassade klasser**. |
| Händelseentiteter | Händelseenheter representerar koncept som relaterar till åtgärder som en kund kan vidta, systemhändelser eller andra koncept där du kan vilja spåra ändringar över tid. Enheter som tillhör den här kategorin ska representeras av scheman baserade på klassen **[!DNL XDM ExperienceEvent]**. |

### Överväganden för entitetssortering

Avsnitten nedan ger ytterligare vägledning om hur du sorterar dina enheter i ovanstående kategorier.

#### Kundattribut

Om ett företag innehåller attribut som är kopplade till en enskild kund är det troligast en profilenhet. Exempel på kundattribut är:

* Personuppgifter som namn, födelsedatum, kön och konto-ID.
* Platsinformation som adresser och GPS-information.
* Kontaktinformation som telefonnummer och e-postadresser.

#### Spåra data över tid

Om du vill analysera hur vissa attribut inom en enhet ändras över tid är det troligast en händelsenhet. Om du till exempel lägger till produktartiklar i en kundvagn kan du spåra dem som tilläggshändelser i [!DNL Platform]:

| Kund-ID | Typ | Produkt-ID | Kvantitet | Tidsstämpel |
| --- | --- | --- | --- | --- |
| 1234567 | Lägg till | 275098 | 2 | 1 okt 10:32 |
| 1234567 | Ta bort | 275098 | 1 | 1 okt 10:33 |
| 1234567 | Lägg till | 486502 | 1 | 1 okt 10:41 |
| 1234567 | Lägg till | 910482 | 5 | 3 okt 2:15 PM |

#### Användningsexempel för segmentering

När ni kategoriserar era enheter är det viktigt att tänka på de målgruppssegment ni kanske vill bygga för att hantera era specifika affärsanvändningsfall.

Ett företag vill t.ex. känna till alla &quot;Guld&quot; eller &quot;Platinum&quot;-medlemmar i deras lojalitetsprogram som har gjort fler än fem inköp det senaste året. På grundval av denna segmentlogik kan följande slutsatser dras om hur relevanta enheter bör representeras:

* &quot;Gold&quot; och &quot;Platinum&quot; representerar lojalitetsstatus som gäller för en enskild kund. Eftersom segmentlogiken endast gäller kundernas aktuella lojalitetsstatus, kan dessa data modelleras som en del av ett profilschema. Om du vill spåra förändringar i lojalitetsstatus över tiden kan du även skapa ett ytterligare händelseschema för förändringar av lojalitetsstatusen.
* Inköp är händelser som inträffar vid en viss tidpunkt och segmentlogiken gäller köphändelser inom ett angivet tidsfönster. Dessa data bör därför modelleras som ett händelseschema.

#### Användningsexempel vid aktivering

Förutom att ta hänsyn till användningsfall för segmentering bör du också granska användningsexemplen för aktivering för dessa segment för att identifiera ytterligare relevanta attribut.

Ett företag har till exempel skapat ett målgruppssegment baserat på regeln `country = US`. När segmentet sedan aktiveras för vissa efterföljande mål vill företaget filtrera alla exporterade profiler baserat på hemstatus. Därför bör ett `state`-attribut också hämtas i den tillämpliga profilentiteten.

#### Sammanställda värden

Baserat på användningsfallet och detaljrikedomen i era data bör ni bestämma om vissa värden behöver föraggregeras innan de inkluderas i en profil eller en händelseenhet.

Ett företag vill till exempel skapa ett segment baserat på antalet kundvagnsköp. Du kan välja att inkludera dessa data med lägsta granularitet genom att ta med varje tidsstämplad inköpshändelse som sin egen enhet. Detta kan ibland öka antalet registrerade händelser exponentiellt. Om du vill minska antalet inkapslade händelser kan du välja att skapa ett aggregerat värde `numberOfPurchases` under en vecklong- eller månadsperiod. Andra sammanställningsfunktioner som MIN och MAX kan också användas i dessa situationer.

>[!CAUTION]
>
>Experience Platform utför för närvarande inte automatisk värdeaggregering, även om detta planeras för framtida releaser. Om du väljer att använda aggregerade värden måste du utföra beräkningarna externt innan du skickar data till [!DNL Platform].

#### Kardinalitet

Kardinalerna i ERD kan även ge vissa ledtrådar om hur ni kategoriserar era era enheter. Om det finns en en-till-många-relation mellan två enheter kommer den enhet som representerar&quot;många&quot; sannolikt att vara en händelseenhet. Det finns dock även fall där&quot;många&quot; är en uppsättning uppslagsenheter som anges som en array i en profilentitet.

>[!NOTE]
>
>Eftersom det inte finns någon universell strategi för att passa in alla användningsfall är det viktigt att tänka på fördelarna och nackdelarna med varje situation när enheter kategoriseras baserat på kardinalitet. Mer information finns i [nästa avsnitt](#pros-and-cons).

I följande tabell visas några vanliga entitetsrelationer och de kategorier som kan härledas från dem:

| Relation | Kardinalitet | Enhetskategorier |
| --- | --- | --- |
| Kunder- och kundvagnscheckout | En till många | En enskild kund kan ha många kassor, vilket är händelser som kan spåras över tiden. Kunderna skulle därför vara en profilenhet, medan kundvagnsutcheckningar skulle vara en händelseenhet. |
| Kunder- och förmånskonton | En till en | En enskild kund kan bara ha ett förmånskonto, och vice versa. Eftersom relationen är en-till-en representerar både kunder och lojalitetskonton profilentiteter. |
| Kunder och prenumerationer | En till många | En enskild kund kan ha många prenumerationer. Eftersom företaget bara är berört med en kunds aktuella prenumerationer är kunderna en profilenhet, medan prenumerationer är en sökenhet. |

### Fördelar och koner för olika enhetsklasser {#pros-and-cons}

I föregående avsnitt fanns allmänna riktlinjer för hur du ska kategorisera dina enheter, men det är viktigt att du förstår att det ofta kan finnas fördelar och nackdelar för att välja en enhetskategori framför en annan. Följande fallstudie är avsedd att illustrera hur du kan överväga dina alternativ i dessa situationer.

Ett företag håller reda på aktiva prenumerationer för sina kunder, där en kund kan ha många prenumerationer. Företaget vill också inkludera prenumerationer för segmenteringsanvändning, som att hitta alla användare med aktiva prenumerationer.

I det här scenariot har företaget två möjliga alternativ för att representera en kunds prenumerationer i sin datamodell:

1. [Använd profilattribut](#profile-approach)
1. [Använd händelseentiteter](#event-approach)

#### Metod 1: Använd profilattribut {#profile-approach}

Det första sättet är att inkludera en array med prenumerationer som attribut i profilentiteten för kunder. Objekt i den här arrayen skulle innehålla fält för `category`, `status`, `planName`, `startDate` och `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Proffs**

* Segmentering är möjligt för det avsedda användningsfallet.
* Schemat bevarar bara de senaste prenumerationsposterna för en kund.

**Kon**

* Hela arrayen måste anges om varje gång ett fält i arrayen ändras.
* Om olika datakällor eller affärsenheter matar in data i arrayen blir det en utmaning att synkronisera den senaste uppdaterade arrayen över alla kanaler.

#### Metod 2: Använd händelseentiteter {#event-approach}

Det andra sättet är att använda händelsescheman för att representera prenumerationer. Detta innebär att man måste importera samma prenumerationsfält som det första tillvägagångssättet, med tillägg av ett prenumerations-ID, ett kund-ID och en tidsstämpel för när prenumerationshändelsen inträffade.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Proffs**

* Segmenteringsreglerna kan vara mer flexibla (t.ex. att hitta alla kunder som har ändrat sina prenumerationer de senaste 30 dagarna).
* När en kunds prenumerationsstatus ändras behöver du inte längre uppdatera en lång, potentiellt komplex array inom kundens profilattribut. Detta är särskilt användbart om kundens prenumerationslista ändras samtidigt från flera källor.

**Kon**

* Segmenteringen blir mer komplicerad för det ursprungliga användningsfallet (som identifierar statusen för kundens senaste prenumerationer). Segmentet behöver nu ytterligare logik för att flagga den senaste prenumerationshändelsen för en kund för att kunna kontrollera dess status.

## Skapa scheman baserat på dina kategoriserade entiteter

När du har sorterat dina enheter i profil-, uppslags- och händelsekategorier kan du börja konvertera din datamodell till XDM-scheman. I demonstrationssyfte har exempeldatamodellen som visades tidigare sorterats i lämpliga kategorier i följande diagram:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

Kategorin som en entitet har sorterats under bör avgöra vilken XDM-klass du baserar dess schema på. Så här upprepar du:

* Profilentiteter bör använda klassen [!DNL XDM Individual Profile].
* Händelseentiteter bör använda klassen [!DNL XDM ExperienceEvent].
* Sökentiteter bör använda anpassade XDM-klasser som definieras av organisationen.

>[!NOTE]
>
>Händelseentiteter representeras nästan alltid av separata scheman, men entiteter i profilen eller uppslagskategorierna kan kombineras i ett enda XDM-schema, beroende på deras kardinalitet.
>
>Eftersom kundentiteten till exempel har en 1:1-relation med LoyaltyAccounts-entiteten, kan schemat för kundentiteten även innehålla ett `LoyaltyAccount`-objekt som innehåller rätt lojalitetsfält för varje kund. Om relationen är en till många kan den entitet som representerar&quot;många&quot; däremot representeras av ett separat schema eller en array med profilattribut, beroende på hur komplex den är.

Avsnitten nedan innehåller allmän vägledning om hur du konstruerar scheman baserade på din ERD.

### Anta en iterativ modelleringsmetod

[Reglerna för schemautveckling](./composition.md#evolution) anger att endast icke-förstörande ändringar kan göras i scheman när de har implementerats. När du har lagt till ett fält i ett schema och data har importerats till det fältet kan fältet alltså inte längre tas bort. Därför är det viktigt att du använder en iterativ modelleringsmetod när du först skapar dina scheman, och börjar med en förenklad implementering som successivt blir mer komplicerad över tiden.

Om du är osäker på om ett visst fält är nödvändigt för att inkluderas i ett schema är det bästa sättet att utelämna det. Om det senare fastställs att fältet är nödvändigt kan det alltid läggas till i nästa iteration i schemat.

### Identitetsfält

I Experience Platform används XDM-fält som markerats som identiteter för att sammanfoga information om enskilda kunder som kommer från flera datakällor. Även om ett schema kan ha flera fält markerade som identiteter måste en enda primär identitet definieras för att schemat ska kunna aktiveras för användning i [!DNL Real-time Customer Profile]. Mer information om hur dessa fält används finns i avsnittet [identitetsfält](./composition.md#identity) i grunderna för schemakomposition.

När du utformar dina scheman kommer eventuella primärnycklar i relationsdatabastabeller troligtvis att vara lämpliga för primära identiteter. Andra exempel på tillämpliga identitetsfält är kundens e-postadresser, telefonnummer, konto-ID:n och [ECID](../../identity-service/ecid.md).

### programblandningar från Adobe

Experience Platform har flera färdiga XDM-mixiner för datainhämtning i samband med följande Adobe-program:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Med [[!UICONTROL Adobe Analytics ExperienceEvent Template Mixin]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) kan du till exempel mappa [!DNL Analytics]-specifika fält till XDM-scheman. Beroende på vilka Adobe-program du arbetar med bör du använda dessa Adobe-anpassade mixiner i dina scheman.

<img src="../images/best-practices/analytics-mixin.png" width="700"><br>

Adobe-programblandningar tilldelar automatiskt en primär standardidentitet genom att använda fältet `identityMap`, som är ett systemgenererat, skrivskyddat objekt som mappar standardvärden för identiteter för en enskild kund.

För Adobe Analytics är ECID standardidentitet. Om ett ECID-värde inte anges av en kund blir den primära identiteten i stället AAID som standard.

>[!IMPORTANT]
>
>När du använder programblandningar från Adobe ska inga andra fält markeras som primär identitet. Om det finns ytterligare egenskaper som måste markeras som identiteter måste de här fälten tilldelas som sekundära identiteter i stället.

## Nästa steg

Det här dokumentet innehåller allmänna riktlinjer och bästa praxis för utformning av din datamodell för Experience Platform. Sammanfattning:

* Använd en uppifrån och ned-metod genom att sortera dina datatabeller i profil-, uppslags- och händelsekategorier innan du skapar dina scheman.
* Det finns ofta flera strategier och alternativ när det gäller att utforma scheman för olika syften.
* Datamodellen bör stödja era affärsanvändningsfall, som segmentering eller kundreseanalys.
* Gör dina scheman så enkla som möjligt och lägg bara till nya fält när det är absolut nödvändigt.

När du är klar kan du gå till självstudiekursen om att [skapa ett schema i användargränssnittet](../tutorials/create-schema-ui.md) för steg-instruktioner om hur du skapar ett schema, tilldelar lämplig klass för entiteten och lägger till fält som data ska mappas till.