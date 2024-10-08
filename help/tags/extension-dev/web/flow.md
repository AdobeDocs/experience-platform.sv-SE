---
title: Webbtilläggsflöde
description: Lär dig hur webbtilläggskomponenter interagerar med varandra vid körning i Adobe Experience Platform.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Webbtilläggsflöde

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

I webbtillägg har varje händelse, villkor, åtgärd och dataelementtyp både en vy där användarna kan ändra inställningar och en biblioteksmodul för att agera utifrån de användardefinierade inställningarna.

Som framgår av följande högnivådiagram visas tilläggets händelsetyp inuti en iframe i programmet som är integrerat med Adobe Experience Platform. Användaren använder sedan vyn för att ändra inställningar som sedan sparas inom plattformen. När biblioteket för tagg-körning skapas inkluderas både tilläggets biblioteksmodul för händelsetyp och de användardefinierade inställningarna i körningsbiblioteket. Vid körning matar Platform in de användardefinierade inställningarna i biblioteksmodulen.

![tilläggsflödesdiagram](../images/flow/web/extension-flow.png)

I följande diagram ser du länken mellan händelser, villkor och åtgärder i regelbearbetningsflödet.

![regelbearbetningsflödesdiagram](../images/flow/web/rule-processing-flow.png)

Regelbearbetningsflödet innehåller följande faser:

1. Metoden `settings` och `trigger` tillhandahålls till händelsebiblioteksmodulen vid start.
1. När händelsebiblioteksmodulen fastställer att händelsen har inträffat anropar händelsbiblioteket `trigger`.
1. Taggar skickar `settings` till regelns villkorsbiblioteksmoduler där villkor utvärderas.
1. Varje villkorsbiblioteksmodul returnerar om ett villkor utvärderas till true.
1. Om alla villkor godkänns körs regelns åtgärder.
