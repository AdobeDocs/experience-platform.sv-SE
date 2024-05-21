---
title: AI Assistant för Adobe Experience Platform
description: Lär dig hur du använder AI Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: 6beaefb23f4deb382b7844fcf58efbd72b1da2ec
workflow-type: tm+mt
source-wordcount: '3085'
ht-degree: 0%

---

# AI Assistant för Adobe Experience Platform

>[!NOTE]
>
>AI Assistant för Adobe Experience Platform är för närvarande i Beta. Funktionen och dokumentationen kan komma att ändras.

AI Assistant är en gränssnittsfunktion som du kan använda för att navigera bland och förstå Adobe Experience Platform- och Real-time Customer Data Platform-koncept och användarinformation om dina objekt.

Du kan fråga AI Assistant efter information som:

* Vägledning om hur man utför uppgifter som rör data och målgrupper.
* Status och mått för befintliga dataobjekt i organisationen.
* Använd exempel och nyanser för att få en bättre förståelse för era dataobjekt, inklusive attribut, målgrupper, dataflöden, datauppsättningar, mål, scheman och källor.

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
   * Vilka målgrupper har aktiverats?

>[!ENDSHADEBOX]

## Mål som du kan uppnå med AI Assistant {#objectives}

Du kan använda AI Assistant för mål som:

| Syfte | Beskrivning | Exempel |
| --- | --- | --- |
| Utbildningsbegrepp och fortsatta arbetsflöden | <ul><li>Som nybörjare kan du använda AI Assistant för att lära dig Real-Time CDP- och Adobe Journey Optimizer-koncept och själv ta till vara produkter och funktioner som du inte känner till.</li><li>Som erfaren användare kan du använda AI Assistant för att lösa ett edge-fall som kan blockera ditt arbetsflöde. | <ul><li>Hur skapar jag en kontrollpanel i Journey Analytics?</li><li>Berätta några användningsfall för Real-Time CDP.</li></ul> |
| Felsökning | Använd AI Assistant för att lära dig hur du felsöker grundläggande fel som kan uppstå i arbetsflödet. | <ul><li>Vad är felet? {ERROR_MESSAGE} menar du?</li><li>Varför kan jag inte ta bort målgruppen Luma: Email Audience?</li></ul> |
| Sandlådehygien | Använd AI Assistant för att identifiera eventuella dubbletter eller oanvända objekt så att du effektivt kan underhålla sandlådan. | <ul><li>Kan ni visa mig målgrupper som är lika?</li><li>Finns det några scheman som inte har någon associerad datauppsättning?</li></ul> |
| Värdeanalys | Använd AI Assistant för att identifiera dina mest använda dataobjekt och utvärdera eventuella prestandaindikatorer eller hitta de värdefullaste dataobjekten. | <ul><li>Hur många profiler finns i segmentdefinitionen&quot;Luma: Email Audience&quot;?</li><li>När aktiverades målgrupper för målgrupper i Experience Cloud?</li></ul> |
| Sök | Använd AI Assistant för att hitta Experience Platform-objekt som stöds, som målgrupper, datauppsättningar, destinationer, scheman och källor. | <ul><li>Visa en lista över målgrupper som innehåller&quot;Luma&quot; i namnet som skapades under det senaste kvartalet.</li><li>Vilka attribut finns i XDM-schemat&quot;Luma: Custom Actions&quot;?</li></ul> |
| Effektanalys | Använd AI Assistant för att identifiera dataobjekt som har använts i vissa arbetsflöden, så att du kan bedöma effekten av eventuella ändringar. | <ul><li>Vilka målgrupper använder `homeAddress.city` i schemat &quot;Luma: PersonProfiles&quot;?</li><li>Vilka datamängder är `consents.marketing.push.val` vilket profilattribut som lagras i?</li></ul> |

## Åtkomst till AI-assistenten i användargränssnittet i Experience Platform

Välj alternativet **[!UICONTROL AI Assistant icon]** från Experience Platform översta huvud i användargränssnittet.

![Experience Platform hemsida med ikonen AI Assistant vald och gränssnittet AI Assistant öppet.](./images/ai-assistant/ai-assistant.png)

Gränssnittet för AI Assistant visas och du får information om hur du kommer igång direkt. Du kan använda alternativen i [!UICONTROL Ideas to get started] svara på frågor och kommandon som:

* [!UICONTROL Which of my audiences are activated?]
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

### Användningsdata och visualisering {#usage-data-and-visualization}

+++Välj för att visa ett exempel på frågor om användningsdata och datavisualisering

För att AI Assistant ska kunna svara på en fråga om användningsdata inom organisationen måste du vara i en aktiv sandlåda.

I exemplet nedan har AI Assistant följande fråga: **&quot;Visa segmentdefinitioner med över 1 000 profiler och inkludera aktiveringsstatus.&quot;** AI Assistant svarar sedan med ett diagram som visualiserar era segment- och profildata.

