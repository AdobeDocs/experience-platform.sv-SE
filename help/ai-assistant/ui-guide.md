---
title: AI Assistant i Adobe Experience Platform
description: Lär dig hur du använder AI Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 0ee9135b2b303f4abcc4d5e5c7345e2bff9332f3
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 0%

---

# Användargränssnittshandbok för AI Assistant

Läs den här guiden och lär dig hur du kan använda AI Assistant i Adobe Experience Platform-gränssnittet.

## Åtkomst till AI-assistenten i användargränssnittet i Experience Platform

Om du vill starta AI Assistant väljer du **[!UICONTROL AI Assistant icon]** i Experience Platform-gränssnittets övre sidhuvud.

![Hemsidan för Experience Platform, med ikonen AI-assistenten markerad och gränssnittet AI-assistenten öppet.](./images/ai-assistant-full-icon.png)

Gränssnittet för AI Assistant visas och du får information om hur du kommer igång direkt. Du kan använda alternativen under [!UICONTROL Ideas to get started] för att besvara frågor och kommandon som:

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Användargränssnittshandbok för AI Assistant

>[!NOTE]
>
>Följande arbetsflöde är ett exempel som använder processen för att skapa händelseschema för att illustrera hur du kan använda AI Assistant när du använder användargränssnittet i Experience Platform.

Tänk på ett användningsfall där du skapar en **enhetshandel i händelseschema**. När händelseschemat för upplevelse skapades, stötte du på fältet `eventType`. &quot;I det här skedet kan du antingen avsluta ditt arbetsflöde och hänvisa till [grunderna i en schemakomposition](../xdm/schema/composition.md) eller använda AI Assistant för att få svar på dina frågor och hitta ytterligare resurser via de dokumentationslänkar som rekommenderas av AI Assistant.&quot;

Börja med att ange din fråga i textrutan. I exemplet nedan anges frågan: **Vad är fältet eventType i ett ExperienceEvent-schema?**?

![AI-assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/question.png)

AI Assistant frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en stund returnerar AI Assistant ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

![AI-assistenten för Experience Platform med svar på föregående fråga.](./images/answer.png)

När du har fått ett svar från AI Assistant kan du välja bland ett antal alternativ som avgör hur du vill fortsätta.

### AI Assistant-funktioner {#features}

I det här avsnittet beskrivs de olika funktionerna i AI Assistant som du kan använda i dina arbetsflöden på Experience Platform.

### Visa operativa dataobjekt {#view-operational-data-objects}

Beroende på din fråga innehåller AI Assistant ytterligare information om data i din sandlåda. Om du vill visa hur svaret på din fråga gäller för din specifika sandlåda väljer du **[!UICONTROL In your sandbox].**

När du visar data som gäller din sandlåda kan AI Assistant tillhandahålla direktlänkar till specifika UI-sidor som visar dina efterfrågade data.

+++Markera för att visa exempel

I det här exemplet returnerar AI Assistant ytterligare information om befintliga XDM-scheman i sandlådan, inklusive totalt antal och de fem vanligaste fälten.

![Listrutan &quot;i din sandlåda&quot; öppnas och ytterligare information om dina scheman visas.](./images/in-your-sandbox.png)

+++

### Visa citat {#view-citations}

Du kan verifiera svar som AI Assistant skickat till dig genom att granska citat som finns i varje produktinformationssvar.

+++Markera för att visa ett exempel på hur du visar källor

Om du vill visa citat och validera AI Assistants svar väljer du **[!UICONTROL Show sources]**.

![AI-assistentsvaret med &quot;Visa källor&quot; markerat.](./images/show-sources.png)

AI Assistant uppdaterar gränssnittet och ger dig länkar till dokumentation som bekräftar det ursprungliga svaret. När citat är aktiverat uppdaterar AI Assistant svaret så att det innehåller fotnoter som anger vilka delar av svaret som refererar till den angivna dokumentationen.

![En listruta med de citat som AI Assistant tillhandahåller för konceptfrågor.](./images/citations.png)

+++

### Driftsinsikter {#operational-insights}

Du måste vara i en aktiv sandlåda för att AI Assistant ska kunna svara tillräckligt på en fråga om dina operativa insikter.

+++Välj för att visa ett exempel på en fråga om driftsinsikter

