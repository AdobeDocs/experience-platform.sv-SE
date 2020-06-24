---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för segmentering
topic: tutorial
translation-type: tm+mt
source-git-commit: b0ef50e25c27aba121bb01c602867953eb2a5f7e
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Självstudiekurser för segmentering

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån kundprofildata i realtid. Dessa segment konfigureras och underhålls centralt på Platform och är tillgängliga via alla Adobes lösningar. Om du vill veta mer om segmentering börjar du med att läsa översikten över [segmenteringstjänsten](../segmentation/home.md).

## Skapa en segmentdefinition

En segmentdefinition är den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden hos en målpublik. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment. Du kan utveckla, testa, förhandsgranska och spara en segmentdefinition med Platform användargränssnitt eller API:er. Om du vill skapa en segmentdefinition följer du [självstudiekursen](../segmentation/tutorials/create-a-segment.md) för att skapa ett segment eller användarhandboken för [segmentbyggaren](../segmentation/ui/overview.md).

## Utvärdera ett segment och få åtkomst till resultat

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering. Med en schemalagd utvärdering (även kallat schemalagd segmentering) kan du skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan en segmentutvärdering innebär att du skapar en målgrupp direkt. Mer information finns i självstudiekursen för [utvärdering och åtkomst av segmentresultat](../segmentation/tutorials/evaluate-a-segment.md).

## Exportera segmentdata

För att kunna exportera segment som innehåller profildata måste du först [skapa en datauppsättning som data ska exporteras](../segmentation/tutorials/create-dataset-export-segment.md)till och sedan starta ett nytt exportjobb. Steg för att generera ett exportjobb finns i [export-API-självstudiekursen](../segmentation/tutorials/export-data.md).

## Konfigurera sammanslagningsprinciper

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som Platform använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Gå till användarhandboken för [sammanfogningspolicyer om du vill arbeta med sammanfogningspolicyer i Platform-användargränssnittet](../profile/ui/merge-policies.md). Om du vill arbeta med sammanfogningsprinciper med hjälp av API:t för kundprofil i realtid läser du i utvecklarhandboken för [sammanfogningsprinciper](../profile/api/merge-policies.md).

## Stärk regelefterlevnaden för datasegment

Segment som har aktiverats för användning i kundprofilen i realtid innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen för [regelefterlevnad för segment](../segmentation/tutorials/governance.md)om du vill få en mer detaljerad genomgång av hur dataanvändningen efterlevs för ett målgruppssegment.

## Direktuppspelningssegmentering

Direktuppspelningssegmentering är möjligheten att omedelbart utvärdera en kund så snart en händelse kommer in i en viss segmentgrupp. Med den här funktionen kan de flesta segmentregler utvärderas när data skickas till Adobe Experience Platform, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs. Mer information finns i översikten över [direktuppspelningssegmentering](../segmentation/api/streaming-segmentation.md).

## Segmentering för flera enheter

Multientitetssegmentering är möjligheten att utöka profildata med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i profilschemat. Mer information om hur du flyttar finns i dokumentationen [om segmentering av](../segmentation/multi-entity-segmentation.md)flera enheter.