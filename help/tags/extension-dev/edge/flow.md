---
title: Edge Extension Flow
description: Lär dig hur komponenterna i ett kanttillägg i Adobe Experience Platform interagerar med varandra vid körning.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Kanttilläggsflöde

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

I edge-tillägg har varje villkor, åtgärd och dataelementtyp både en vy som gör att användare kan ändra inställningar och en biblioteksmodul kan agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets åtgärdstypvy inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Vyn används sedan för att ändra inställningar som sedan sparas inom plattformen. När taggens körtidsbibliotek skapas inkluderas både tilläggets åtgärdstypbiblioteksmodul och de användardefinierade inställningarna i körningsbiblioteket som distribueras till edge-noden. Användardefinierade inställningar från Platform matas in i biblioteksmodulen vid körning.

![tilläggsflödesdiagram](../images/flow/edge/event-processing-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![flödesdiagram för regelbearbetning](../images/flow/edge/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoderna `settings` och `trigger` tillhandahålls till händelsbiblioteket vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Plattformen skickar `settings` till regelns biblioteksmoduler av typen condition där villkoren sedan utvärderas.
1. Varje villkorstyp returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns körs regelns åtgärder.
