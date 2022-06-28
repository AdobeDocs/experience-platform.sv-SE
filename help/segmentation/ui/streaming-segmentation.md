---
keywords: Experience Platform;hemmabruk;populära ämnen;strömmande segmentering;Segmentering;Segmenteringstjänst;segmenteringstjänst;ui guide;
solution: Experience Platform
title: Användargränssnittshandbok för direktuppspelningssegmentering
topic-legacy: ui guide
description: Med direktuppspelningssegmentering på Adobe Experience Platform kan ni segmentera i nära realtid samtidigt som ni fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificering allt eftersom data når plattformen, vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till plattformen, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 4022eb62e791282bb519f9604b6edf903d69239f
workflow-type: tm+mt
source-wordcount: '1287'
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
>Dessutom kan segment som utvärderas med direktuppspelningssegmentering avvika från det idealiska och det faktiska medlemskapet om segmentet är baserat på ett annat segment som utvärderas med gruppsegmentering. Om till exempel segment A är baserat på segment B och segment B utvärderas med gruppsegmentering, eftersom segment B bara uppdateras var 24:e timme, kommer segment A att flyttas längre bort från de faktiska data tills det synkroniseras om med segmentet B.

## Frågetyper för direktuppspelningssegmentering {#query-types}

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om att aktivera schemalagd segmentering finns i [avsnittet för direktuppspelningssegmentering i användarhandboken för segmentering](./overview.md#scheduled-segmentation).

En fråga utvärderas automatiskt med direktuppspelningssegmentering om den uppfyller något av följande kriterier:

| Frågetyp | Detaljer | Exempel |
| ---------- | ------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| En händelse i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| En händelse med ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse med ett tidsfönster. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |  |
| En händelse med ett profilattribut | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. **Obs!** Frågan utvärderas omedelbart när händelsen kommer. Om en profilhändelse inträffar måste den dock vänta i 24 timmar för att införlivas. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| En händelse med ett profilattribut i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse och ett eller flera profilattribut. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. **Obs!** Om ett segment används, diskvalificeras profilen **var 24:e timme**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Flera händelser med ett profilattribut | En segmentdefinition som refererar till flera händelser **inom de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

En segmentdefinition **not** aktiveras för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).

Observera att följande riktlinjer gäller vid direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Ett strikt tidsordningsvillkor **måste** finns mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **inte** vara en negation.</li></ul> |

Om en segmentdefinition ändras så att den inte längre uppfyller villkoren för direktuppspelningssegmentering, kommer segmentdefinitionen automatiskt att växla från&quot;direktuppspelning&quot; till&quot;Gruppering&quot;.

Dessutom sker okvalificerat segment, på samma sätt som segmentkvalificering, i realtid. Om en publik inte längre kvalificerar sig för ett segment blir det därför omedelbart okvalificerat. Om segmentdefinitionen till exempel frågar efter&quot;Alla användare som har köpt röda skor de senaste tre timmarna&quot;, efter tre timmar, kommer alla profiler som ursprungligen kvalificerades för segmentdefinitionen att vara okvalificerade.

## Segmentdetaljer för direktuppspelning

När du har skapat ett direktuppspelningsaktiverat segment kan du visa information om det segmentet.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Mer om **[!UICONTROL total qualified audience size]** visas. The **[!UICONTROL Total qualified audience size]** visar det totala antalet kvalificerade målgrupper från den senaste slutförda körningen av segmentjobb. Om ett segmentjobb inte slutfördes inom de senaste 24 timmarna hämtas antalet målgrupper från en uppskattning i stället.

Under är ett linjediagram som visar antalet segment som kvalificerats och diskvalificerats under de senaste 24 timmarna. Listrutan kan justeras så att den visar de senaste 24 timmarna, den senaste veckan eller de senaste 30 dagarna.

>[!NOTE]
>
>Ett segment anses vara kvalificerat om det går från att ha ingen status till att realisera eller om det går från att avslutas till att realiseras. Ett segment betraktas som icke-kvalificerat om det går från realiserad till avslutad eller från befintlig till avslutad.
>
>Mer information om de här statusvärdena finns i statustabellen i [segmenteringsöversikt](./overview.md#browse).

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Du hittar mer information om den senaste utvärderingen av segment genom att välja informationsbubblan.

![](../images/ui/streaming-segmentation/info-bubble.png)

Mer information om segmentdefinitioner finns i föregående avsnitt om [segmentdefinitionsinformation](#segment-details).

## Nästa steg

Den här användarhandboken förklarar hur definitioner av direktuppspelningsaktiverade segment fungerar på Adobe Experience Platform och hur man övervakar direktuppspelningsaktiverade segment.

Läs mer om Adobe Experience Platform användargränssnitt i [Användarhandbok för segmentering](./overview.md).

## Bilaga

I följande avsnitt visas vanliga frågor om direktuppspelningssegmentering:

### Händer direktuppspelningssegmentering&quot;utan kvalificering&quot; också i realtid?

I de flesta fall sker icke-kvalificering av direktuppspelad segmentering i realtid. Det gör emellertid direktuppspelningssegment som använder segment av segment **not** diskvalificera i realtid, utan att kvalificera sig efter 24 timmar.

### Vilka data fungerar direktuppspelningssegmentering på?

Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering. Händelser som direktuppspelas i systemet med en tidsstämpel som är äldre än 24 timmar kommer att bearbetas i det efterföljande batchjobbet.

### Hur definieras segment som grupp- eller direktuppspelningssegmentering?

Ett segment definieras som antingen batch- eller direktuppspelningssegmentering baserat på en kombination av frågetyp och händelsehistorikens varaktighet. En lista över vilka segment som ska utvärderas som ett direktuppspelningssegment finns i [frågetyper för direktuppspelningssegmentering](#query-types).

### Kan en användare definiera ett segment som gruppsegmentering eller direktuppspelningssegmentering?

För närvarande kan användaren inte definiera om ett segment ska utvärderas med hjälp av batch- eller direktuppspelningsinmatning, eftersom systemet automatiskt avgör vilken metod segmentet ska utvärderas med.

### Varför ökar antalet&quot;totala kvalificerade&quot; segment medan antalet under&quot;De senaste X dagarna&quot; är noll i segmentinformationsavsnittet?

Antalet kvalificerade segment baseras på det dagliga segmenteringsjobbet, som omfattar målgrupper som är kvalificerade för både batch- och direktuppspelningssegment. Detta värde visas för både grupp- och direktuppspelningssegment.

Numret under de senaste X dagarna **endast** omfattar målgrupper som är kvalificerade för direktuppspelningssegmentering, och **endast** ökar om du har direktuppspelade data i systemet och den räknas in i den direktuppspelningsdefinitionen. Detta värde är **endast** visas för direktuppspelningssegment. Detta resulterar i att detta värde **kan** visas som 0 för gruppsegment.

Om du ser att talet under&quot;De senaste X dagarna&quot; är noll och linjediagrammet också visar noll, har du **not** strömmade alla profiler till systemet som skulle vara kvalificerade för det segmentet.