![Följ upp frågan om användningsdata.](./images/ai-assistant/data-usage-question.png)

Du kan hovra över ett enskilt fält om du vill visa specifika data. Du kan också välja ikonen för att expandera om du vill visa diagrammet i en större vy.

![Uppföljningsfråga som illustrerar datavisualisering.](./images/ai-assistant/data-visualization.png)

En utökad vy av visualiseringen visas. Du kan använda det utökade modala verktyget för att inspektera dina data ytterligare och det är särskilt användbart när visualisering returneras med ett stort antal kolumner.

![Utökat diagram.](./images/ai-assistant/chart-expanded.png)

När en fråga om användningsdata visas ger AI Assistant en förklaring av hur svaret beräknades. I exemplet nedan visar AI Assistant de steg som har utförts för att visa segmentdefinitioner med över 1 000 profiler och deras respektive aktiveringsstatus.

![Uppföljningsfråga om segmentdefinitioner som illustrerar hur AI Assistant beräknade svaret.](./images/ai-assistant/results-explained.png)

Du kan även lägga till filter och ändringar i dina frågor och du kan instruera AI Assistant att återge resultatet baserat på de filter som du inkluderar. Du kan till exempel be AI Assistant att visa en trend för antalet segmentdefinitioner i den ordning de skapades, ta bort segmentdefinitioner med noll som summor och använda namn på månader i stället för heltal när data visas.

+++

### Använd automatisk komplettering {#use-auto-complete}

+++Markera för att visa ett exempel på automatisk komplettering

Du kan använda funktionen för automatisk komplettering för att ta emot en lista med dataobjekt som finns i din sandlåda. Rekommendationer som fylls i automatiskt finns tillgängliga för följande domäner: målgrupper, scheman, datamängder, källor och destinationer.

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

## Användningsdata {#usage-date}

Du kan även ställa frågor om AI Assistant om dina användningsdata i följande domäner:

* Attribut
* Målgrupper
* Dataflöden
* Datauppsättningar
* Destinationer _(Frågor om konton och vissa frågor om dataflöde kan inte besvaras just nu.)_
* Scheman _(Frågor om fältgrupper kan inte besvaras just nu.)_
* Källor _(Frågor om konton kan inte besvaras just nu.)_

För användningsdatafrågor kanske svaren inte speglar det aktuella läget för användargränssnittet. De data som ligger till grund för dessa frågor uppdateras en gång var 24:e timme. De ändringar som användare gör i Real-Time CDP under dagtid synkroniseras till exempel med datalager på natten och blir sedan tillgängliga för användarfrågor på morgonen. Dessutom måste du logga in i en sandlåda för att få frågor om specifika data som rör objekt som målgrupper, scheman, datamängder, attribut och mål.

### Exempel på frågor om användningsdata {#example-usage-data-questions}

+++Välj om du vill se en lista över användningsdatafrågor

I tabellen nedan finns exempel på användningsdatafrågor och användningsexempel:

| Frågetyp | Användningsfall | Exempel |
| --- | --- | --- | 
| Datalinje | Spåra användningen av ett eller flera objekt över andra Experience Platform-objekt | <ul><li>Vilka datauppsättningar använder schemat &quot;ACME schema&quot;?</li><li>Hur många datauppsättningar har importerats med samma schema?</li><li>Vilka datauppsättningar har använts i aktiverade målgrupper?</li><li>Lista scheman som har attribut som används i aktiverade målgrupper.</li><li>Visa vilka målgrupper som är aktiverade för&quot;ACME Destinations&quot; och som har fler än 1 000 profiler.</li><li>Visa vilka attribut som används i de aktiverade målgrupperna som har ändrats efter januari 2023.</li><li>Vilka datauppsättningar hämtas via källan&quot;ACME Amazon S3&quot;?</li><li>Vilka dataflöden är kopplade till&quot;ACME Loyalty Dataflow&quot;?</li><li>Lista scheman som är relaterade till aktiverade målgrupper och som skapades under det senaste året.</li></ul> |
| Distribution och aggregering | Sammanfattningsbaserade frågor om objektanvändning i Experience Platform | <ul><li>Hur många procent av de aktiva målgrupperna?</li><li>Hur många fält används vid segmentering?</li><li>Vilka målgrupper aktiveras för det största antalet destinationer?</li><li>Lista duplicerade målgrupper.</li><li>Visa vilka målgrupper som är aktiverade för&quot;ACME-mål&quot; och rangordna dem efter profilstorlek.</li><li>Vad är procentandelen av de målgrupper som inte har aktiverats men som har fler än 100 profiler. Visa mig deras namn.</li><li>Lista de tre källanslutningarna som samlar in data i mina datauppsättningar.</li><li>Ange de fem vanligaste attributen som används i aktiverade målgrupper baserat på deras förekomst.</li></ul> |
| Objektsökning | Hämta eller få åtkomst till ett Experience Platform-objekt eller dess egenskaper. | <ul><li>Vilka datamängder har inget associerat schema</li><li>Vill du lista attributen som används för&quot;ACME Audience&quot;?</li><li>Ge mig listan över scheman som är aktiverade för profiler, men som inte har ändrats sedan de skapades.</li><li>Vilka målgrupper har ändrats den senaste veckan?</li><li>Ange de målgrupper som har samma segmentdefinitioner tillsammans med deras skapandedatum.</li><li>Vilka datauppsättningar är profilaktiverade och innehåller även hur många målgrupper som har skapats från varje datauppsättning.</li><li>Vilka källkonton är associerade med datauppsättningen XYZ?</li><li>Visa segmentdefinitionen och ändringsdatumet för &quot;ACME Audience&quot;.</li></ul> |
| Objektjämförelse | Identifiera duplicerade målgrupper. | <ul><li>Baserat på segmentdefinitionen kan du lista de målgrupper som är dubbletter.</li><li>Vilka duplicerade målgrupper som aktiveras för &quot;ACME Destinations&quot;.</li></ul> |

