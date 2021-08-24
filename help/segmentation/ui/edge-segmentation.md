---
keywords: Experience Platform;hem;populära ämnen;kantsegmentering;Segmentering;Segmenteringstjänst;segmenteringstjänst;ui guide;streaming edge;
solution: Experience Platform
title: Användargränssnittshandbok för kantsegmentering
topic-legacy: ui guide
description: Kantsegmentering är möjligheten att utvärdera segment i plattformen direkt, vilket möjliggör användning av samma sida och nästa sida.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8f2540902cdcff99627393429424dbfe1de2d3da
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Användargränssnittsguide för kantsegmentering (beta)

>[!NOTE]
>
>Kantsegmentering är för närvarande en betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Kantsegmentering är möjligheten att utvärdera segment i Adobe Experience Platform direkt, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

## Frågetyper för kantsegmentering

En fråga kan utvärderas med kantsegmentering om den uppfyller något av följande kriterier:

| Frågetyp | Detaljer | Exempel |
| ---------- | ------- | ------- |
| Inkommande träff | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Inkommande träde som refererar till en profil | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Inkommande träff med ett tidsfönster på 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse inom 24 timmar |  |
| Inkommande träde som refererar till en profil med ett tidsfönster på 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse inom 24 timmar och ett eller flera profilattribut |  |

Om frågan matchar någon av ovanstående frågetyper utvärderas den automatiskt med kantsegmentering.

Följande frågetyper är **inte** som stöds för kantsegmentering:

| Frågetyp | Detaljer |
| ---------- | ------- |
| Flera händelser | Om en fråga innehåller mer än en händelse kan den inte utvärderas med kantsegmentering. |
| Frekvensfråga | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger. |  |
| Frekvensfråga som refererar till en profil | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger och har ett eller flera profilattribut. |  |

## Nästa steg

Den här användarhandboken förklarar hur du utvärderar segment med kantsegmentering på Adobe Experience Platform.

Läs [användarhandboken för segmentering](./overview.md) om du vill veta mer om hur du använder Adobe Experience Platform användargränssnitt. Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du läsa [API-guiden för kantsegmentering](../api/edge-segmentation.md).
