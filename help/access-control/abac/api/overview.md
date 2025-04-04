---
keywords: Experience Platform;home;populära topics;api;attributbaserad åtkomstkontroll;Attributbaserad åtkomstkontroll
solution: Experience Platform
title: Attributbaserad API-guide för åtkomstkontroll
description: Med det attributbaserade API:t för åtkomstkontroll kan du programmässigt hantera roller och åtkomstprinciper i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# API-guide för attributbaserad åtkomstkontroll

Attributbaserad åtkomstkontroll är en funktion i Adobe Experience Platform som gör att administratörer kan styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Det attributbaserade API:t för åtkomstkontroll används för att komma åt roller, produkter, behörighetskategorier och behörighetsgrupper i Adobe Experience Platform, vilket ger ett användargränssnitt och RESTful API som ger åtkomst till alla tillgängliga biblioteksresurser.

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll ska inte blandas ihop med Experience Platform datastyrningsfunktioner, som gör att du kan använda etiketter och policyer för att styra hur data används i Experience Platform i stället för vilka användare i organisationen som har tillgång till dem. I [API-handboken för principtjänsten](../../../data-governance/api/overview.md) finns anvisningar om hur du använder dessa funktioner programmatiskt.

Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

## Roller

Roller definierar åtkomsten som en administratör, en specialist eller en slutanvändare har till resurser i organisationen. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver. Mer information om hur du arbetar med roller i API finns i [rollslutpunktshandboken](./roles.md).

## Policyer

Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler. Med slutpunkten `/policies` kan du programmässigt hantera principer i din organisation. Mer information om hur du arbetar med principer i API finns i [principslutpunktshandboken](./policies.md).

## Produkter

Med slutpunkten `/products` i det attributbaserade API:t för åtkomstkontroll kan du programmässigt hantera produkter samt behörighetskategorier och behörighetsgrupper som är kopplade till produkter i organisationen. Mer information om hur du arbetar med produkter och deras motsvarande behörighetskategorier och behörighetsgrupper i API:t finns i [produktslutpunktshandboken](./products.md).

## Nästa steg

Om du vill börja ringa anrop med det attributbaserade API:t för åtkomstkontroll läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
