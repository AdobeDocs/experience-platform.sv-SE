---
title: AI Assistant i Adobe Experience Platform
description: Lär dig hur du använder AI Assistant för att navigera bland och förstå koncept för Experience Platform och Real-time Customer Data Platform, samt användningsinformation om dina objekt.
source-git-commit: 0820ba0f14e9eae5d89cd48490b1af5f9afcda70
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Användargränssnittshandbok för AI Assistant

Läs den här guiden och lär dig hur du kan använda AI Assistant i Adobe Experience Platform-gränssnittet.

## Åtkomst till AI-assistenten i användargränssnittet i Experience Platform

Välj alternativet **[!UICONTROL AI Assistant icon]** från Experience Platform översta huvud i användargränssnittet.

![Experience Platform hemsida med ikonen AI Assistant vald och gränssnittet AI Assistant öppet.](./images/ai-assistant.png)

Gränssnittet för AI Assistant visas och du får information om hur du kommer igång direkt. Du kan använda alternativen i [!UICONTROL Ideas to get started] svara på frågor och kommandon som:

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Användargränssnittshandbok för AI Assistant

>[!NOTE]
>
>Följande arbetsflöde är ett exempel som använder processen för att skapa händelseschema för att illustrera hur du kan använda AI Assistant när du använder användargränssnittet i Experience Platform.

Tänk dig ett användningsexempel där du skapar en **Enhetshandel i händelseschema**. När upplevelsehändelsens schema skapades stöter du på `eventType` fält. &quot;Nu kan du välja att antingen avsluta arbetsflödet och se [grunderna i en schemakomposition](../xdm/schema/composition.md) eller så kan du använda AI Assistant för att få svar på dina frågor och hitta ytterligare resurser via de dokumentationslänkar som rekommenderas av AI Assistant.&quot;

Börja med att ange din fråga i textrutan. I exemplet nedan ställs frågan: &quot;**Vad är fältet eventType i ett ExperienceEvent-schema?**&quot;

![AI-assistenten för Experience Platform med följande fråga förberedd för fråga:&quot;Vad är fältet eventType i ett ExperienceEvent-schema?](./images/question.png)

AI Assistant frågar sedan efter sin kunskapsbas och beräknar ett svar. Efter en stund returnerar AI Assistant ett svar och relaterade förslag som du kan använda som uppföljningsuppmaningar.

![AI Assistant för Experience Platform med svar på föregående fråga.](./images/answer.png)

När du har fått ett svar från AI Assistant kan du välja bland ett antal alternativ som avgör hur du vill fortsätta.

### AI Assistant-funktioner {#features}

I det här avsnittet beskrivs de olika funktionerna i AI Assistant som du kan använda i dina arbetsflöden på Experience Platform.

### Visa operativa dataobjekt {#view-operational-data-objects}

Beroende på din fråga innehåller AI Assistant ytterligare information om data i din sandlåda. Om du vill visa hur svaret på frågan gäller för din specifika sandlåda väljer du **[!UICONTROL In your sandbox].**

När du visar data som gäller din sandlåda kan AI Assistant tillhandahålla direktlänkar till specifika UI-sidor som visar dina efterfrågade data.

+++Markera för att visa exempel

I det här exemplet returnerar AI Assistant ytterligare information om befintliga XDM-scheman i sandlådan, inklusive totalt antal och de fem vanligaste fälten.

![Listrutan&quot;i din sandlåda&quot; öppnas och ytterligare information om dina scheman visas.](./images/in-your-sandbox.png)

+++

### Visa citat {#view-citations}

Du kan verifiera svar som AI Assistant skickat till dig genom att granska citat som finns i varje produktinformationssvar.

+++Markera för att visa ett exempel på hur du visar källor

Om du vill visa citat och validera AI Assistants svar väljer du **[!UICONTROL Show sources]**.

![AI Assistant-svaret med Visa källor markerat.](./images/show-sources.png)

AI Assistant uppdaterar gränssnittet och ger dig länkar till dokumentation som bekräftar det ursprungliga svaret. När citat är aktiverat uppdaterar AI Assistant svaret så att det innehåller fotnoter som anger vilka delar av svaret som refererar till den angivna dokumentationen.

![En listruta med de citat som AI Assistant tillhandahåller för konceptfrågor.](./images/citations.png)

Du kan också använda de förslag som AI Assistant ger under **[!UICONTROL Related suggestions]** om du vill utforska ämnen som hör till den ursprungliga frågan.

![En lista med förslag från AI Assistant.](./images/related-suggestions.png)

