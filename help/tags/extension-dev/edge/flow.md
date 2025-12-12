---
title: Edge Extension Flow
description: Lär dig hur komponenterna i ett kanttillägg i Adobe Experience Platform interagerar med varandra vid körning.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Edge-tilläggsflöde

I edge-tillägg har varje villkor, åtgärd och dataelementtyp både en vy som gör att användare kan ändra inställningar och en biblioteksmodul kan agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets åtgärdstypvy inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Vyn används sedan för att ändra inställningar som sedan sparas i Experience Platform. När taggens körtidsbibliotek skapas inkluderas både tilläggets åtgärdstypbiblioteksmodul och de användardefinierade inställningarna i körningsbiblioteket som distribueras till edge-noden. Användardefinierade inställningar från Experience Platform injiceras i biblioteksmodulen vid körning.

![tilläggsflödesdiagram](../images/flow/edge/event-processing-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![regelbearbetningsflödesdiagram](../images/flow/edge/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoden `settings` och `trigger` tillhandahålls till händelsebiblioteksmodulen vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Experience Platform skickar `settings` till regelns biblioteksmoduler av typen condition där villkoren sedan utvärderas.
1. Varje villkorstyp returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns utförs regelns åtgärder.
