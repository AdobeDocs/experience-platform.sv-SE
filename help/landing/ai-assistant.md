---
title: AI Assistant för Adobe Experience Platform
description: Lär dig hur du använder AI Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: b1f2d85f5a1cf6bb38344c87496488a919800029
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 0%

---

# AI Assistant för Adobe Experience Platform

>[!NOTE]
>
> AI Assistant för Adobe Experience Platform ligger i Alpha. Funktionen och dokumentationen kan komma att ändras.

AI Assistant är en gränssnittsfunktion som du kan använda för att navigera bland och förstå Adobe Experience Platform- och Real-time Customer Data Platform-koncept och användarinformation om dina objekt.

Du kan fråga AI Assistant efter information som:

* Vägledning om hur man utför uppgifter som rör data och målgrupper.
* Status och mått för befintliga dataobjekt i organisationen.
* Använd exempel och nyanser för att få en bättre förståelse för dataobjekten, inklusive attribut, dataflöden, datauppsättningar, mål, scheman, segment och källor.

Läs guiden nedan för att lära dig hur du kan använda AI Assistant för att navigera i och förstå dina arbetsflöden för Experience Platform och Real-Time CDP.

>[!BEGINSHADEBOX]

**Hur fungerar AI Assistant?**

AI Assistant besvarar dina inskickade frågor genom att fråga en databas och sedan omvandla data från databasen till ett läsbart svar.

Denna interna representation av underliggande data kallas även kunskapsdiagram - ett omfattande nät av koncept, data och metadata för ett givet svar.

Kunskapsdiagrammet består av deldiagram som refereras när frågor skickas:

* Kundanvändningsdata.
* Kundanvändningsdata för olika metabutiker.
* Experience League dokumentation.

Det finns två frågeklasser att tänka på innan du frågar AI Assistant:

* **Konceptfrågor**: Konceptfrågor handlar om Adobe-koncept som rör data eller målgrupper. Några exempel på konceptfrågor är:
   * Vad är skillnaden mellan gruppsegmentering och direktuppspelningssegmentering?
   * Finns det branschdatamodeller och hur använder jag dem?
   * Vad är Real-Time CDP bäst för?
* **Användningsfrågor**: Användningsfrågor handlar om dataobjekten i organisationen. Några exempel på användningsfrågor är:
   * Hur många datauppsättningar har jag?
   * Hur många schemaattribut har aldrig använts?
   * Vilka segment har aktiverats?

>[!ENDSHADEBOX]

## Mål som du kan uppnå med AI Assistant

Du kan använda AI Assistant för mål som:

| Syfte | Beskrivning |
| --- | --- |
| Att lära sig Experience Platform och Real-Time CDP | Du kan ställa frågor om konceptuella AI Assistant så att du kan komma in på Experience Platform och Real-Time CDP. Du kan också använda AI Assistant för att lära dig mer om objekt och beteenden som du inte är bekant med. |
| Säkerställa dataskornighet i sandlådor | Du kan använda AI Assistant för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan upprätthålla sandlådans renhet. |
| Samordna värdeanalys | Du kan använda AI Assistant för att identifiera dina mest använda objekt och utvärdera eventuella prestandaindikatorer eller hitta de mest värdefulla data. |
| Förstå effektanalys | Du kan använda AI Assistant för att identifiera objekt som har använts i vissa arbetsflöden, så att du kan utvärdera effekten av eventuella ändringar. |
| Övervaka dina data | Du kan använda AI Assistant för att övervaka dataflöden, inmatning och utvärderingsjobb så att du kan visa eventuella avvikelser eller rapportera om förloppet. |

## Åtkomst till AI-assistenten i användargränssnittet i Experience Platform

Välj alternativet **[!UICONTROL AI Assistant icon]** från Experience Platform översta huvud i användargränssnittet.

![Experience Platform hemsida med ikonen AI Assistant vald och gränssnittet AI Assistant öppet.](./images/ai-assistant/ai-assistant.png)

Gränssnittet för AI Assistant visas och du får information om hur du kommer igång direkt. Du kan använda alternativen i [!UICONTROL Ideas to get started] svara på frågor och kommandon som:

