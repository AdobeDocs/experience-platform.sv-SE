---
title: Assistent för Adobe Experience Platform
description: Lär dig hur du använder Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: 5bdfc5282e71d05ff0db39c32fc02c60fd8d1c34
workflow-type: tm+mt
source-wordcount: '2347'
ht-degree: 0%

---

# Assistent för Adobe Experience Platform

>[!NOTE]
>
>Assistenten för Adobe Experience Platform är för närvarande i Alpha. Funktionen och dokumentationen kan komma att ändras.

Assistant är en gränssnittsfunktion som du kan använda för att navigera och förstå Adobe Experience Platform- och Real-time Customer Data Platform-koncept och användningsinformation om dina objekt.

Du kan fråga Assistant om du vill ha information om:

* Vägledning om hur man utför uppgifter som rör data och målgrupper.
* Status och mått för befintliga dataobjekt i organisationen.
* Använd exempel och nyanser för att få en bättre förståelse för dataobjekten, inklusive attribut, datauppsättningar, destinationer, scheman, segment och källor.

Läs guiden nedan för att lära dig mer om hur du kan använda Assistant för att navigera i och förstå dina arbetsflöden för Experience Platform och Real-Time CDP.

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

## Åtkomstassistenten i användargränssnittet i Experience Platform

Välj **[!UICONTROL Assistant icon]** från Experience Platform översta huvud i användargränssnittet.

![Experience Platform hemsida med assistentikonen vald och assistentgränssnittet öppet.](./images/ai-assistant/ai-assistant.png)

Assistentgränssnittet öppnas och du får information om hur du kommer igång. Du kan använda alternativen i [!UICONTROL Ideas to get started] svara på frågor och kommandon som:

