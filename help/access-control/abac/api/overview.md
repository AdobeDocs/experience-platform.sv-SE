---
keywords: Experience Platform;hem;populära ämnen;api;attributbaserad åtkomstkontroll;Attributbaserad åtkomstkontroll
solution: Experience Platform
title: Attributbaserad API-guide för åtkomstkontroll
description: Med det attributbaserade API:t för åtkomstkontroll kan du programmässigt hantera roller och åtkomstprinciper i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# API-guide för attributbaserad åtkomstkontroll

Attributbaserad åtkomstkontroll är en funktion i Adobe Experience Platform som gör att administratörer kan styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Det attributbaserade API:t för åtkomstkontroll används för att komma åt roller, produkter, behörighetskategorier och behörighetsgrupper i Adobe Experience Platform, vilket ger ett användargränssnitt och RESTful API som ger åtkomst till alla tillgängliga biblioteksresurser.

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll ska inte blandas ihop med Experience Platform datastyrningsfunktioner, som gör att du kan använda etiketter och policyer för att styra hur data används i plattformar i stället för vilka användare i organisationen har tillgång till dem. Se [API-guide för principtjänst](../../../data-governance/api/overview.md) för steg om hur du programmässigt utnyttjar dessa funktioner.

Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

## Roller

Roller definierar åtkomsten som en administratör, en specialist eller en slutanvändare har till resurser i organisationen. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver. Se [rollslutpunktshandbok](./roles.md) om du vill ha mer information om hur du arbetar med roller i API:t.

## Policyer

Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler. The `/policies` kan du programmässigt hantera principer i organisationen. Se [stödlinje för principslutpunkt](./policies.md) om du vill ha mer information om hur du arbetar med principer i API:t.

## Produkter

The `/products` -slutpunkten i det attributbaserade API:t för åtkomstkontroll gör det möjligt att programmässigt hantera produkter samt behörighetskategorier och behörighetsgrupper som är kopplade till produkter i organisationen. Se [slutpunktsguide för produkter](./products.md) om du vill ha mer information om hur du arbetar med produkter och deras motsvarande behörighetskategorier och behörighetsgrupper i API:t.

## Nästa steg

Om du vill börja ringa anrop med det attributbaserade API:t för åtkomstkontroll läser du [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.
