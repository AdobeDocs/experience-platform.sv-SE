---
keywords: Experience Platform;hem;populära ämnen;kantsegmentering;Segmentering;Segmenteringstjänst;segmenteringstjänst;ui guide;streaming edge;
solution: Experience Platform
title: Användargränssnittshandbok för kantsegmentering
topic-legacy: ui guide
description: Kantsegmentering är möjligheten att utvärdera segment i plattformen direkt, vilket möjliggör användning av samma sida och nästa sida.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 6bb1f417b5856f153adebe4deaac4fab264ef3a8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Användargränssnittsguide för kantsegmentering (beta)

>[!IMPORTANT]
>
>Kantsegmentering är för närvarande en betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Kantsegmentering är möjligheten att omedelbart utvärdera segment i Adobe Experience Platform [på kanten](../../edge/home.md), vilket möjliggör användning av samma sida och nästa sida vid personalisering.

## Frågetyper för kantsegmentering

För närvarande kan endast utvalda frågetyper utvärderas med kantsegmentering. I följande avsnitt finns en lista med frågetyper som kan utvärderas med kantsegmentering och de som för närvarande inte stöds.

### Frågetyper som stöds

En fråga kan utvärderas med kantsegmentering om den uppfyller något av villkoren i följande tabell.

>[!NOTE]
>
>Om frågan matchar någon av frågetyperna i följande tabell utvärderas den automatiskt med kantsegmentering. Den här funktionen bestäms automatiskt av systemet baserat på frågeuttrycket.

| Frågetyp | Detaljer | Exempel |
| ---------- | ------- | ------- |
| Inkommande träff | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Inkommande träde som refererar till en profil | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Inkommande träff med ett tidsfönster på 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse inom 24 timmar |  |
| Inkommande träde som refererar till en profil med ett tidsfönster på 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse inom 24 timmar och ett eller flera profilattribut |  |

### Frågetyper stöds inte för närvarande

Följande frågetyper är **inte** som stöds för kantsegmentering:

| Frågetyp | Detaljer |
| ---------- | ------- |
| Flera händelser | Om en fråga innehåller mer än en händelse kan den inte utvärderas med kantsegmentering. |
| Frekvensfråga | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger. |  |
| Frekvensfråga som refererar till en profil | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger och har ett eller flera profilattribut. |  |

## Nästa steg

Den här guiden förklarar hur du utvärderar segment med kantsegmentering på Adobe Experience Platform. Mer information om hur du använder användargränssnittet i Experience Platform finns i [användarhandboken för segmentering](./overview.md). Om du vill lära dig att utföra liknande åtgärder och arbeta med segment med hjälp av API:er för Experience Platform går du till [API-guiden för kantsegmentering](../api/edge-segmentation.md).
