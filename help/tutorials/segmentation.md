---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för segmentering
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån kundprofildata i realtid. Dessa segment är centralt konfigurerade och underhållna på Platform och är tillgängliga för alla Adobe-lösningar.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Självstudiekurser för segmentering

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar. Om du vill veta mer om segmentering börjar du med att läsa översikten över [segmenteringstjänsten](../segmentation/home.md).

## Skapa en segmentdefinition

En segmentdefinition är den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden hos en målpublik. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment. Du kan utveckla, testa, förhandsgranska och spara en segmentdefinition med hjälp av [!DNL Platform] användargränssnittet eller API:erna. Om du vill skapa en segmentdefinition följer du [självstudiekursen](../segmentation/tutorials/create-a-segment.md) för att skapa ett segment eller användarhandboken för [segmentbyggaren](../segmentation/ui/overview.md).

## Utvärdera ett segment och få åtkomst till resultat

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering. Med en schemalagd utvärdering (även kallat schemalagd segmentering) kan du skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan en segmentutvärdering innebär att du skapar en målgrupp direkt. Mer information finns i självstudiekursen för [utvärdering och åtkomst av segmentresultat](../segmentation/tutorials/evaluate-a-segment.md).

## Exportera segmentdata

När du exporterar segment som innehåller [!DNL Profile] data måste du först [skapa en datauppsättning som data exporteras](../segmentation/tutorials/create-dataset-export-segment.md)till och sedan starta ett nytt exportjobb. Steg för att generera ett exportjobb finns i självstudiekursen om hur du [utvärderar ett segment](../segmentation/tutorials/evaluate-a-segment.md).

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Om du vill arbeta med kopplingsprofiler i [!DNL Platform] användargränssnittet går du till [användarhandboken](../profile/ui/merge-policies.md)för kopplingsprofiler. Om du vill arbeta med sammanfogningsprinciper med hjälp av API:t läser du i [!DNL Real-time Customer Profile] utvecklarhandboken [](../profile/api/merge-policies.md)för sammanfogningsprinciper.

## Stärk regelefterlevnaden för datasegment

Segment som är aktiverade för användning i [!DNL Real-time Customer Profile] innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen för [regelefterlevnad för segment](../segmentation/tutorials/governance.md)om du vill få en mer detaljerad genomgång av hur dataanvändningen efterlevs för ett målgruppssegment.

## Direktuppspelningssegmentering

Direktuppspelningssegmentering är möjligheten att omedelbart utvärdera en kund så snart en händelse kommer in i en viss segmentgrupp. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till Adobe Experience Platform, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs. Mer information finns i översikten över [direktuppspelningssegmentering](../segmentation/api/streaming-segmentation.md).

## Segmentering för flera enheter

Multientitetssegmentering är möjligheten att utöka [!DNL Profile] data med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i [!DNL Profile] schemat. Mer information om hur du flyttar finns i dokumentationen [om segmentering av](../segmentation/multi-entity-segmentation.md)flera enheter.