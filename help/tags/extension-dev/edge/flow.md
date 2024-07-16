---
title: Edge Extension Flow
description: Lär dig hur komponenterna i ett kanttillägg i Adobe Experience Platform interagerar med varandra vid körning.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Edge-tilläggsflöde

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

I edge-tillägg har varje villkor, åtgärd och dataelementtyp både en vy som gör att användare kan ändra inställningar och en biblioteksmodul kan agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets åtgärdstypvy inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Vyn används sedan för att ändra inställningar som sedan sparas inom plattformen. När taggens körtidsbibliotek skapas inkluderas både tilläggets åtgärdstypbiblioteksmodul och de användardefinierade inställningarna i körningsbiblioteket som distribueras till edge-noden. Användardefinierade inställningar från Platform matas in i biblioteksmodulen vid körning.

![tilläggsflödesdiagram](../images/flow/edge/event-processing-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![regelbearbetningsflödesdiagram](../images/flow/edge/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoden `settings` och `trigger` tillhandahålls till händelsebiblioteksmodulen vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Plattformen skickar `settings` till regelns biblioteksmoduler av typen condition där villkoren sedan utvärderas.
1. Varje villkorstyp returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns körs regelns åtgärder.