+++

### Driftsinsikter {#operational-insights}

Du måste vara i en aktiv sandlåda för att AI Assistant ska kunna svara tillräckligt på en fråga om dina operativa insikter.

+++Välj för att visa ett exempel på en fråga om driftsinsikter

I exemplet nedan tillfrågas följande om AI Assistant: **&quot;Visa dataflöden som har skapats med Amazon S3-källa&quot;**, svarar AI Assistant sedan med en tabell över dina dataflöden och deras motsvarande ID:n. Om du vill visa hela datatabellen väljer du ikonen Expandera högst upp till höger.

![Uppföljningsfråga om operativa insikter.](./images/usage-data-question.png)

En utökad vy av tabellen visas med en mer omfattande lista över dataflöden baserat på parametrarna för frågan.

![En vy av den utökade tabellen.](./images/table.png)

När AI Assistant tillfrågas om driftsinsikter kan den förklara hur svaret har beräknats. I exemplet nedan beskriver AI Assistant de steg som har vidtagits för att identifiera de dataflöden som har skapats med [!DNL Amazon S3] källa.

![Uppföljningsfråga om segmentdefinitioner som illustrerar hur AI Assistant beräknade svaret.](./images/answer-explained.png)

Du kan även lägga till filter och ändringar i dina frågor och du kan instruera AI Assistant att återge resultatet baserat på de filter som du inkluderar. Du kan till exempel be AI Assistant att visa en trend för antalet segmentdefinitioner i den ordning som de skapades, ta bort segmentdefinitioner med noll som summor och använda namn på månader i stället för heltal när data visas.

+++

### Använd automatisk komplettering {#use-auto-complete}

Du kan använda funktionen för automatisk komplettering för att ta emot en lista med dataobjekt som finns i din sandlåda. Rekommendationer som fylls i automatiskt finns tillgängliga för följande domäner: målgrupper, scheman, datamängder, källor och destinationer.

+++Markera för att visa ett exempel på automatisk komplettering

Du kan använda Fyll i automatiskt genom att ta med plustecknet (**`+`**) i din fråga. Du kan också välja plustecknet (**`+`**) längst ned i textrutan. Ett fönster visas med en lista över rekommenderade dataobjekt från sandlådan.

![Exempel på automatisk komplettering](./images/autocomplete.png)

+++

### Använda flera omgångar {#use-multi-turn}

Du kan använda AI Assistants multibläddringsfunktioner för att få en mer naturlig konversation under upplevelsen. AI Assistant kan besvara uppföljningsfrågor. det sammanhanget kan härledas från en tidigare interaktion.

+++Markera för att visa ett exempel på flera omgångar

I exemplet nedan ombeds AI Assistant först att ange det totala antalet dataflöden och sedan ombeds att ange en lista över de 10 senaste dataflödena.

![Exempel på multisväng](./images/multi-turn.png)

+++

## Ge feedback {#feedback}

Du kan ge återkoppling om din upplevelse med AI Assistant med hjälp av alternativen i svaret.

Om du vill ge feedback väljer du antingen tummen uppåt, tummen nedåt eller en flagga när du har fått ett svar från AI-assistenten och anger sedan din feedback i textrutan.

![Feedback-alternativet i AI Assistant.](./images/provide-feedback.png)

Om du vill återställa väljer du ellipserna (**`...`**) i AI Assistant-gränssnittet och välj **[!UICONTROL Start new conversation]**. Detta informerar AI Assistant om att du avser att ändra ämnen och kan vara särskilt användbart vid felsökning av frågor som antingen är felaktiga eller refererar till felaktig information.

+++Markera för att visa fler exempel

>[!BEGINTABS]

>[!TAB Tummen upp]

Välj ikonen med tummen uppåt för att ge feedback på vad som gick bra med din upplevelse av AI-assistenten.

![Fönstret för positiv feedback.](./images/thumbs-up.png)

>[!TAB Tummen ned]

Välj ikonen med reglaget nedåt för att ge feedback på vad som kan förbättras baserat på din erfarenhet av AI Assistant. Under det här steget kan du även ge specifika kommentarer om din upplevelse. Synpunkter i kommentarerna granskas dagligen.

![Fönstret för negativ feedback.](./images/thumbs-down.png)

>[!TAB Flagga]

Välj flaggikonen om du vill visa fler rapporter om din upplevelse med hjälp av AI-assistenten.

![Rapportresultatfönstret.](./images/flag.png)

>[!ENDTABS]

+++