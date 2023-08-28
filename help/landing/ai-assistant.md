---
title: AI Assistant för Adobe Experience Platform
description: Lär dig hur du använder AI Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
badge: Alfa
hide: true
hidefromtoc: true
source-git-commit: e84f5aff6885535b58874a4fe02db2944e1d9b7f
workflow-type: tm+mt
source-wordcount: '2622'
ht-degree: 0%

---

# AI Assistant för Adobe Experience Platform

>[!NOTE]
>
>AI Assistant för Adobe Experience Platform finns för närvarande i Alfa. Funktionen och dokumentationen kan komma att ändras.

AI Assistant för Adobe Experience Platform är en gränssnittsfunktion som du kan använda för att navigera och förstå koncept för Experience Platform och Real-time Customer Data Platform samt användningsinformation om dina objekt.

Du kan fråga AI-assistenten efter information som:

* Vägledning om hur man utför uppgifter som rör data och målgrupper.
* Status och mått för befintliga dataobjekt i organisationen.
* Använd exempel och nyanser för att få en bättre förståelse för dataobjekten, inklusive attribut, datauppsättningar, destinationer, scheman, segment och källor.

Det här dokumentet innehåller information om hur du kan få svar på frågor om Experience Platform och Real-Time CDP koncept och hur du kan få tillgång till och använda AI Assistant.

>[!BEGINSHADEBOX]

**Hur fungerar AI-assistenten?**

AI Assistant svarar på dina inskickade frågor genom att fråga en databas och sedan omvandla data från databasen till ett läsbart svar.

Denna interna representation av underliggande data kallas även kunskapsdiagram - ett omfattande nät av koncept, data och metadata för ett givet svar.

Kunskapsdiagrammet består av deldiagram som refereras när frågor skickas:

* Kundanvändningsdata.
* Kundanvändningsdata för olika metabutiker.
* Experience League dokumentation.

Det finns två typer av frågor att tänka på innan du frågar AI-assistenten:

* **Konceptfrågor**: Konceptfrågor handlar om Adobe-koncept som rör data eller målgrupper. Några exempel på konceptfrågor är:
   * Vad är skillnaden mellan gruppsegmentering och direktuppspelningssegmentering?
   * Finns det branschdatamodeller och hur använder jag dem?
   * Vad är Real-Time CDP bäst för?
* **Användningsfrågor**: Användningsfrågor handlar om dataobjekten i organisationen. Några exempel på användningsfrågor är:
   * Hur många datauppsättningar har jag?
   * Hur många schemaattribut har aldrig använts?
   * Vilka segment har aktiverats?

>[!ENDSHADEBOX]

## Åtkomst till AI-assistenten för Experience Platform i användargränssnittet

Du kommer åt AI-assistenten via sidhuvudsnavigeringen i användargränssnittet för Experience Platform.

Välj **[!UICONTROL AI Assistant icon]** i sidhuvudet för att öppna AI-assistentpanelen.

![Experience Platform användargränssnittets hemsida med ikonen AI Assistant vald.](./images/ai-assistant/ai-assistant.png)

Härifrån kan du skriva in din fråga i textrutan och fråga AI-assistenten efter koncept för data eller målgrupper. Du kan också ställa frågor om dataobjekten för att bättre förstå hur du kan använda dem för dina respektive användningsfall.

### Exempel: Använd AI-assistenten för att snabba upp framtagningen av scheman

>[!NOTE]
>
>I följande exempelarbetsflöde används ExperienceEvent-schemaprocessen för att illustrera hur du kan använda AI-assistenten när du använder användargränssnittet i Experience Platform.

Tänk dig ett användningsexempel där du skapar en **Enhetshandel i händelseschema**. När du skapar ExperienceEvent-scheman stöter du på `eventType` fält. Nu kan du antingen lämna arbetsflödet och läsa dokumentationen på [grunderna i en schemakomposition](../xdm/schema/composition.md), eller så kan du använda AI-assistenten för att få svar på dina frågor direkt.

Till att börja med skriver du in din fråga i textrutan. I exemplet nedan ställs frågan: &quot;**Vad är fältet eventType i ett Experience Event-schema?**&quot;

![AI-assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/ai-assistant/question.png)

AI-assistenten frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en stund returnerar AI-assistenten ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

![AI-assistenten för Experience Platform med svar på föregående fråga.](./images/ai-assistant/answer.png)

Du kan lära dig mer om ett visst ämne genom att ställa en uppföljningsfråga. I nästa exempel tillfrågas AI-assistenten om hur eventType kan användas i segmentering.

![En uppföljningsfråga och ett svar visas på AI-assistenten för Experience Platform.](./images/ai-assistant/follow-up-answer.png)

