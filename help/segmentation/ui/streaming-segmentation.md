---
solution: Experience Platform
title: Användargränssnittshandbok för direktuppspelningssegmentering
description: Med direktuppspelad segmentering på Adobe Experience Platform kan ni segmentera i nära realtid samtidigt som ni fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificering allt eftersom data når plattformen, vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till plattformen, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---

# Direktuppspelningssegmentering

>[!NOTE]
>
>Följande dokument visar hur du använder direktuppspelningssegmentering med användargränssnittet. Mer information om hur du använder direktuppspelningssegmentering med API:t finns i [API-guide för direktuppspelningssegmentering](../api/streaming-segmentation.md).

Direktuppspelningssegmentering på [!DNL Adobe Experience Platform] gör det möjligt för kunderna att segmentera i nära realtid samtidigt som de fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificeringen i takt med att data strömmas in i [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data skickas till [!DNL Platform], vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

>[!NOTE]
>
>Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Data som hämtas in med hjälp av en batchbaserad källa utvärderas nightly, även om de kvalificerar för direktuppspelningssegmentering.
>
>Dessutom kan segment som utvärderas med direktuppspelningssegmentering avvika från det idealiska och det faktiska medlemskapet om segmentdefinitionen baseras på en annan segmentdefinition som utvärderas med gruppsegmentering. Om till exempel segment A är baserat på segment B och segment B utvärderas med gruppsegmentering, eftersom segment B bara uppdateras var 24:e timme, kommer segment A att flyttas längre bort från de faktiska data tills det synkroniseras om med segmentet B.

## Frågetyper för direktuppspelningssegmentering {#query-types}

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om att aktivera schemalagd segmentering finns i [Översikt över Audience Portal](./audience-portal.md#scheduled-segmentation).

En fråga utvärderas automatiskt med direktuppspelningssegmentering om den uppfyller något av följande kriterier:

| Frågetyp | Information | Exempel |
| ---------- | ------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | ![Ett exempel på en enstaka händelse visas.](../images/ui/streaming-segmentation/incoming-hit.png) |
| En händelse i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. | ![Ett exempel på en enstaka händelse i ett relativt tidsfönster visas.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| En händelse med ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse med ett tidsfönster. | ![Ett exempel på en enstaka händelse med ett tidsfönster visas.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. | |
| En händelse med ett profilattribut inom ett relativt tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse, med ett eller flera profilattribut, och som inträffar inom ett relativt tidsfönster på mindre än 24 timmar. | ![Ett exempel på en enstaka händelse med ett profilattribut i ett relativt tidsfönster visas.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. **Obs!** Om ett segment används, diskvalificeras profilen **var 24:e timme**. | ![Ett exempel på ett segment visas.](../images/ui/streaming-segmentation/two-batches.png) |
| Flera händelser med ett profilattribut | En segmentdefinition som refererar till flera händelser **inom de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. | ![Ett exempel på flera händelser med ett profilattribut visas.](../images/ui/streaming-segmentation/event-history-success.png) |

En segmentdefinition **not** aktiveras för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).
- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment` -händelse.
   - Om segmentdefinitionen i `inSegment` -händelsen är bara profil, segmentdefinitionen **kommer** aktiveras för direktuppspelningssegmentering.
- I segmentdefinitionen används&quot;Ignorera år&quot; som en del av tidsbegränsningarna.

Observera att följande riktlinjer gäller vid direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Ett strikt tidsordningsvillkor **måste** finns mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **inte** vara en negation.</li></ul> |

Om en segmentdefinition ändras så att den inte längre uppfyller villkoren för direktuppspelningssegmentering, kommer segmentdefinitionen automatiskt att växla från&quot;direktuppspelning&quot; till&quot;Gruppering&quot;.

Dessutom sker okvalificerat segment, på samma sätt som segmentkvalificering, i realtid. Om en publik inte längre kvalificerar sig för ett segment blir det därför omedelbart okvalificerat. Om segmentdefinitionen till exempel frågar efter&quot;Alla användare som har köpt röda skor de senaste tre timmarna&quot;, efter tre timmar, kommer alla profiler som ursprungligen kvalificerades för segmentdefinitionen att vara okvalificerade.

## Definitionsdetaljer för direktuppspelningssegmentering

När du har skapat ett direktuppspelningsaktiverat segment kan du visa information om det segmentet.

![Sidan med segmentdefinitionsinformation visas.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

I synnerhet **[!UICONTROL Total qualified]** Mätvärdet visas, vilket visar det totala antalet kvalificerade målgrupper baserat på utvärdering av grupper och direktuppspelning för det här segmentet.

Underliggande är ett linjediagram som visar antalet nya målgrupper som uppdaterats under de senaste 24 timmarna med direktuppspelningsmetoden. Listrutan kan justeras så att den visar de senaste 24 timmarna, den senaste veckan eller de senaste 30 dagarna. The **[!UICONTROL New audience updated]** Mätvärdet baseras på förändringen i målgruppens storlek under det valda tidsintervallet, utvärderat genom direktuppspelningssegmentering. Det här måttet inkluderar inte den totala kvalificerade målgruppen från den dagliga grupputvärderingen av segment.

>[!NOTE]
>
>En segmentdefinition anses vara kvalificerad om den går från att ha ingen status till att realisera eller om den går från avslutad till realiserad. En segmentdefinition anses vara okvalificerad om den går från realiserad till avslutad.
>
>Mer information om de här statusvärdena finns i statustabellen i [Översikt över målgruppsportalen](./audience-portal.md#customize).

![Profilerna över tidskortet markeras och visar ett linjediagram över profilerna över tiden.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Mer information om den senaste utvärderingen av segment finns i informationsbubblan bredvid **[!UICONTROL Total qualified]**.

![Informationsbubblan för de totala kvalificerade profilerna har valts. Här visas information om den senaste tiden för segmentutvärdering.](../images/ui/streaming-segmentation/info-bubble.png)

Mer information om segmentdefinitioner finns i föregående avsnitt om [segmentdefinitionsinformation](#segment-details).

## Nästa steg

Den här användarhandboken förklarar hur definitioner av direktuppspelningsaktiverade segment fungerar i Adobe Experience Platform och hur man övervakar direktuppspelningsaktiverade segment.

Läs mer om Adobe Experience Platform användargränssnitt i [Användarhandbok för segmentering](./overview.md).

## Bilaga

I följande avsnitt visas vanliga frågor om direktuppspelningssegmentering:

### Händer direktuppspelad segmentering&quot;utan kvalificering&quot; också i realtid?

I de flesta fall sker icke-kvalificering av direktuppspelad segmentering i realtid. Det gör emellertid direktuppspelningssegment som använder segment av segment **not** diskvalificera i realtid, utan att kvalificera sig efter 24 timmar.

### Vilka data fungerar direktuppspelningssegmentering på?

Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering. Händelser som direktuppspelas i systemet med en tidsstämpel som är äldre än 24 timmar kommer att bearbetas i det efterföljande batchjobbet.

### Hur definieras segment som grupp- eller direktuppspelningssegmentering?

En segmentdefinition definieras som grupp-, direktuppspelnings- eller kantsegmentering baserat på en kombination av frågetyp och händelsehistorikens varaktighet. En lista över vilka segment som ska utvärderas som en segmentdefinition för direktuppspelning finns i [frågetyper för direktuppspelningssegmentering](#query-types).

Observera att om en segmentdefinition innehåller **båda** en `inSegment` -uttryck och en direkt händelsekedja kan den inte kvalificera sig för direktuppspelningssegmentering. Om du vill att den här segmentdefinitionen ska vara giltig för direktuppspelningssegmentering, bör du göra den direkta single-event-kedjan till ett eget segment.

### Varför ökar antalet&quot;totalt kvalificerade&quot; segment medan antalet under&quot;Senaste X dagarna&quot; är noll i avsnittet med segmentdefinitionsdetaljer?

Antalet kvalificerade segment baseras på det dagliga segmenteringsjobbet, som omfattar målgrupper som är kvalificerade för både batch- och direktuppspelningssegment. Detta värde visas för både grupp- och direktuppspelningssegment.

Numret under de senaste X dagarna **endast** omfattar målgrupper som är kvalificerade för direktuppspelningssegmentering, och **endast** ökar om du har direktuppspelade data i systemet och den räknas in i den direktuppspelningsdefinitionen. Det här värdet är **endast** visas för direktuppspelningssegment. Detta resulterar i att detta värde **kan** visas som 0 för gruppsegment.

Om du ser att talet under&quot;De senaste X dagarna&quot; är noll och linjediagrammet också visar noll, har du **not** strömmade alla profiler till systemet som skulle vara kvalificerade för det segmentet.

### Hur lång tid tar det innan en segmentdefinition är tillgänglig?

Det tar upp till en timme innan en segmentdefinition är tillgänglig.

### Finns det några begränsningar för de data som strömmas in?

För att direktuppspelade data ska kunna användas vid direktuppspelningssegmentering finns det **måste** vara mellanrum mellan de händelser som direktuppspelas i. Om för många händelser direktuppspelas inom samma sekund kommer Platform att behandla dessa händelser som robotgenererade data och de kommer att ignoreras. Som bästa praxis bör du ha **minst** fem sekunder mellan händelsedata för att säkerställa att data används på rätt sätt.
