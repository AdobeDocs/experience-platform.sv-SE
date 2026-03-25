---
title: Bildskärmssegmentering
description: Lär dig hur du använder kontrollpanelen för övervakning för att observera kantsegmenteringens genomströmning.
source-git-commit: 809f80c721d6eedf5ee88dbb1cf4bf7e5a413614
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Bildskärmssegmentering

Du kan använda kontrollpanelen för övervakning i Adobe Experience Platform-gränssnittet för att övervaka kantsegmentering i realtid inom organisationen. Använd den här funktionen för att få större genomskinlighet i genomströmningen av dina kantdata.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Datastreams](../../datastreams/overview.md): Med datastreams kan du ansluta Experience Platform Edge Network till din datamängd.
* [Kapacitet](../../landing/license-usage-and-guardrails/capacity.md): I Experience Platform kan du få reda på om din organisation har överskridit några av dina skyddsprofiler och du får information om hur du åtgärdar dessa problem.
* [Edge-segmentering](../../segmentation/methods/edge-segmentation.md): Edge-segmentering är möjligheten att omedelbart utvärdera segmentdefinitioner i Adobe Experience Platform [&#x200B; vid kanten](../../landing/edge-and-hub-comparison.md), vilket möjliggör användning av samma sida och nästa sidpersonalisering.

## Åtkomst {#access}

Om du vill få åtkomst till kontrollpanelen för kantsegmenteringsgenomströmning väljer du **[!UICONTROL Monitoring]** i avsnittet **[!UICONTROL Data management]** följt av **[!UICONTROL Edge]**.

![Metoden för att komma åt kontrollpanelen för kantsegmentering av bildskärmar är markerad.](/help/dataflows/assets/ui/monitor-edge/access.png)

Kontrollpanelen visas. Detta visar övervakningsmått för edge streaming-genomströmning, ett diagram som visar hastigheten för edge streaming-genomströmning och en datastream-vy. Dessa mått kan filtreras efter tjänst, kanter och datum.

![Filtreringsalternativen på kontrollpanelen är markerade.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Du kan bara se datastream-vyn **endast** om du väljer [!UICONTROL Edge segmentation throughput].

Om du filtrerar efter tjänst kan du välja vilken tjänst du vill visa dataflödesinformationen om. Detta inkluderar tjänster som Edge segmentering, datainsamling, Target, Adobe Journey Optimizer, Offer Decisioning, anpassade anpassade destinationer, händelsevidarebefordran, Adobe Analytics och Adobe Audience Manager.

Om du filtrerar efter kant kan du välja vilken kant du vill visa information om. De kanter som stöds är US East Coast, US West Coast, Europe, India, Singapore, Australia, Japan och Schweiz. Du kan markera flera kanter som ska visas samtidigt.

Om du filtrerar efter datum kan du välja tidsskala för att filtrera händelserna. Den här tidsskalan kan ställas in till 30 dagar. Du kan också använda någon av följande förkonfigurerade tidsskalor: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] och [!UICONTROL Last 30 days].

## Övervakningsmått för kanttäckning

Mättabellen ger information som är specifik för den valda tjänstens kanttäckning. I följande tabell finns mer information om varje kolumn.

| Mått | Beskrivning |
| ------ | ----------- |
| Mottagna begäranden | Antalet begäranden som tagits emot av de markerade kanterna inom tidsramen. |
| Högsta genomströmning | Den högsta graden av begäranden som tas emot av de markerade kanterna inom tidsramen. |

{style="table-layout:auto"}

## Övervaka diagram för kantsegmenteringsgenomströmning

Övervakningsdiagrammet visar de poster per sekund som tagits emot av de markerade kanterna inom den angivna tidsramen, jämfört med den tillåtna maxkapaciteten.

![Diagrammet för kantsegmenteringsgenomflöde visas.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Datastream-vy

>[!NOTE]
>
>Datastream-vyn är **endast** tillgänglig om du filtrerar efter Edge segmenteringsgenomströmning.

I datastream-visningsavsnittet visas en lista med de senaste datastreamarna som passerat genom sandlådans kanter.

![Datastream-vyn visas och visar information om de listade datastreams.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Fält | Beskrivning |
| ----- | ----------- |
| Datastream-namn | Namnet på datastream. |
| Datauppsättningar | Namnet på de datauppsättningar som datastream tillhör. |
| Tjänsten är aktiverad | Namnen på de tjänster som datastream är aktiverad för. |
| Begäranden | Antalet begäranden som har skickats via datastream. |
| Högsta genomströmning | Högsta antal begäranden som har skickats via datastream. |