+++

## Tar hand om dina frågor {#phrasing-your-questions}

Du måste ge AI Assistant tydliga och kontextuella uppgifter för att få ett så korrekt svar som möjligt. Se följande lista med tips om hur du ställer en tydlig fråga i sitt sammanhang:

* Ange din uppgift och/eller fråga kortfattat.
* Undvik tvetydigt språk och alltför komplex syntax för att underlätta förståelsen.
* Ange relevant sammanhang för dina uppgifter och/eller frågor eftersom kontexten kan hjälpa AI Assistant att generera mer relevanta svar.

Läs tabellen nedan för mer information om de effektivaste strategierna när du ställer frågor till AI Assistant:

| Gör | Exempel |
| --- | --- |
| <ul><li>Var tydlig med objektet eller informationen som du vill hämta eller analysera.</li><li>Försök att ange dataobjektens namn inom citattecken. Om du bara känner till en del av objektnamnet kan du även ange det i frågan.</li><li>Använd [objekt som slutförs automatiskt](./ui-guide.md#use-auto-complete) för att hjälpa AI Assistant att bättre förstå sammanhanget i din fråga.</li></ul> | <ul><li>Vilka datauppsättningar använder schemat&quot;Luma - Loyalty&quot;?</li><li>Visa de aktiverade segmenten som har &quot;Luma&quot; i sina namn. Rangordna dem efter antal profiler.</li></ul> |
| <ul><li>Undvik tvetydighet och använd tydligt språk</li><li>Använd exakt terminologi för att få bättre tydlighet i frågan.</li><li>När du ställer frågor om Adobe Experience Platform kan du försöka använda terminologi som är specifik för Experience Platform för att förbättra relevansen i svaren.</li></ul> | <ul><li>Hur många profiler har jag i&quot;ACME Audience&quot;.</li><li>Visa de fem främsta XDM-attributen som används i aktiverade målgrupper.</li></ul> |
| <ul><li>Ange sammanhang eller ange ett villkor för att filtrera resultaten.</li><li>Använd ett filtervillkor i frågorna för att begränsa mängden data i svaret.</li></ul> | <ul><li>Visa målgrupper som inte har aktiverats och skapats för mer än sex månader sedan och som aldrig har ändrats.</li><li>Visa att målgrupper är aktiverade för&quot;ACME Destination&quot; och har fler än 10 000 profiler.</li></ul> |

{style="table-layout:auto"}

| Gör det inte | Exempel |
| --- | --- |
| Använd oklart eller tvetydigt språk. | <ul><li>Ge mig information om datauppsättningar.</li><li>Hur många användare har jag i&quot;ACME Audience&quot;?</li><li>Visa segment.</li><li>Listattribut.</li></ul> |
| Gör ofullständiga förfrågningar. | &quot;Luma - lojalitetsdatauppsättning&quot; |
| Anta kunskap utan sammanhang. | <ul><li>Målgrupper de senaste sex månaderna.</li><li>Bygg en fråga åt mig.</li></ul> |
| Formge alltför komplexa frågor. | Gör en omfattande analys av datalinjer för alla objekt och deras beroenden. |
| Utelämna villkor eller parametrar. | Visa datauppsättningar. |

{style="table-layout:auto"}

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
| Vilken är min största publik? | Vilken är min största publik? Använda data. | Tala uttryckligen om för AI-assistenten att du vill att svaret ska baseras på data. |
| Vilken är min största publik? | Visa min största publik. | Det finns tillfällen då en fråga om vad.. kan bli fel för en dokumentationsbaserad fråga. Att använda ett kommando som &quot;list&quot; är en starkare indikator på att du ställer en fråga med data i sitt sammanhang. |
| Hur många datauppsättningar har jag? | Räkna mina datauppsättningar. | Den ursprungliga frågan fungerar för målgrupper, men fungerar kanske inte med datauppsättningar. |
