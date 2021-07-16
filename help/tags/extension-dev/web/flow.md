---
title: Webbtilläggsflöde
description: Lär dig hur webbtilläggskomponenter interagerar med varandra vid körning i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Webbtilläggsflöde

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

I webbtillägg har varje händelse, villkor, åtgärd och dataelementtyp både en vy där användarna kan ändra inställningar och en biblioteksmodul för att agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets händelsetyp inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Användaren använder sedan vyn för att ändra inställningar som sedan sparas inom plattformen. När biblioteket för tagg-körning skapas inkluderas både tilläggets biblioteksmodul för händelsetyp och de användardefinierade inställningarna i körningsbiblioteket. Vid körning matar Platform in de användardefinierade inställningarna i biblioteksmodulen.

![tilläggsflödesdiagram](../images/flow/web/extension-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![flödesdiagram för regelbearbetning](../images/flow/web/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoderna `settings` och `trigger` tillhandahålls till händelsbiblioteket vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Taggar skickar `settings` till regelns villkorsbiblioteksmoduler där villkoren utvärderas.
1. Varje villkorsbiblioteksmodul returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns körs regelns åtgärder.