Du kan även ställa frågor till AI Assistant om din dataanvändning. När du frågar om dataanvändning måste du vara i en aktiv sandlåda för att AI-assistenten ska kunna svara på din fråga.

![En fråga om dataanvändning där man frågar hur många segment en användare har.](./images/ai-assistant/data-usage-question.png)

Med varje svar kan AI-assistenten ge dig ett sätt att validera svaret genom att visa dess källa. Länkar till dokumentationen tillhandahålls för konceptfrågor, medan frågor om dataanvändning kan verifieras med en SQL-fråga som visar hur svaret beräknades.

>[!BEGINSHADEBOX]

**Din feedback har begärts**

Under det här alfavärdet får du gärna ge feedback på de svar du får från AI-assistenten. Alla svar och inskickade kommentarer granskas för att fortsätta förbättra AI Assistant-upplevelsen.

Om du vill ge feedback väljer du antingen tummen uppåt eller tummen nedåt när du fått ett svar från AI-assistenten och anger sedan din feedback i textrutan. Nästa, välj **[!UICONTROL Submit feedback]** att skicka in.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB Visa källa]

Välj **[!UICONTROL Show source]** en lista med länkar till den dokumentation som AI-assistenten refererar till för att beräkna sitt svar.

![Länkarna till källan som visas i AI-assistenten.](./images/ai-assistant/show-sources.png)

>[!TAB Tummen upp]

Välj ikonen med tummen uppåt för att ge feedback på vad som gick bra med din upplevelse av AI-assistenten.

![Fönstret för positiv feedback.](./images/ai-assistant/positive-feedback.png)

>[!TAB Tummen ned]

Välj ikonen med reglaget nedåt för att ge feedback på vad som kan förbättras baserat på din erfarenhet av AI Assistant. Under det här steget kan du även ge specifika kommentarer om din upplevelse. Synpunkter i kommentarerna granskas dagligen.

![Fönstret för negativ feedback.](./images/ai-assistant/negative-feedback.png)

>[!TAB Flagga]

Välj flaggikonen om du vill visa fler rapporter om din upplevelse med hjälp av AI-assistenten.