* [!UICONTROL Which of my segments are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

![The &quot;ideas to get started&quot; section of AI Assistant.](./images/ai-assistant/ideas-to-get-started.png)

Om du vill interagera med AI Assistant använder du inmatningsrutan för att skriva in frågor eller kommandon. Du kan också använda (**`+`**) för att använda funktionen Komplettera automatiskt och bokmärkesikonen för att komma åt frågor och kommandon med bokmärken.

![Inmatningsrutan för AI Assistant är markerad.](./images/ai-assistant/interact.png)

## Exempel: Använd AI Assistant för att skapa scheman snabbare

>[!NOTE]
>
>Följande arbetsflöde är ett exempel som använder processen för att skapa händelseschema för att illustrera hur du kan använda AI Assistant när du använder användargränssnittet i Experience Platform.

Tänk dig ett användningsexempel där du skapar en **Enhetshandel i händelseschema**. När upplevelsehändelsens schema skapades stöter du på `eventType` fält. &quot;Nu kan du välja att antingen avsluta arbetsflödet och se [grunderna i en schemakomposition](../xdm/schema/composition.md) eller så kan du använda AI Assistant för att få svar på dina frågor och hitta ytterligare resurser via de dokumentationslänkar som rekommenderas av AI Assistant.&quot;

Börja med att ange din fråga i textrutan. I exemplet nedan ställs frågan: &quot;**Vad är fältet eventType i ett ExperienceEvent-schema?**&quot;

![AI-assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/ai-assistant/question.png)

AI Assistant frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en stund returnerar AI Assistant ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

![AI Assistant för Experience Platform med svar på föregående fråga.](./images/ai-assistant/answer.png)

När du har fått ett svar från AI Assistant kan du välja bland ett antal alternativ som avgör hur du vill fortsätta.

### Spara frågan {#save-your-query}

+++Välj för att visa ett exempel på hur du sparar en fråga

Om du vill spara frågan väljer du bokmärkesikonen bredvid frågan.

![Skärmbild av ett markerat bokmärke.](./images/ai-assistant/save-your-query.png)

Om du vill få åtkomst till dina sparade frågor väljer du bokmärkesikonen under inmatningsrutan och väljer sedan den fråga du vill köra.

![Skärmbild av bokmärkesikoner och en lista över sparade frågor.](./images/ai-assistant/bookmarks.png)

+++

### Visa data i din sandlåda {#view-data-in-your-sandbox}

+++Markera för att visa exempel

Beroende på din fråga innehåller AI Assistant ytterligare information om data i din sandlåda. Om du vill visa hur svaret på din fråga gäller för din sandlåda väljer du **[!UICONTROL In your sandbox].**

Under det här steget kan AI Assistant tillhandahålla direktlänkar till gränssnittssidorna för vissa objekt i fråga. I exemplet nedan innehåller AI Assistant direkta länkar till [!UICONTROL Schemas] och [!UICONTROL Segments] Gränssnittssidor.

![Skärmbild av alternativet&quot;I din sandlåda&quot;.](./images/ai-assistant/in-your-sandbox.png)

+++

### Verifiera svaret {#verify-the-response}

+++Markera för att visa ett exempel på hur du visar källor

Om du vill visa citat och validera AI Assistants svar väljer du **[!UICONTROL Show sources]**. AI Assistant tillhandahåller länkar till dokumentation som bekräftar dess svar. Du kan även använda frågor som AI Assistant tillhandahåller under [!UICONTROL Related suggestions] om du vill utforska ämnen som hör till den ursprungliga frågan.

![Skärmbild av &quot;Visa källor&quot;.](./images/ai-assistant/show-sources.png)

+++

### Dataanvändning och visualisering {#data-usage-and-visualization}

+++Välj för att visa ett exempel på frågor om dataanvändning och datavisualisering

För att AI Assistant ska kunna svara på en fråga om dataanvändning inom organisationen måste du vara i en aktiv sandlåda.

I exemplet nedan har AI Assistant följande fråga: **&quot;Visa segmentdefinitioner med över 1 000 profiler och inkludera aktiveringsstatus.&quot;** AI Assistant svarar sedan med ett diagram som visualiserar era segment- och profildata.

![Följ upp frågan om dataanvändning.](./images/ai-assistant/data-usage-question.png)

Du kan hovra över ett enskilt fält om du vill visa specifika data. Du kan också välja ikonen för att expandera om du vill visa diagrammet i en större vy.

![Uppföljningsfråga som illustrerar datavisualisering.](./images/ai-assistant/data-visualization.png)

En utökad vy av visualiseringen visas. Du kan använda det utökade modala verktyget för att inspektera dina data ytterligare och det är särskilt användbart när visualisering returneras med ett stort antal kolumner.

![Utökat diagram.](./images/ai-assistant/chart-expanded.png)

När du får en fråga om dataanvändning ger AI Assistant en förklaring av hur svaret beräknades. I exemplet nedan visar AI Assistant de steg som har utförts för att visa segmentdefinitioner med över 1 000 profiler och deras respektive aktiveringsstatus.

![Uppföljningsfråga om segment som illustrerar hur AI Assistant beräknade svaret.](./images/ai-assistant/results-explained.png)

Du kan även lägga till filter och ändringar i dina frågor och du kan instruera AI Assistant att återge resultatet baserat på de filter som du inkluderar. Du kan till exempel be AI Assistant att visa en trend för antalet segmentdefinitioner i den ordning de skapades, ta bort segmentdefinitioner med noll som summor och använda namn på månader i stället för heltal när data visas.

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

Du kan använda AI Assistants multibläddringsfunktioner för att få en mer naturlig konversation under upplevelsen. AI Assistant kan besvara uppföljningsfrågor. det sammanhanget kan härledas från en tidigare interaktion.

I exemplet nedan tillfrågas AI Assistant om det totala antalet dataflöden i den aktuella organisationen.

![Exempel på multisväng](./images/ai-assistant/multi-turn-one.png)

Därefter får AI Assistant en ny uppföljningsbegäran. Den här gången svarar AI Assistant genom att lista de dataflöden som finns i organisationen.

![Exempel på flera svarstider med fråga och svar](./images/ai-assistant/multi-turn-two.png)

+++

## Dokumentation {#documentation}

Dokumentationsindexet täcker för närvarande Adobe Experience Platform (Real-Time CDP och Publiker). Indexet uppdateras regelbundet.

Modellen för dokumentationsåterhämtning har utbildats i Experience Platform (Real-Time CDP och Publiker). Frågor som inte omfattas av Adobe Experience Platform, t.ex. frågor om andra Adobe-produkter som Adobe Target och Creative Cloud Suite, kan inte besvaras.

## Dataanvändning {#data-usage}

Du kan även ställa frågor om din dataanvändning i följande domäner:

* Attribut
* Dataflöden
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

Under det här Alpha-steget uppmanas du att ge feedback på de svar du får från AI-assistenten. Alla svar och inskickade kommentarer granskas för att fortsätta förbättra AI Assistant-upplevelsen.

Om du vill ge feedback väljer du antingen tummen uppåt eller tummen nedåt när du fått ett svar från AI-assistenten och anger sedan din feedback i textrutan. Nästa, välj **[!UICONTROL Submit feedback]** att skicka in.

>[!ENDSHADEBOX]

+++Ge feedback

>[!BEGINTABS]

>[!TAB Tummen upp]

Välj ikonen med tummen uppåt för att ge feedback på vad som gick bra med din upplevelse av AI-assistenten.

![Fönstret för positiv feedback.](./images/ai-assistant/thumbs-up.png)

>[!TAB Tummen ned]

Välj ikonen med reglaget nedåt för att ge feedback på vad som kan förbättras baserat på din erfarenhet av AI Assistant. Under det här steget kan du även ge specifika kommentarer om din upplevelse. Synpunkter i kommentarerna granskas dagligen.

![Fönstret för negativ feedback.](./images/ai-assistant/thumbs-down.png)

>[!TAB Flagga]

Välj flaggikonen om du vill visa fler rapporter om din upplevelse med hjälp av AI-assistenten.

![Rapportresultatfönstret.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Ytterligare information {#additional-information}

Mer information om AI-assistenten för Experience Platform finns i det här avsnittet.

### Caveats and limits {#caveats-and-limitations}

I följande avsnitt beskrivs aktuella kavattar och begränsningar som ska beaktas när AI Assistant används.
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the AI Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The AI Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The AI Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The AI Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The AI Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The AI Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The AI Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the AI Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The AI Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The AI Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the AI Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the AI Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### Begränsat litet snack

Du kan använda AI Assistant i små samtal, men den här kapaciteten är för närvarande begränsad.

#### Funktionsfrågor

AI-assistenten kan ge ett felaktigt intryck av vad den kan göra. Följande typer av frågor kan besvaras felaktigt:

| Exempelfråga | Anteckning |
| --- | --- |
| &quot;Kan du svara på frågor om {ENTITY}?&quot; | Så länge AI-assistenten kan hitta en sida som refererar till en viss enhet i sitt index, kommer den att svara ja. |
| &quot;Vet ni **x** språk?&quot; | AI-assistenten har för närvarande bara stöd för engelska, men kan svara&quot;ja&quot; på grund av att den underliggande modellen kan stödja den. |
| &quot;Kan du göra..?&quot; | AI-assistenten kan svara ja, även om den inte kan det. |

### Tips {#tips}

I följande avsnitt beskrivs några tips och tillfälliga lösningar som du bör tänka på när du använder AI Assistant.

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
