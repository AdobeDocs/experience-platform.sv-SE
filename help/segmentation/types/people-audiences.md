---
solution: Experience Platform
title: Målgrupper
description: Lär dig målinrikta människor med hjälp av målgrupper.
source-git-commit: d73f8c47f9eedff05446688f0c798c322e51aa5d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Målgruppsguide

I Adobe Experience Platform kan personbaserade målgrupper målinrikta specifika grupper av människor för era marknadsföringskampanjer.

Målgrupper använder kundprofildata för att inrikta sig på specifika marknader, vilket gör att ni bättre kan rikta in er på specifika demografiska data som ni vill annonsera mot.

## Terminologi {#terminology}

Innan du börjar med en publik, se skillnaderna mellan olika typer av målgrupper:

- **Kontomålgrupper**: En kontomålgrupp är en målgrupp som skapas med **konto**-profildata. Kontoprofildata kan användas för att skapa målgrupper som riktar sig till personer i efterföljande konton. Mer information om målgrupper för konton finns i [översikten över målgrupper för konton](./account-audiences.md).
- **Målgrupper**: En målgrupp är en målgrupp som skapas med **kundprofildata**. Kundprofildata kan användas för att skapa målgrupper som riktar sig till företagets kunder.
- **Potentiella målgrupper**: En publik för potentiella kunder är en målgrupp som skapas med **prospekt** profildata. Prospektprofildata kan användas för att skapa målgrupper från oautentiserade användare. Mer information om potentiella målgrupper finns i [översikten över potentiella målgrupper](./prospect-audiences.md).

## Åtkomst {#access}

Om du vill få åtkomst till målgrupper väljer du **[!UICONTROL Audiences]** i avsnittet **[!UICONTROL Customers]**.

![Fliken Publiker är markerad i avsnittet Kunder.](../images/types/people/select-audiences.png)

Audience Portal visas med en lista över alla målgrupper i organisationen.

![Målportalen för målgrupper visas.](../images/types/people/people-audiences.png)

I den här vyn visas information om målgruppen, inklusive namn, antal profiler, ursprung, livscykelstatus, skapat datum och senaste uppdateringsdatum.

Du kan också använda sök- och filtreringsfunktionerna för att snabbt söka efter och sortera efter specifika kontogrupper. Mer information om den här funktionen finns i [Översikt över målportalen](../ui/audience-portal.md#manage-audiences).

## Målgruppsinformation {#details}

Om du vill visa information om en viss målgrupp väljer du en målgrupp på Audience Portal.

![En angiven målgrupp markeras i Audience Portal.](../images/types/people/select-audience.png)

Sidan med målgruppsinformation visas. Information, inklusive beskrivning, ursprung och livscykeltillstånd visas.

![Sidan med målgruppsinformation visas med information om målgruppen.](../images/types/people/audience-details.png)

Mer information om sidan med målgruppsinformation finns i avsnittet [målgruppsinformation i översikten över målgruppsportalen](../ui/audience-portal.md#audience-details).

## Skapa målgrupper {#create}

Du kan skapa en målgrupp med hjälp av Audience Composer eller Segment Builder. Om du vill komma igång med att skapa en målgrupp väljer du Skapa målgrupp på Audience Portal.

![Knappen Skapa målgrupp är markerad.](../images/types/people/select-create-audience.png)

En pover visas där du kan välja mellan att sätta ihop en målgrupp eller skapa regler.

![En pover som visar ett val mellan disposition och målgrupp och byggregler visas.](../images/types/people/create-audience-popover.png)

Mer information om hur du skapar målgrupper finns i översikten över [målgruppsportalen](../ui/audience-portal.md#create-audience).

## Aktivera målgrupp {#activate}

När ni har skapat er målgrupp kan ni aktivera den för andra tjänster längre fram i kedjan.

Välj den målgrupp som du vill aktivera, följt av **[!UICONTROL Activate to destination]**.

![Knappen Aktivera till mål är markerad under snabbåtgärdsmenyn.](../images/types/people/activate-to-destination.png)

Sidan [!UICONTROL Activate destination] visas med en lista över tillgängliga mål beroende på målgruppens uppdateringsfrekvens. Mer information om aktiveringsprocessen finns i [aktiveringsöversikten](../../destinations/ui/activation-overview.md).

## Nästa steg

När du har läst den här guiden kan du skapa och hantera dina målgrupper i Adobe Experience Platform. Läs [översikten över målgruppstyper](./overview.md) om du vill veta mer om de olika typerna av målgrupper.