![Rapportresultatfönstret.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### Ideas för att komma igång

Du kan också använda de förinställda uppmaningar som AI Assistant ger för att komma igång.

![De instruktioner som visas på AI-assistentpanelen.](./images/ai-assistant/ideas.png)

## Ytterligare information

Mer information om AI-assistenten för Experience Platform finns i det här avsnittet.

### Omfång

AI-assistenten kan besvara frågor baserat på dokumentationen och din dataanvändning.

#### Dokumentation

Du kan ställa dokumentationsfrågor baserat på Real-time Customer Data Platform och Publiker. Dokumentationsindexet täcker för närvarande Adobe Experience Platform (Real-Time CDP och Publiker). Indexet uppdateras regelbundet.

Modellen för dokumentationsåterhämtning har utbildats i Experience Platform (Real-Time CDP och Publiker). Frågor som inte omfattas av Adobe Experience Platform, t.ex. frågor om andra Adobe-produkter som Adobe Target och Creative Cloud Suite, kan inte besvaras.

#### Dataanvändning

Du kan även ställa frågor till AI Assistant om din dataanvändning i följande domäner:

* Attribut
* Datauppsättningar
* Mål 
* Scheman
* Segment
* Källor

För användningsdatafrågor kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som ligger till grund för dessa frågor uppdateras var 12 till 24:e timme. Du kan behöva formatera dina frågor som:&quot;När var segmentet med titeln? {TITLE} skapad?&quot; istället för: &quot;När var {TITLE} segmentet skapades?&quot;

Du måste logga in i en sandlåda för att få frågor om specifika data som rör objekt som scheman, datamängder, attribut, mål och segment.

+++Välj för en lista över frågor om dataanvändning som stöds

Nedan följer en lista över aktuella frågor om dataanvändning som stöds, grupperade efter domän.

>[!BEGINTABS]

>[!TAB Segment]

* Finns det duplicerade segment?
* Visa alla strömningssegment.
* Är segment namngivna {SEGMENT_ID} utvärderat i batch- eller direktuppspelning?
* Vilka segment är dubbletter?
* Hur många segment finns det totalt?
* Finns det några segment med samma namn men olika ID:n?
* Vilken är fördelningen av utvärderingsmetoder (batch, edge, streaming) mellan segment?
* Visa en lista över segment som senast ändrades under den senaste månaden.
* Vilka segment har ändrats den senaste veckan?
* Finns det några segment som inte har ändrats de senaste sex månaderna?
* Lista segment som skapades det senaste året.
* Visa segment som senast ändrades idag.
* Finns det några mönster eller trender för när man ska skapa segment under det senaste året?
* Kan du identifiera segment som inte har ändrats sedan de skapades?
* Finns det några segment som inte har ändrats sedan de skapades?
* Hur ser trenden ut när det gäller att skapa segment?
* Vilken är fördelningen av datum när segmentet skapades?
* Vilken är fördelningen av ändringsdatum för segment?
* Vilka segment har mest användarprofiler?
* Vilka segment har minst användarprofiler?
* Visa alla gruppsegment.
* Visa alla kantsegment.
* Vilka segment aktiveras?
* Vilka segment vidarebefordras till Facebook?
* Är segmentet&quot;APAC-kunder&quot; batch eller direktuppspelning?
* Hur många profiler har Active Work-segmentet?
* Har något av mina segment 0 profiler?
* Vilka datauppsättningar påverkar Bronze loyalty-segmentet?
* Vilka segmentdefinitioner använder XDM-fält som innehåller &quot;kön&quot;?
* Vilka ifyllda XDM-fält finns i strömningssegment?
* Hur många XDM-fält finns det för alla segmentdefinitioner?
* Vilka segment påverkar datauppsättningen&quot;Professional Users&quot;?
* Vilka segment vidarebefordras till HTTP API?
* Av de segment som är aktiverade, som är aktiverade till det största antalet måltyper?
* Vad är det totala antalet aktiverade segment?
* Hur många segment aktiveras?
* Hur många duplicerade segment aktiveras?
* Hur många segment aktiveras för varje mål?
* Vilka segment aktiveras för 0, 1 eller flera destinationer? Visa fördelningen.
* Vilka segment aktiveras för det största antalet destinationer?
* Vilka duplicerade segment är aktiverade?
* Vilka segment aktiveras för Adobe Target?
* Hur många gånger används varje sammanfogningsprincip i alla segment?

>[!TAB Scheman]

* Hur många XDM-scheman har definierats?
* Vilka är de senast skapade scheman?
* Hur många scheman för varje XDM-klass?
* Vilket schema använder datauppsättningen&quot;Segmentinmatning&quot;?
* Vilka scheman används inte av några datauppsättningar?

>[!TAB Mål ]

* Hur många destinationer finns det?
* Vilka är de senast skapade destinationerna?
* Vilka mål är associerade med varje segment?

>[!TAB Källor]

* Hur många källor har skapats?
* Vilka är de senast skapade källorna?
* Hur många källor finns tillgängliga, uppdelade efter kategori?
* Kan jag skapa en källanslutning från S3?
* Vilka källor bidrog till datauppsättningen Mutual365?

>[!TAB Datauppsättningar]

* Hur många datauppsättningar finns det?
* Vilka är de senast skapade datauppsättningarna?
* Vilka datauppsättningar är aktiverade för den enhetliga profilen?
* Finns det en TTL-uppsättning för segmentinmatningsdatauppsättningen?
* Vad är TTL-värdet för Professional-användardatauppsättningen?
* Vilka datauppsättningar använder Professional Users-schemat?

>[!TAB Attribut]

* Vilka XDM-fält är oftast ifyllda i alla DataSets?
* Vilka XDM-fält och -attribut används oftast i olika scheman?
* Vilka XDM-fält och attribut används i Professional Users-schemat?
* Lista de attribut som används för det här segmentet med ID {SEGMENT_ID}.
* Hur många XDM-fält används i 2+ segment?
* Vilka fält används oftast i olika segment?
* Finns det fält som bara används i ett segment?
* Vilka attribut används för Bronze-segmentet?
* Vilka attribut används inte i något segment?
* Vilka attribut används oftast i segment?

>[!ENDTABS]

+++

### Konversationsupplevelser

Du måste ta hänsyn till flera nyanser i konversationsupplevelsen när du frågar AI-assistenten.

>[!NOTE]
>
>Dessa begränsningar är tillfälliga och förbättras under hela alfavärdet.

>[!BEGINTABS]

>[!TAB Det går inte att härleda kontext från föregående diskussion]

AI-assistenten kan för närvarande inte referera till tidigare diskussioner som kontext för en given fråga. Se tabellen nedan för exempel:

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Finns det olika typer av sådana?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Uppföljningsfråga:&quot;Finns det olika typer av **segment**?&quot;</li></ul> | AI-assistenten kan inte sluta sig till vad &quot;de&quot; betyder. |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du utveckla mer?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Fråga:&quot;Förklara vad ett segment är i detalj&quot;</li></ul> | AI Assistant kan inte referera till dokumentation som baseras på &quot;mer&quot; på ett intelligent sätt. |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du ge mig ett exempel på en sådan?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du ge mig ett exempel på ett segment?&quot;</li></ul> | AI-assistenten kan inte sluta sig till vad du vill ha ett exempel på. |
| <ul><li>Första frågan:&quot;Vad är ett gruppsegment?&quot;</li><li>Följa frågan:&quot;Hur fungerar det jämfört med ett direktuppspelningssegment?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett gruppsegment?&quot;</li><li>Följ upp frågan:&quot;Kan du jämföra ett direktuppspelningssegment med ett gruppsegment?&quot;</li></ul> | AI-assistenten kan inte sluta sig till vad &quot;den&quot; hänvisar till och kan därför inte jämföra direktuppspelningssegmentet. |
| <ul><li>Första frågan:&quot;Hur många segment har jag?&quot;</li><li>Fråga:&quot;Hur många av dem använder Facebook som mål?&quot;</li></ul> | <ul><li>Första frågan:&quot;Hur många segment har jag?&quot;</li><li>Fråga:&quot;Hur många av de segment jag har använder Facebook som mål?&quot;</li></ul> | AI-assistenten kan inte sluta sig till vad &quot;de&quot; syftar på. |

{style="table-layout:auto"}

>[!TAB Det går inte att härleda kontext från en sida]

När du frågar AI-assistenten om ett visst element på Experience Platform-användargränssnittssidan som du är på, måste du tydligt definiera det specifika elementet i din fråga.

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| &quot;Vad gör det här?&quot; | &quot;Vad gör {PAGE_NAME} eller hur? | AI-assistenten kan inte sluta sig till vad &quot;detta&quot; syftar på. Du måste ange det specifika sidelementet som du frågar om. |
| &quot;Varför sparar det inte?&quot; | &quot;Varför kan jag inte spara en ny sandlåda med namnet {NAME}?&quot; | AI-assistenten kan inte sluta sig till vad &quot;den&quot; syftar på och kan inte veta att du har problem med en enhet. |

{style="table-layout:auto"}

Dessutom kan AI-assistenten bara besvara frågor om felmeddelanden, eftersom felet är dokumenterat i Experience League.

>[!TAB Tvetydighet]

Du måste formulera dina frågor tydligt och definiera dem i en produkt, ett program eller en domän, eftersom AI Assistant för närvarande inte kan tolka frågor.

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| &quot;Hur skapar jag ett filter? | Hur skapar jag ett filter i Profilfrågespråk? | Du måste ange den funktion som du filtrerar efter eftersom en mängd olika Experience Platform-funktioner stöder filtrering. |
| &quot;Hur kommer jag igång? | Hur kommer jag igång med att använda destinationer? | Du måste ge en tydlig bild av dina mål och användningsfall eftersom alltför breda koncept kan resultera i generiska eller onödigt specifika svar. |

{style="table-layout:auto"}

>[!ENDTABS]

### Begränsat litet snack

Du kan använda AI Assistant i små samtal, men den här kapaciteten är för närvarande begränsad.

### Funktionsfrågor

AI-assistenten kan ge ett felaktigt intryck av vad den kan göra. Följande typer av frågor kan besvaras felaktigt:

| Exempelfråga | Anteckning |
| --- | --- |
| &quot;Kan du svara på frågor om {ENTITY}?&quot; | Så länge AI-assistenten kan hitta en sida som refererar till en viss enhet i sitt index, kommer den att svara ja. |
| &quot;Vet ni **x** språk?&quot; | AI-assistenten har för närvarande bara stöd för engelska, men kan svara&quot;ja&quot; på grund av att den underliggande modellen kan stödja den. |
| &quot;Kan du göra..?&quot; | AI-assistenten kan svara ja, även om den inte kan det. |

### Tips

#### Frågor kan besvaras med fel informationskälla

Det finns tillfällen när din fråga om dina användningsdata kan resultera i ett svar baserat på dokumentationen. Detta beror på att AI-assistenten felaktigt kan dirigera din fråga till fel informationskälla. Du kan förhindra detta genom att:

* Reparera frågan för att använda mer SQL-liknande språk
* Uttryckligen anropa informationskällan som ska användas.

Se tabellen nedan för exempel:

| Felaktig fråga | Bra fråga | Anteckningar |
| --- | --- | --- |
| Vad är mitt största segment? | Vad är mitt största segment? Använda data. | Tala uttryckligen om för AI-assistenten att du vill att svaret ska baseras på data. |
| Vad är mitt största segment? | Lista mitt största segment. | Det finns tillfällen då en fråga om vad.. kan bli fel för en dokumentationsbaserad fråga. Att använda ett kommando som &quot;list&quot; är en starkare indikator på att du ställer en fråga med data i sitt sammanhang. |
| Hur många datauppsättningar har jag? | Räkna mina datauppsättningar. | Den ursprungliga frågan fungerar för segment, men fungerar kanske inte med datauppsättningar. |
