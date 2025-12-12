---
title: Webbtilläggsflöde
description: Lär dig hur webbtilläggskomponenter interagerar med varandra vid körning i Adobe Experience Platform.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Webbtilläggsflöde

I webbtillägg har varje händelse, villkor, åtgärd och dataelementtyp både en vy där användarna kan ändra inställningar och en biblioteksmodul för att agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets händelsetyp inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Användaren använder sedan vyn för att ändra inställningar som sedan sparas i Experience Platform. När biblioteket för tagg-körning skapas inkluderas både tilläggets biblioteksmodul för händelsetyp och de användardefinierade inställningarna i körningsbiblioteket. Under körningen matar Experience Platform in de användardefinierade inställningarna i biblioteksmodulen.

![tilläggsflödesdiagram](../images/flow/web/extension-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![regelbearbetningsflödesdiagram](../images/flow/web/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoden `settings` och `trigger` tillhandahålls till händelsebiblioteksmodulen vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Taggar skickar `settings` till regelns villkorsbiblioteksmoduler där villkor utvärderas.
1. Varje villkorsbiblioteksmodul returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns utförs regelns åtgärder.