* [!UICONTROL Which of my segments are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

![The &quot;ideas to get started&quot; section of Assistant.](./images/ai-assistant/ideas-to-get-started.png)

Om du vill interagera med Assistant använder du inmatningsrutan för att skriva in frågor eller kommandon. Du kan också använda (**`+`**) för att använda funktionen Komplettera automatiskt och bokmärkesikonen för att komma åt frågor och kommandon med bokmärken.

![Inmatningsrutan Assistant är markerad.](./images/ai-assistant/interact.png)

## Exempel: Använd assistenten för att snabba upp framtagningen av scheman

>[!NOTE]
>
>Följande arbetsflöde är ett exempel som använder processen att skapa händelseschema för att illustrera hur du kan använda Assistant när du använder användargränssnittet i Experience Platform.

Tänk dig ett användningsexempel där du skapar en **Enhetshandel i händelseschema**. När upplevelsehändelsens schema skapades stöter du på `eventType` fält. &quot;Nu kan du välja att antingen avsluta arbetsflödet och se [grunderna i en schemakomposition](../xdm/schema/composition.md) eller så kan du använda Assistant för att få svar på dina frågor och hitta ytterligare resurser via de dokumentationslänkar som rekommenderas av Assistant.&quot;

Börja med att ange din fråga i textrutan. I exemplet nedan ställs frågan: &quot;**Vad är fältet eventType i ett ExperienceEvent-schema?**&quot;

![Assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/ai-assistant/question.png)

Assistenten frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en liten stund returnerar assistenten ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

![Assistent för Experience Platform med svar på föregående fråga.](./images/ai-assistant/answer.png)

När du har fått ett svar från assistenten kan du välja bland ett antal alternativ som avgör hur du vill fortsätta.

### Spara frågan {#save-your-query}

+++Välj för att visa ett exempel på hur du sparar en fråga

Om du vill spara frågan väljer du bokmärkesikonen bredvid frågan.

![Skärmbild av ett markerat bokmärke.](./images/ai-assistant/save-your-query.png)

Om du vill få åtkomst till dina sparade frågor väljer du bokmärkesikonen under inmatningsrutan och väljer sedan den fråga du vill köra.

![Skärmbild av bokmärkesikoner och en lista över sparade frågor.](./images/ai-assistant/bookmarks.png)

+++

### Visa data i din sandlåda {#view-data-in-your-sandbox}

+++Markera för att visa exempel

Beroende på din fråga ger Assistant ytterligare information som gäller data i din sandlåda. Om du vill visa hur svaret på din fråga gäller för din sandlåda väljer du **[!UICONTROL In your sandbox].**

Under det här steget kan assistenten tillhandahålla direktlänkar till gränssnittssidorna för vissa objekt i fråga. I exemplet nedan ger Assistant direktlänkar till [!UICONTROL Schemas] och [!UICONTROL Segments] Gränssnittssidor.

![Skärmbild av alternativet&quot;I din sandlåda&quot;.](./images/ai-assistant/in-your-sandbox.png)

+++

### Verifiera svaret {#verify-the-response}

+++Markera för att visa ett exempel på hur du visar källor

Om du vill visa citat och validera assistentens svar väljer du **[!UICONTROL Show sources]**. Assistenten tillhandahåller länkar till dokumentation som bekräftar dess svar. Du kan även använda frågor som Assistant tillhandahåller under [!UICONTROL Related suggestions] om du vill utforska ämnen som hör till den ursprungliga frågan.

![Skärmbild av &quot;Visa källor&quot;.](./images/ai-assistant/show-sources.png)

+++

### Dataanvändning och visualisering {#data-usage-and-visualization}

+++Välj för att visa ett exempel på frågor om dataanvändning och datavisualisering

Du kan fråga Assistant om din dataanvändning. Du måste vara i en aktiv sandlåda för att assistenten ska kunna besvara en fråga om dataanvändning gällande data i organisationen.

![Följ upp frågan om dataanvändning.](./images/ai-assistant/data-usage-question.png)

När assistenten tillfrågas om dataanvändning ger han även en förklaring till hur svaret beräknades. I exemplet nedan visar Assistant de steg som har vidtagits för att visa segment med över 1 000 profiler och deras respektive aktiveringsstatus.

![Följ upp frågan om segment som illustrerar hur Assistant beräknade svaret.](./images/ai-assistant/results-explained.png)

Assistant återger diagram för att visualisera data. Du kan även lägga till filter och ändringar i dina frågor och du kan instruera Assistant att återge resultatet baserat på de filter som du inkluderar. Du kan till exempel be Assistant att visa en trend för antalet segment i den ordning som de skapades, ta bort segment utan totalprofiler och använda namn på månader i stället för heltal när data visas.

![Uppföljningsfråga som illustrerar datavisualisering.](./images/ai-assistant/data-visualization.png)

+++

### Använd automatisk komplettering {#use-auto-complete}

+++Markera för att visa ett exempel på automatisk komplettering

Du kan använda funktionen för automatisk komplettering för att ta emot en lista med dataobjekt som finns i din sandlåda. Det finns rekommendationer för att slutföra automatiskt för följande domäner: segment, scheman, datauppsättningar, källor och mål.

Du kan använda Fyll i automatiskt genom att ta med plustecknet (**`+`**) i din fråga. Du kan också välja plustecknet (**`+`**) längst ned i textrutan. Ett fönster visas med en lista över rekommenderade dataobjekt från sandlådan.

![Exempel på automatisk komplettering](./images/ai-assistant/auto-complete-one.png)

Sedan markerar du det dataobjekt som du vill fråga för att slutföra din fråga och skickar sedan din fråga.

![Exempel på automatisk komplettering med fråga och svar](./images/ai-assistant/auto-complete-two.png)

+++

### Använda flera omgångar {#use-multi-turn}

+++Markera för att visa ett exempel på flera omgångar

Du kan använda Assistants multibläddringsfunktioner för att få en mer naturlig konversation under upplevelsen. Assistenten kan besvara uppföljningsfrågor. det sammanhanget kan härledas från en tidigare interaktion.

I exemplet nedan tillfrågas Assistant om det totala antalet dataflöden i den aktuella organisationen.

![Exempel på multisväng](./images/ai-assistant/multi-turn-one.png)

Assistenten får sedan en ny uppföljningsbegäran. Den här gången svarar Assistant genom att lista de dataflöden som finns i organisationen.

![Exempel på flera svarstider med fråga och svar](./images/ai-assistant/multi-turn-two.png)

+++

## Omfång {#scope}

Assistenten kan svara på frågor om Real-Time CDP och Experience Platform, liksom om din användarkontos dataanvändning. Assistenten kan även härleda kontext baserat på den gränssnittssida som du befinner dig i. Den kan identifiera

* Användarkontot som du använder.
* Organisationen som du tillhör.
* Sidan som du visar på skärmen.
* Resursen (inklusive typ och ID) som du visar på skärmen.
* Med tanke på att du arbetar med ett visst arbetsflöde i Experience Platform eller Real-Time CDP kan Assistant ta reda på vad du tänker.

### Dokumentation {#documentation}

Dokumentationsindexet täcker för närvarande Adobe Experience Platform (Real-Time CDP och Publiker). Indexet uppdateras regelbundet.

Modellen för dokumentationsåterhämtning har utbildats i Experience Platform (Real-Time CDP och Publiker). Frågor som inte omfattas av Adobe Experience Platform, t.ex. frågor om andra Adobe-produkter som Adobe Target och Creative Cloud Suite, kan inte besvaras.

### Dataanvändning {#data-usage}

Du kan även ställa frågor till assistenten om din dataanvändning i följande domäner:

* Attribut
* Datauppsättningar
* Destinationer _(Frågor om konton och vissa frågor om dataflöde kan inte besvaras just nu.)_
* Scheman _(Frågor om fältgrupper kan inte besvaras just nu.)_
* Segment
* Källor _(Frågor om konton kan inte besvaras just nu.)_

För användningsdatafrågor kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som ligger till grund för dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Du kan behöva formatera dina frågor som:&quot;När var segmentet med titeln? {TITLE} skapad?&quot; istället för: &quot;När var {TITLE} segmentet skapades?&quot;

Du måste logga in i en sandlåda för att få frågor om specifika data som rör objekt som scheman, datamängder, attribut, mål och segment.

### Exempel på frågor om dataanvändning {#example-data-usage-questions}

+++Välj för att visa en lista med exempelfrågor om dataanvändning

| Frågetyp | Beskrivning | Exempel |
| --- | --- | --- | 
| Datalinje | Spåra användningen av ett eller flera objekt över andra Experience Platform-objekt | <ul><li>Vilka datauppsättningar som används {SCHEMA_NAME} schema?</li><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilka datauppsättningar har använts i aktiverade segment?</li><li>Lista de scheman som har attribut som används i aktiverade segment.</li><li>Visa de segment som aktiveras för {DESTINATION_ACCOUNT_NAME} och har fler än 1 000 profiler.</li><li>Visa de attribut som används i aktiverade segment som har ändrats efter januari 2023.</li><li>Vilka datauppsättningar hämtas via {SOURCE_NAME}?</li><li>Vilka dataflöden som är associerade med {DATAFLOW_NAME}</li><li>Visa scheman som är relaterade till aktiverade segment och som skapades under det senaste året.</li></ul> |
| Distribution och aggregering | Sammanfattningsbaserade frågor om objektanvändning i Experience Platform | <ul><li>Hur många procent av de aktiverade segmenten?</li><li>Hur många fält används vid segmentering?</li><li>Vilka segment aktiveras för det största antalet destinationer?</li><li>Lista duplicerade segment.</li><li>Visa de segment som är aktiverade för {DESTINATION_ACCOUNT_NAME} och rangordna dem efter profilstorlek.</li><li>Hur stor procentandel av segmenten som inte har aktiverats men som har fler än 100 profiler. Visa mig deras namn.</li><li>Lista de tre källanslutningarna som samlar in data i mina datauppsättningar.</li><li>Visa de fem vanligaste attributen som används i aktiverade segment baserat på deras förekomst.</li></ul> |
| Objektsökning | Hämta eller få åtkomst till ett Experience Platform-objekt eller dess egenskaper. | <ul><li>Vilka datamängder har inget associerat schema</li><li>Visa de attribut som används för {SEGMENT_NAME}?</li><li>Ge mig listan över scheman som är aktiverade för profiler, men som inte har ändrats sedan de skapades.</li><li>Vilka segment har ändrats den senaste veckan?</li><li>Visa en lista över de segment som har samma segmentdefinitioner tillsammans med deras skapandedatum.</li><li>Vilka datauppsättningar är profilaktiverade och innehåller även hur många segment som har skapats från varje datauppsättning.</li><li>Vilka källkonton är associerade med datauppsättningen XYZ?</li><li>Visa segmentdefinitionen och ändringsdatumet för {SEGMENT_NAME}.</li></ul> |

+++

## Ge feedback {#feedback}

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

## Ytterligare information {#additional-information}

Mer information om assistenten för Experience Platform finns i det här avsnittet.

### Caveats and limits {#caveats-and-limitations}

I följande avsnitt beskrivs aktuella kavattar och begränsningar som ska beaktas när assistenten används.
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### Begränsat litet snack

Du kan delta i små samtal med assistenten, men den här kapaciteten är för närvarande begränsad.

#### Funktionsfrågor

Assistenten kan ge ett felaktigt intryck av vad den kan göra. Följande typer av frågor kan besvaras felaktigt:

| Exempelfråga | Anteckning |
| --- | --- |
| &quot;Kan du svara på frågor om {ENTITY}?&quot; | Så länge assistenten kan hitta en sida som refererar till en viss enhet i sitt index, kommer den att svara ja. |
| &quot;Vet ni **x** språk?&quot; | Assistenten har för närvarande bara stöd för engelska, men kan svara&quot;ja&quot; på grund av att den underliggande modellen har stöd för den. |
| &quot;Kan du göra..?&quot; | Assistenten kan svara ja, även om den inte kan det. |

### Tips {#tips}

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
