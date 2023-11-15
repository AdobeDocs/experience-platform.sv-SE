---
title: Assistent för Adobe Experience Platform
description: Lär dig hur du använder Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
badge: Alfa
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: e204e1cc70f0c87632f7d259194d34276f6fab72
workflow-type: tm+mt
source-wordcount: '2563'
ht-degree: 0%

---

# Assistent för Adobe Experience Platform

>[!NOTE]
>
>Assistenten för Adobe Experience Platform är för närvarande i Alpha. Funktionen och dokumentationen kan komma att ändras.

Assistenten för Adobe Experience Platform är en gränssnittsfunktion som du kan använda för att navigera och förstå koncept för Experience Platform och Real-time Customer Data Platform samt för att få information om hur du använder dina objekt.

Du kan fråga Assistant om du vill ha information om:

* Vägledning om hur man utför uppgifter som rör data och målgrupper.
* Status och mått för befintliga dataobjekt i organisationen.
* Använd exempel och nyanser för att få en bättre förståelse för dataobjekten, inklusive attribut, datauppsättningar, destinationer, scheman, segment och källor.

Det här dokumentet innehåller information om hur du kan få svar på frågor och koncept från Experience Platform och Real-Time CDP med Assistant.

>[!BEGINSHADEBOX]

**Hur fungerar Assistant?**

Assistenten svarar på dina inskickade frågor genom att fråga en databas och sedan omvandla data från databasen till ett läsbart svar.

Denna interna representation av underliggande data kallas även kunskapsdiagram - ett omfattande nät av koncept, data och metadata för ett givet svar.

Kunskapsdiagrammet består av deldiagram som refereras när frågor skickas:

* Kundanvändningsdata.
* Kundanvändningsdata för olika metabutiker.
* Experience League dokumentation.

Det finns två frågeklasser att tänka på innan du frågar assistenten:

* **Konceptfrågor**: Konceptfrågor handlar om Adobe-koncept som rör data eller målgrupper. Några exempel på konceptfrågor är:
   * Vad är skillnaden mellan gruppsegmentering och direktuppspelningssegmentering?
   * Finns det branschdatamodeller och hur använder jag dem?
   * Vad är Real-Time CDP bäst för?
* **Användningsfrågor**: Användningsfrågor handlar om dataobjekten i organisationen. Några exempel på användningsfrågor är:
   * Hur många datauppsättningar har jag?
   * Hur många schemaattribut har aldrig använts?
   * Vilka segment har aktiverats?

>[!ENDSHADEBOX]

## Åtkomstassistenten för Experience Platform i användargränssnittet

Du kommer åt Assistant via sidhuvudsnavigeringen i användargränssnittet för Experience Platform.

Välj **[!UICONTROL Assistant icon]** från sidhuvudet till startpanelen.

![Experience Platform användargränssnittets hemsida med assistentikonen vald.](./images/ai-assistant/ai-assistant.png)

<!-- +++Use immersive mode

To use [!DNL Immersive mode] select the focus icon in the header navigation of the Assistant.

![select-immersive](./images/ai-assistant/select-immersive.png)

A dedicated pop-up interface for Assistant appears at the center of your screen.

![immersive-mode](./images/ai-assistant/immersive-mode.png)

+++

From here, you can input your question in the text box and query Assistant for concepts regarding data or audiences. You can also ask questions about your data objects to better understand how you can use them for your respective use case.  -->

### Exempel: Använd Assistant för att snabba upp skapandet av schemat

>[!NOTE]
>
>I följande exempelarbetsflöde används ExperienceEvent-schemaprocessen för att illustrera hur du kan använda Assistant när du använder användargränssnittet i Experience Platform.

Tänk dig ett användningsexempel där du skapar en **Enhetshandel i händelseschema**. När du skapar ExperienceEvent-scheman stöter du på `eventType` fält. Nu kan du antingen lämna arbetsflödet och läsa dokumentationen på [grunderna i en schemakomposition](../xdm/schema/composition.md)eller så kan du använda Assistant för att få svar på dina frågor direkt.

Börja med att ange din fråga i textrutan. I exemplet nedan ställs frågan: &quot;**Vad är fältet eventType i ett ExperienceEvent-schema?**&quot;

![Assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/ai-assistant/question.png)

Assistenten frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en liten stund returnerar assistenten ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

Ett givet svar ger hyperlänkar till alla refererade entiteter. Välj i exemplet nedan **[!UICONTROL Schemas]** för att visa en lista över de refererade scheman, eller **[!UICONTROL Segments]** om du vill visa en lista över de refererade segmenten.

![Assistent för Experience Platform med svar på föregående fråga.](./images/ai-assistant/answer.png)

Assistenten ger dig ett sätt att validera svaret genom att visa dess källa. Länkar till dokumentationen tillhandahålls för konceptfrågor, medan frågor om dataanvändning kan verifieras med en SQL-fråga som visar hur svaret beräknades.

