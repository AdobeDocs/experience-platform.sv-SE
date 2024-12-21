---
solution: Experience Platform
title: Användargränssnittshandbok för segmentering i Edge
description: Lär dig hur du använder kantsegmentering för att utvärdera segmentdefinitioner i plattformar direkt, vilket möjliggör användning av samma sida och nästa sidpersonalisering.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 828a586f0264147676da5c43c73d3b3b9d50b9c2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Användargränssnittsguide för Edge-segmentering

>[!NOTE]
>
>Edge segmentering är nu allmänt tillgängligt för alla plattformsanvändare. Om du skapade definitioner för kantsegment under betaversionen kommer dessa segmentdefinitioner att fortsätta att fungera.

Edge-segmentering är möjligheten att omedelbart utvärdera segment i Adobe Experience Platform [på kanten](../../web-sdk/home.md), vilket möjliggör användning av samma sida och nästa sida vid personalisering.

>[!IMPORTANT]
>
> Kantdata lagras på en edge-serverplats som ligger närmast den plats där de samlades in och kan lagras på en annan plats än den som anges som Adobe Experience Platform datacenter (eller huvudserver).
>
> Dessutom kommer kantsegmenteringsmotorn endast att efterleva begäranden på kanten där det finns **en** primär markerad identitet, vilket är förenligt med icke-kantbaserade primära identiteter.

## Edge segmenteringsfrågetyper {#query-types}

För närvarande kan endast utvalda frågetyper utvärderas med kantsegmentering. I följande avsnitt finns en lista med frågetyper som kan utvärderas med kantsegmentering och de som för närvarande inte stöds.

En fråga kan utvärderas med kantsegmentering om den uppfyller något av villkoren i följande tabell.

>[!NOTE]
>
>Om frågan matchar någon av frågetyperna i följande tabell utvärderas den automatiskt med kantsegmentering. Den här funktionen bestäms automatiskt av systemet baserat på frågeuttrycket.

| Frågetyp | Information |
| ---------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. |
| En händelse i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. |
| En händelse med ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse med ett tidsfönster. |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |
| En händelse med ett profilattribut inom ett relativt tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse, med ett eller flera profilattribut, och som inträffar inom ett relativt tidsfönster på mindre än 24 timmar. |
| Segmentering | En segmentdefinition som innehåller en eller flera gruppdefinitioner eller definitioner för direktuppspelade segment. **Obs!** Om segmentet används med **batch**-segmentdefinitioner kan det ta **upp till 24 timmar** att diskvalificera profilen. Om segment används med segmentdefinitioner för **direktuppspelning**, kommer profilinaktiveringen att ske på ett direktuppspelningssätt. |
| Flera händelser med ett profilattribut | Alla segmentdefinitioner som refererar till flera icke-sekventiella händelser **under de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. |

En segmentdefinition kommer **inte** att aktiveras för kantsegmentering i följande scenario:

- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment`-händelse.
   - Om segmentdefinitionen i `inSegment`-händelsen bara är en profil aktiveras segmentdefinitionen **** för kantsegmentering.
- I segmentdefinitionen används&quot;Ignorera år&quot; som en del av tidsbegränsningarna.

## Nästa steg

Den här guiden förklarar hur du utvärderar segmentdefinitioner med kantsegmentering i Adobe Experience Platform. Mer information om hur du använder användargränssnittet i Experience Platform finns i [användarhandboken för segmentering](./overview.md). Om du vill lära dig hur du utför liknande åtgärder och arbetar med segmentdefinitioner med hjälp av API:er för Experience Platform går du till [API-guiden för kantsegmentering](../api/edge-segmentation.md).

## Bilaga

I följande avsnitt visas vanliga frågor om kantsegmentering:

### Hur lång tid tar det innan en segmentdefinition är tillgänglig på Edge Network?

Det tar upp till en timme innan en segmentdefinition är tillgänglig på Edge Network.
