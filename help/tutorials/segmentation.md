---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Självstudiekurser för segmentering
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån kundprofildata i realtid. Dessa segment är centralt konfigurerade och underhållna på Platform och är tillgängliga för alla Adobe-lösningar.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Självstudiekurser för segmentering

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile]-data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar. Läs [Översikt över segmenteringstjänsten](../segmentation/home.md) om du vill veta mer om segmentering.

## Skapa en segmentdefinition

En segmentdefinition är den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden hos en målgrupp. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment. Du kan utveckla, testa, förhandsgranska och spara en segmentdefinition med användargränssnittet eller API:erna för [!DNL Platform]. Om du vill skapa en segmentdefinition följer du [självstudiekursen ](../segmentation/tutorials/create-a-segment.md) eller [användarhandboken för Segment Builder](../segmentation/ui/overview.md).

## Utvärdera ett segment och få åtkomst till resultat

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering. Med en schemalagd utvärdering (även kallat schemalagd segmentering) kan du skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan en segmentutvärdering innebär att du skapar en målgrupp direkt. Om du vill veta mer kan du gå till självstudiekursen för [utvärdering och åtkomst av segmentresultat](../segmentation/tutorials/evaluate-a-segment.md).

## Exportera segmentdata

För att kunna exportera segment som innehåller [!DNL Profile]-data måste du först [skapa en datauppsättning som data ska exporteras till](../segmentation/tutorials/create-dataset-export-segment.md) och sedan starta ett nytt exportjobb. Steg för att skapa ett exportjobb finns i självstudiekursen [där ett segment](../segmentation/tutorials/evaluate-a-segment.md) utvärderas.

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanfogar dessa data är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Om du vill arbeta med sammanfogningsprinciper i användargränssnittet för [!DNL Platform] går du till [användarhandboken för sammanfogningsprinciper](../profile/ui/merge-policies.md). Mer information om hur du arbetar med sammanfogningsprinciper med hjälp av API:t [!DNL Real-time Customer Profile] finns i [utvecklarhandboken för sammanfogningsprinciper](../profile/api/merge-policies.md).

## Stärk regelefterlevnaden för datasegment

Segment som är aktiverade för användning i [!DNL Real-time Customer Profile] innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen [för efterlevnad av gällande regler för dataanvändning för segment](../segmentation/tutorials/governance.md) för att se hur ni kontrollerar att data används för ett målgruppssegment.

## Direktuppspelningssegmentering

Direktuppspelningssegmentering är möjligheten att omedelbart utvärdera en kund så snart en händelse kommer in i en viss segmentgrupp. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till Adobe Experience Platform, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs. Mer information finns i [översikten över direktuppspelningssegmentering](../segmentation/api/streaming-segmentation.md).

## Segmentering för flera enheter

Multientitetssegmentering är möjligheten att utöka [!DNL Profile]-data med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i [!DNL Profile]-schemat. Mer information om hur du flyttar finns i [dokumentationen om segmentering av flera enheter](../segmentation/multi-entity-segmentation.md).