![Alternativ som tillhandahålls av assistenten efter att ett svar har returnerats.](./images/ai-assistant/options.png)

#### Uppföljningsfråga

+++Välj för att visa ett exempel på en uppföljningsfråga

Du kan lära dig mer om ett visst ämne genom att ställa en uppföljningsfråga. I nästa exempel tillfrågas assistenten om hur eventType kan användas i segmentering.

![En uppföljningsfråga och ett svar som visas på assistenten för Experience Platform.](./images/ai-assistant/follow-up-question.png)

+++

#### Dataanvändningsfråga

+++Välj för att visa ett exempel på en fråga om dataanvändning

Du kan även ställa frågor till assistenten om din dataanvändning. När du frågar om dataanvändning måste du vara i en aktiv sandlåda för att assistenten ska kunna svara på din fråga.

För svar som innehåller information om dataanvändning tillhandahåller Assistant länkar till de berörda enheterna. Assistenten ger dig dessutom en förklaring av hur svaret beräknades.

![En fråga om dataanvändning där man frågar hur många segment en användare har.](./images/ai-assistant/data-usage-question.png)

+++

#### Använd automatisk komplettering

+++Markera för att visa ett exempel på automatisk komplettering

Du kan använda funktionen för automatisk komplettering för att ta emot en lista med dataobjekt som finns i din sandlåda. Det finns rekommendationer för att slutföra automatiskt för följande domäner: segment, scheman, datauppsättningar, källor och mål.

Om du vill använda Fyll i automatiskt anger du ett plustecken (**`+`**) som en del av din fråga. Du kan också välja plustecknet (**`+`**) i textrutan. Sedan visas ett fönster med en lista över rekommenderade dataobjekt som finns i sandlådan.

![](./images/ai-assistant/autocomplete-options.png)

Sedan markerar du det dataobjekt som du vill fråga för att slutföra din fråga och skickar sedan din fråga.

![](./images/ai-assistant/autocomplete-question.png)

+++

## Omfång

Assistenten kan svara på frågor om Real-Time CDP och Experience Platform, liksom om din användarkontos dataanvändning. Assistenten kan även härleda kontext baserat på den gränssnittssida som du befinner dig i. Den kan identifiera

* Användarkontot som du använder.
* Organisationen som du tillhör.
* Sidan som du visar på skärmen.
* Resursen (inklusive typ och ID) som du visar på skärmen.
* Med tanke på att du arbetar med ett visst arbetsflöde i Experience Platform eller Real-Time CDP kan Assistant ta reda på vad du tänker.

### Dokumentation

Dokumentationsindexet täcker för närvarande Adobe Experience Platform (Real-Time CDP och Publiker). Indexet uppdateras regelbundet.

Modellen för dokumentationsåterhämtning har utbildats i Experience Platform (Real-Time CDP och Publiker). Frågor som inte omfattas av Adobe Experience Platform, t.ex. frågor om andra Adobe-produkter som Adobe Target och Creative Cloud Suite, kan inte besvaras.

### Dataanvändning

Du kan även ställa frågor till assistenten om din dataanvändning i följande domäner:

* Attribut
* Datauppsättningar
* Destinationer _(Frågor om konton och vissa frågor om dataflöde kan inte besvaras just nu.)_
* Scheman _(Frågor om fältgrupper kan inte besvaras just nu.)_
* Segment
* Källor _(Frågor om konton kan inte besvaras just nu.)_

För användningsdatafrågor kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som ligger till grund för dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Du kan behöva formatera dina frågor som:&quot;När var segmentet med titeln? {TITLE} skapad?&quot; istället för: &quot;När var {TITLE} segmentet skapades?&quot;

Du måste logga in i en sandlåda för att få frågor om specifika data som rör objekt som scheman, datamängder, attribut, mål och segment.

### Exempel på frågor om dataanvändning

+++Välj för att visa en lista med exempelfrågor om dataanvändning