I exemplet nedan tillfrågas följande om AI Assistant: **Visa dataflöden som har skapats med Amazon S3-källan**.

![En fråga om driftsinsikter.](./images/op-insights-question.png)

AI Assistant svarar sedan med en tabell över dina dataflöden och deras motsvarande ID:n. Om du vill visa hela datatabellen väljer du ikonen Expandera högst upp till höger.

![Ett svar på användbara insikter](./images/op-insights-answer.png)

En utökad vy av tabellen visas med en mer omfattande lista över dataflöden baserat på parametrarna för frågan.

![En vy av den utökade tabellen.](./images/table.png)

När AI Assistant tillfrågas om driftsinsikter kan den förklara hur svaret har beräknats. I exemplet nedan visar AI Assistant de steg som har vidtagits för att identifiera dataflödena som skapades med källan [!DNL Amazon S3].

![AI Assistant ger en förklaring av hur svaret beräknades.](./images/answer-explained.png)

Du kan även lägga till filter och ändringar i dina frågor och du kan instruera AI Assistant att återge resultatet baserat på de filter som du inkluderar. Du kan till exempel be AI Assistant att visa en trend för antalet segmentdefinitioner i den ordning som de skapades, ta bort segmentdefinitioner med noll som summor och använda namn på månader i stället för heltal när data visas.

**Obs!** Svaren om driftsinsikter finns för närvarande i betaversion. Klicka på verktygstipsikonen i AI Assistant-användargränssnittet för att visa Beta-meddelandet och för en länk till dokumentationen.

![AI Assistant-verktygstipsikonen har valts.](./images/op-insights-beta-note.png)

+++

### Verifiera svar från operativa insikter {#verify-responses}

Du kan verifiera varje svar som rör frågor om driftsinsikter med hjälp av en SQL-fråga som AI Assistant tillhandahåller.

+++Välj för att visa exempel på verifiering av svar på operativa insikter

När du har fått ett svar på en fråga om driftsinsikter väljer du **[!UICONTROL Show sources]** och sedan **[!UICONTROL View source query]**.

![visa källfråga](./images/view-source-query.png)

När AI Assistant får en fråga om driftsinsikter kan du använda den för att verifiera processen som tog att beräkna svaret. Den här källfrågan är endast avsedd för verifiering och stöds inte av frågetjänsten.

![exempel på källfråga](./images/source-query.png)

+++

### Använd enhet som slutförs automatiskt {#use-entity-auto-complete}

Du kan använda funktionen för automatisk komplettering för att ta emot en lista med dataobjekt som finns i din sandlåda. Rekommendationer som fylls i automatiskt finns tillgängliga för följande domäner: målgrupper, scheman, datamängder, resor, källor och destinationer.

+++Markera för att visa ett exempel på automatisk komplettering

Du kan använda Fyll i automatiskt genom att ta med plustecknet (**`+`**) i frågan. Du kan också välja plustecknet (**`+`**) längst ned i textrutan. Ett fönster visas med en lista över rekommenderade dataobjekt från sandlådan.

![Exempel på automatisk komplettering](./images/autocomplete.png)

+++

### Använda flera omgångar {#use-multi-turn}

Du kan använda AI Assistants multibläddringsfunktioner för att få en mer naturlig konversation under upplevelsen. AI Assistant kan besvara uppföljningsfrågor. det sammanhanget kan härledas från en tidigare interaktion.

+++Markera för att visa ett exempel på flera omgångar

I exemplet nedan ombeds AI Assistant först att ange det totala antalet dataflöden och sedan ombeds att ange en lista över de 10 senaste dataflödena.

![Exempel på multitur](./images/multiturn.png)

+++

### Starta en ny konversation

Du kan ändra ämnen med AI Assistant genom att återställa och starta en ny konversation.

+++Välj för att visa ett exempel på hur du återställer konversationen

Återställ genom att markera ellipserna (**`...`**) i AI Assistant-gränssnittet och sedan välja **[!UICONTROL Start new conversation]**. Detta informerar AI Assistant om att du avser att ändra ämnen och kan vara särskilt användbart vid felsökning av frågor som antingen är felaktiga eller refererar till felaktig information.

![De markerade ellipserna och alternativet för att starta ny konversation har valts.](./images/reset.png)

+++

### Använd identifiering {#use-discoverability}

