---
title: Identiteter och identitetsnamnutrymmen
seo-title: Adobe Experience Platform Identity Service
description: description
seo-description: seo-beskrivning
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Identiteter i CDP i realtid

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att knyta samman identiteter mellan olika enheter och system. Normalt interagerar era kunder med ert varumärke i flera kanaler, vilket kan innebära att ni surfar på er webbplats online, gör ett köp i butiken, går med i ert lojalitetsprogram eller ringer en supportavdelning för att nämna några. I de olika systemen finns det en identitet som skapats för kunden och som gör det möjligt att sammanföra dessa identiteter för att få en helhetsbild. [!DNL Identity Service]

I stället för att nu ha fem separata kunder som interagerar med ert varumärke i fem olika kanaler kan ni se att detta är samma kund, och ni kan se till att de får en enhetlig, personaliserad och relevant upplevelse genom varje interaktion. Efterhand som mer information om kunden (till exempel en anonym webbläsare på er webbplats bestämmer sig för att registrera sig för ett konto och logga in) sammanfogas informationen och kundens bild blir allt tydligare.

## Identitetsnamnutrymmen

Identitetsnamnutrymmen är en komponent i [!DNL Identity Service] och fungerar som indikatorer som ger ytterligare kontext till kundidentiteter. Ett exempel på ett vanligt ID-namnutrymme är&quot;E-post&quot;, där användningen av samma e-postadress på flera webbplatser gör att du kan sammanfoga flera olika identiteter, var och en med ett unikt kund-ID, som i själva verket tillhör samma kund. [!DNL Experience Platform] I kan du använda ID-namnutrymmen för att söka efter enskilda profiler i användargränssnittet. Mer information om visningsprofiler finns i [profilvisningsöversikten](/help/rtcdp/profile/profile-viewer.md). Mer information om namnutrymmen för identiteter finns i översikten över [namnutrymmen](../../identity-service/namespaces.md).

## Identitetsdiagram

Ett identitetsdiagram är en karta över relationer mellan olika identitetsnamnutrymmen, som ger dig en visuell representation av hur kunden interagerar med varumärket i olika kanaler. Alla kundidentitetsdiagram hanteras och uppdateras gemensamt av [!DNL Identity Service] i nära realtid som svar på kundaktivitet.

[!DNL Identity Service] hanterar ett identitetsdiagram som bara är synligt för din organisation och som bygger på dina data, kallas för det privata diagrammet. [!DNL Identity Service] förbättrar det privata diagrammet när en inkapslad datapost innehåller mer än en identitet, vilket lägger till en relation mellan de identifierade identiteterna.

## Nästa steg

Identiteter, och relationerna mellan dem, definieras och upprätthålls av [!DNL Identity Service] och utnyttjas av [!DNL Real-time Customer Profile] för att skapa en fullständig bild av varje enskild kund och deras interaktioner. Mer information finns i [identitetstjänstens dokumentation](../../identity-service/home.md).