| Frågetyp | Beskrivning | Exempel |
| --- | --- | --- | 
| Datalinje | Spåra användningen av ett eller flera objekt över andra Experience Platform-objekt | <ul><li>Vilka datauppsättningar som används {SCHEMA_NAME} schema?</li><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilka datauppsättningar har använts i aktiverade segment?</li><li>Lista de scheman som har attribut som används i aktiverade segment.</li><li>Visa de segment som aktiveras för {DESTINATION_ACCOUNT_NAME} och har fler än 1 000 profiler.</li><li>Visa de attribut som används i aktiverade segment som har ändrats efter januari 2023.</li><li>Visa scheman som är relaterade till aktiverade segment och som skapades under det senaste året.</li></ul> |
| Distribution och aggregering | Sammanfattningsbaserade frågor om objektanvändning i Experience Platform | <ul><li>Hur många procent av de aktiverade segmenten?</li><li>Hur många fält används vid segmentering?</li><li>Vilka segment aktiveras för det största antalet destinationer?</li><li>Lista duplicerade segment.</li><li>Visa de segment som är aktiverade för {DESTINATION_ACCOUNT_NAME} och rangordna dem efter profilstorlek.</li><li>Hur stor procentandel av segmenten som inte har aktiverats men som har fler än 100 profiler. Visa mig deras namn.</li><li>Visa de fem vanligaste attributen som används i aktiverade segment baserat på deras förekomst.</li></ul> |
| Objektsökning | Hämta eller få åtkomst till ett Experience Platform-objekt eller dess egenskaper. | <ul><li>Vilka datamängder har inget associerat schema</li><li>Visa de attribut som används för {SEGMENT_NAME}?</li><li>Ge mig listan över scheman som är aktiverade för profiler, men som inte har ändrats sedan de skapades.</li><li>Vilka segment har ändrats den senaste veckan?</li><li>Visa en lista över de segment som har samma segmentdefinitioner tillsammans med deras skapandedatum.</li><li>Vilka datauppsättningar är profilaktiverade och innehåller även hur många segment som har skapats från varje datauppsättning.</li><li>Visa segmentdefinitionen och ändringsdatumet för {SEGMENT_NAME}.</li></ul> |

+++

## Verifiera svaret

Du kan verifiera det svar som assistenten returnerar på flera olika sätt.

### Citat från dokumentation

I varje svar ger Assistant dig citat som du kan referera till för verifiering eller mer information.

Välj **[!UICONTROL Show source]** en lista med länkar till dokumentation som assistenten refererar till för att beräkna sitt svar. När du väljer en länk till den refererade dokumentationen, kommer du till det relevanta avsnittet på den aktuella sidan med den specifika informationen markerad.

![Länkarna till källan som visas i assistenten.](./images/ai-assistant/show-sources.png)

## Ge feedback

>[!BEGINSHADEBOX]

**Din feedback har begärts**

Under den här Alpha-fasen uppmanas du att ge feedback på de svar du får från assistenten. Alla svar och inskickade kommentarer granskas för att fortsätta förbättra assistentupplevelsen.

Om du vill ge feedback väljer du antingen tummen uppåt eller tummen nedåt när du fått ett svar från assistenten och anger sedan dina kommentarer i textrutan. Nästa, välj **[!UICONTROL Submit feedback]** att skicka in.

>[!ENDSHADEBOX]

+++Ge feedback

>[!BEGINTABS]

>[!TAB Tummen upp]

Klicka på ikonen för att visa vad som gick bra med assistenten.

![Fönstret för positiv feedback.](./images/ai-assistant/thumbs-up.png)

>[!TAB Tummen ned]

Välj ikonen med reglaget nedåt för att ge feedback på vad som kan förbättras baserat på din erfarenhet av assistenten. Under det här steget kan du även ge specifika kommentarer om din upplevelse. Synpunkter i kommentarerna granskas dagligen.

![Fönstret för negativ feedback.](./images/ai-assistant/thumbs-down.png)

>[!TAB Flagga]

Välj flaggikonen om du vill visa fler rapporter om din upplevelse med assistenten.

