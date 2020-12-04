---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Direktuppspelningssegmentering
topic: ui guide
description: Med direktuppspelningssegmentering på Adobe Experience Platform kan ni segmentera i nära realtid samtidigt som ni fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificering allt eftersom data når plattformen, vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till plattformen, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.
translation-type: tm+mt
source-git-commit: 2bd4b773f7763ca408b55e3b0e2d0bbe9e7b66ba
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---


# Direktuppspelningssegmentering

>[!NOTE]
>
>Följande dokument visar hur du använder direktuppspelningssegmentering med användargränssnittet. Mer information om hur du använder direktuppspelningssegmentering med API:t finns i [API-handboken](../api/streaming-segmentation.md)för direktuppspelningssegmentering.

Med direktuppspelningssegmentering på [!DNL Adobe Experience Platform] kan kunderna segmentera i nära realtid samtidigt som de fokuserar på datarikedom. Med direktuppspelningssegmentering sker nu segmentkvalificering som strömmande data når [!DNL Platform]och eliminerar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till [!DNL Platform], vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

>[!NOTE]
>
>Direktuppspelningssegmentering kan bara användas för att utvärdera data som direktuppspelas på plattformen. Med andra ord kommer data som hämtas via batchinmatning inte att utvärderas genom direktuppspelningssegmentering, utan kommer att utvärderas tillsammans med det nightly schemalagda segmenterade jobbet.

## Frågetyper för direktuppspelningssegmentering

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om hur du aktiverar schemalagd segmentering finns [i avsnittet om direktuppspelningssegmentering i användarhandboken](./overview.md#scheduled-segmentation)för segmentering.

En fråga utvärderas automatiskt med direktuppspelningssegmentering om den uppfyller något av följande kriterier:

| Frågetyp | Detaljer | Exempel |
| ---------- | ------- | ------- |
| Inkommande träff | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Inkommande träff inom ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |  |
| Inkommande träde som refererar till en profil | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Inkommande träde som refererar till en profil inom ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse och ett eller flera profilattribut. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Flera händelser som refererar till en profil | Alla segmentdefinitioner som refererar till flera händelser **under de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

En segmentdefinition aktiveras **inte** för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).

Dessutom gäller vissa riktlinjer för direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Det **måste** finnas ett strikt tidsordningsvillkor mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **kan dock inte** vara en negation.</li></ul> |

Om en segmentdefinition ändras så att den inte längre uppfyller villkoren för direktuppspelningssegmentering, kommer segmentdefinitionen automatiskt att växla från&quot;direktuppspelning&quot; till&quot;Gruppering&quot;.

## Segmentdetaljer för direktuppspelning

När du har skapat ett direktuppspelningsaktiverat segment kan du visa information om det segmentet.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Mer information om **[!UICONTROL total qualified audience size]** finns. Här **[!UICONTROL Total qualified audience size]** visas det totala antalet kvalificerade målgrupper från den senaste körningen av segmentjobbet. Om ett segmentjobb inte slutfördes inom de senaste 24 timmarna hämtas antalet målgrupper från en uppskattning i stället.

Under är ett linjediagram som visar antalet segment som kvalificerats och diskvalificerats under de senaste 24 timmarna. Listrutan kan justeras så att den visar de senaste 24 timmarna, den senaste veckan eller de senaste 30 dagarna.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Du hittar mer information om den senaste utvärderingen av segment genom att välja informationsbubblan.

![](../images/ui/streaming-segmentation/info-bubble.png)

Mer information om segmentdefinitioner finns i föregående avsnitt om [segmentdefinitionsdetaljer](#segment-details).

## Film om direktuppspelad segmentering

Följande video är avsedd att ge en bättre förståelse för direktuppspelningssegmentering. Här visas ett exempel på en kundupplevelse följt av en snabb genomgång av de viktigaste funktionerna i [!DNL Platform] gränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Nästa steg

Den här användarhandboken förklarar hur definitioner av direktuppspelningsaktiverade segment fungerar på Adobe Experience Platform och hur man övervakar direktuppspelningsaktiverade segment.

Mer information om hur du använder Adobe Experience Platform användargränssnitt finns i användarhandboken för [segmentering](./overview.md).