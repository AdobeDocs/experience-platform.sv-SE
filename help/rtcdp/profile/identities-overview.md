---
keywords: identiteter rtcdp;rtcdp identiteter;cdp-identiteter i realtid
title: Identiteter i Real-time Customer Data Platform
description: Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att knyta samman identiteter mellan olika enheter och system.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Översikt över identiteter

Adobe Experience Platform [!DNL Identity Service] hjälper dig att få en bättre bild av dina kunder och deras beteende genom att förena identiteter på olika enheter och system. Normalt interagerar era kunder med ert varumärke i flera kanaler, vilket kan innebära att ni surfar på er webbplats online, gör ett köp i butiken, går med i ert lojalitetsprogram eller ringer en supportavdelning för att nämna några. I de här systemen finns det en identitet som skapats för den kunden, och med [!DNL Identity Service] kan du sammanföra dessa identiteter för att se hela bilden.

I stället för att nu ha fem separata kunder som interagerar med ert varumärke i fem olika kanaler kan ni se att detta är samma kund, och ni kan se till att de får en enhetlig, personaliserad och relevant upplevelse genom varje interaktion. Efterhand som mer information om kunden (till exempel en anonym webbläsare på er webbplats bestämmer sig för att registrera sig för ett konto och logga in) sammanfogas informationen och kundens bild blir allt tydligare.

## Identitetsnamnutrymmen

Identitetsnamnutrymmen är en komponent i [!DNL Identity Service] och fungerar som indikatorer som ger ytterligare kontext till kundidentiteter. Ett exempel på ett vanligt ID-namnutrymme är&quot;E-post&quot;, där användningen av samma e-postadress på flera webbplatser gör att du kan sammanfoga flera olika identiteter, var och en med ett unikt kund-ID, som i själva verket tillhör samma kund. I [!DNL Experience Platform] kan du använda ID-namnutrymmen för att söka efter enskilda profiler i användargränssnittet. Mer information om hur du visar profiler finns i [översikten över profilbläddringen](profile-browse.md). Mer information om namnutrymmen för identiteter finns i [översikten över namnutrymmet för identiteter](../../identity-service/features/namespaces.md).

## Identitetsdiagram

Ett identitetsdiagram är en karta över relationer mellan olika identiteter, som ger dig en visuell representation av hur kunden interagerar med ert varumärke i olika kanaler. Alla kundidentitetsdiagram hanteras och uppdateras gemensamt av identitetstjänsten som svar på kundaktivitet.

[!DNL Identity Service] hanterar ett identitetsdiagram som bara är synligt för din organisation och som bygger på dina data. [!DNL Identity Service] utökar diagrammet när en inkapslad datapost innehåller mer än en identitet, vilket lägger till en relation mellan de identifierade identiteterna.

## Nästa steg

Identiteter, och relationerna mellan dem, definieras och underhålls av [!DNL Identity Service] och utnyttjas av [!DNL Real-Time Customer Profile] för att skapa en fullständig bild av varje enskild kund och deras interaktioner. Mer information finns i [identitetstjänstens dokumentation](../../identity-service/home.md).