![Rapportresultatfönstret.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Ytterligare information

Mer information om assistenten för Experience Platform finns i det här avsnittet.

### Caveats and limits

I följande avsnitt beskrivs aktuella kavattar och begränsningar som ska beaktas när assistenten används.

#### Konversationsupplevelser

Du måste ta hänsyn till flera nyanser om konversationsupplevelsen när du frågar assistenten.

>[!NOTE]
>
>Dessa begränsningar är tillfälliga och förbättras under hela alfavärdet.

>[!BEGINTABS]

>[!TAB Det går inte att härleda kontext från föregående diskussion]

Assistenten kan för närvarande inte referera till tidigare diskussioner som kontext för en given fråga. Se tabellen nedan för exempel:

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Finns det olika typer av sådana?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Uppföljningsfråga:&quot;Finns det olika typer av **segment**?&quot;</li></ul> | Assistenten kan inte sluta sig till vad &quot;de&quot; betyder. |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du utveckla mer?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Fråga:&quot;Förklara vad ett segment är i detalj&quot;</li></ul> | Assistenten kan inte på ett intelligent sätt referera till dokumentation baserad på &quot;mer&quot;. |
| <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du ge mig ett exempel på en sådan?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett segment?&quot;</li><li>Följa upp frågan:&quot;Kan du ge mig ett exempel på ett segment?&quot;</li></ul> | Assistenten kan inte sluta sig till vad du vill ha ett exempel på. |
| <ul><li>Första frågan:&quot;Vad är ett gruppsegment?&quot;</li><li>Följa frågan:&quot;Hur fungerar det jämfört med ett direktuppspelningssegment?&quot;</li></ul> | <ul><li>Första frågan:&quot;Vad är ett gruppsegment?&quot;</li><li>Följ upp frågan:&quot;Kan du jämföra ett direktuppspelningssegment med ett gruppsegment?&quot;</li></ul> | Assistenten kan inte sluta sig till vad &quot;den&quot; syftar på och kan därför inte jämföra direktuppspelningssegmentet. |
| <ul><li>Första frågan:&quot;Hur många segment har jag?&quot;</li><li>Fråga:&quot;Hur många av dem använder Facebook som mål?&quot;</li></ul> | <ul><li>Första frågan:&quot;Hur många segment har jag?&quot;</li><li>Fråga:&quot;Hur många av de segment jag har använder Facebook som mål?&quot;</li></ul> | Assistenten kan inte sluta sig till vad &quot;de&quot; syftar på. |

{style="table-layout:auto"}

>[!TAB Det går inte att härleda kontext från en sida]

När du frågar assistenten om ett visst element på användargränssnittssidan för Experience Platform som du är på, måste du tydligt definiera det specifika elementet i din fråga.

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| &quot;Vad gör det här?&quot; | &quot;Vad gör {PAGE_NAME} eller hur? | Assistenten kan inte sluta sig till vad &quot;this&quot; syftar på. Du måste ange det specifika sidelementet som du frågar om. |
| &quot;Varför sparar det inte?&quot; | &quot;Varför kan jag inte spara en ny sandlåda med namnet {NAME}?&quot; | Assistenten kan inte sluta sig till vad &quot;det&quot; syftar på och kan inte veta att du har problem med en entitet. |

{style="table-layout:auto"}

Assistenten kan dessutom bara besvara frågor om felmeddelanden, eftersom felet är dokumenterat i Experience League.

>[!TAB Tvetydighet]

Du måste formulera dina frågor tydligt och definiera dem i en produkt, ett program eller en domän, eftersom assistenten för närvarande inte kan tolka några frågor.

| Tvetydig fråga | Tydlig fråga | Anteckning |
| --- | --- | --- |
| &quot;Hur skapar jag ett filter? | Hur skapar jag ett filter i Profilfrågespråk? | Du måste ange den funktion som du filtrerar efter eftersom en mängd olika Experience Platform-funktioner stöder filtrering. |
| &quot;Hur kommer jag igång? | Hur kommer jag igång med att använda destinationer? | Du måste ge en tydlig bild av dina mål och användningsfall eftersom alltför breda koncept kan resultera i generiska eller onödigt specifika svar. |

{style="table-layout:auto"}

>[!ENDTABS]

#### Begränsat litet snack

Du kan delta i små samtal med assistenten, men den här kapaciteten är för närvarande begränsad.

#### Funktionsfrågor

Assistenten kan ge ett felaktigt intryck av vad den kan göra. Följande typer av frågor kan besvaras felaktigt:

| Exempelfråga | Anteckning |
| --- | --- |
| &quot;Kan du svara på frågor om {ENTITY}?&quot; | Så länge assistenten kan hitta en sida som refererar till en viss enhet i sitt index, kommer den att svara ja. |
| &quot;Vet ni **x** språk?&quot; | Assistenten har för närvarande bara stöd för engelska, men kan svara&quot;ja&quot; på grund av att den underliggande modellen har stöd för den. |
| &quot;Kan du göra..?&quot; | Assistenten kan svara ja, även om den inte kan det. |

### Tips

I följande avsnitt beskrivs några tips och tillfälliga lösningar som du bör tänka på när du använder Assistant.

#### Frågor kan besvaras med fel informationskälla

Det finns tillfällen när din fråga om dina användningsdata kan resultera i ett svar baserat på dokumentationen. Detta beror på att assistenten felaktigt kan dirigera din fråga till fel informationskälla. Du kan förhindra detta genom att:

* Reparera frågan för att använda mer SQL-liknande språk
* Uttryckligen anropa informationskällan som ska användas.

Se tabellen nedan för exempel:

| Felaktig fråga | Bra fråga | Anteckningar |
| --- | --- | --- |
| Vad är mitt största segment? | Vad är mitt största segment? Använda data. | Tala uttryckligen om för assistenten att du vill att svaret ska baseras på data. |
| Vad är mitt största segment? | Lista mitt största segment. | Det finns tillfällen då en fråga om vad.. kan bli fel för en dokumentationsbaserad fråga. Att använda ett kommando som &quot;list&quot; är en starkare indikator på att du ställer en fråga med data i sitt sammanhang. |
| Hur många datauppsättningar har jag? | Räkna mina datauppsättningar. | Den ursprungliga frågan fungerar för segment, men fungerar kanske inte med datauppsättningar. |