Du kan använda AI Assistants identifieringsfunktion för att visa en lista över allmänna ämnen, grupperade i entiteter, som AI Assistant stöder.

+++Markera för att visa exempel på identifierbarhet

Om du vill visa upptäckbarhet väljer du glödlampsikonen i det övre huvudet i AI Assistant-gränssnittet.

![Identifieringsfunktionen för AI-assistenten.](./images/lightbulb.png)

Välj sedan en kategori och välj en fråga i listan. Du kan använda den här funktionen för att få en bättre uppfattning om vilka typer av frågor som AI Assistant kan svara på. Du kan även uppdatera befintliga uppmaningar med specifik information som gäller din sandlåda med fritext eller [autofyll](#use-auto-complete).

![AI-assistenten uppmanar till identifiering.](./images/prompt.png)

+++

### Använd automatisk ifyllning av fråga {#use-question-autocomplete}

Du kan använda funktionen för automatisk komplettering av frågor i AI Assistant för att välja en fråga från en lista med rekommendationer från AI Assistant.

+++Markera för att visa ett exempel på automatisk ifyllning av fråga

Om du vill visa panelen med förslag på frågor skriver du minst sju (7) tecken i indatarutan. Välj sedan den fråga som är relevant för dig på menyn som visas.

![Popup-panelen med förslag på frågor från AI Assistant.](./images/suggested_questions.png)

Du kan behöva uppdatera platshållare i vissa fall där en föreslagen fråga innehåller operativa insikter. Du kan till exempel behöva lägga till det specifika namnet för en datauppsättning eller en målgrupp om AI Assistant-förslaget innehåller platshållare.

![Ett förslag från AI Assistant som innehåller platshållare.](./images/placeholder.png)

Platshållare markeras med blått. Markera platshållaren för att börja uppdatera värdet. Du får bäst resultat om du använder siffror i stället för text på numeriska platshållare. Du kan också använda funktionen för automatisk komplettering av entiteten för att uppdatera platshållarvärdena. Du kan inte skicka en fråga som har ofyllda platshållare.

**OBS!**: Förslag är aktiverade som standard. Välj **[!UICONTROL Suggest ideas]** för att inaktivera funktionen.

![Ett förslag från AI Assistant med uppdaterade platshållare.](./images/updated_placeholder.png)

+++

### Använd relaterade förslag {#use-related-suggestions}

Du kan använda avsnittet med relaterade förslag i varje AI Assistant-svar för att fortsätta konversationen.

+++Markera för att visa exempel på relaterade förslag

Relaterade förslag returneras med alla svar från AI Assistant. Om du vill fortsätta konversationen väljer du något av förslagen i avsnittet med relaterade förslag.

![En lista med relaterade förslag från AI-assistenten.](./images/related_suggestions.png)

På samma sätt som platshållarna i fråga fyller i automatiskt måste du uppdatera platshållare som ingår i relaterade förslag innan du kan skicka frågan.

![En fråga från relaterade förslag med platshållarna uppdaterade.](./images/related_suggestions_placeholder.png)

+++

## Ge feedback {#feedback}

Du kan ge återkoppling om din upplevelse med AI Assistant med hjälp av alternativen i svaret.

Om du vill ge feedback väljer du antingen tummen uppåt, tummen nedåt eller en flagga när du har fått ett svar från AI-assistenten och anger sedan din feedback i textrutan.

![Återbetalningsalternativet i AI Assistant.](./images/provide-feedback.png)

+++Markera för att visa fler exempel

>[!BEGINTABS]

>[!TAB Tummen uppåt]

Välj ikonen med tummen uppåt för att ge feedback på vad som gick bra med din upplevelse av AI-assistenten.

![Fönstret för positiv feedback.](./images/thumbs-up.png)

>[!TAB Tummen nere]

Välj ikonen med reglaget nedåt för att ge feedback på vad som kan förbättras baserat på din erfarenhet av AI Assistant. Under det här steget kan du även ge specifika kommentarer om din upplevelse. Synpunkter i kommentarerna granskas dagligen.

![Fönstret för negativ feedback.](./images/thumbs-down.png)

>[!TAB Flagga]

Välj flaggikonen om du vill visa fler rapporter om din upplevelse med hjälp av AI-assistenten.

![Rapportresultatfönstret.](./images/flag.png)

>[!ENDTABS]

+++
