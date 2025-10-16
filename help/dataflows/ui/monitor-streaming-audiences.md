---
title: Övervaka direktuppspelande målgrupper
description: Lär dig använda kontrollpanelen för övervakning för att övervaka målgrupper som utvärderas med direktuppspelningssegmentering
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Övervaka direktuppspelande målgrupper

intro blurb

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Dataflöden](../home.md): Dataflöden representerar datajobb som överför information mellan Experience Platform. De är konfigurerade för olika tjänster för att underlätta flyttning av data från källkopplingar till måldatauppsättningar, samt till identitetstjänst, kundprofil i realtid och destinationer.
* [Segmenteringstjänst](../../segmentation/home.md):
* [Kapacitet](../../landing/license-usage-and-guardrails/capacity.md): I Experience Platform kan du få reda på om din organisation har överskridit några av dina skyddsprofiler och du får information om hur du åtgärdar dessa problem.

## Övervakningsstatistik för direktuppspelande målgrupper {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Utvärderingsgrad"
>abstract="Det här måttet representerar antalet poster som utvärderas per sekund."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95-fördröjning vid förtäring"
>abstract="Detta mätresultat mäter 95:e percentilfördröjningen för en händelse som anländer till Adobe Experience Platform för att lyckas utvärdera den till publiken."
>text="Learn more in documentation"

Tabellen nedan innehåller mer detaljerad information om de mätvärden som används för att direktuppspela målgrupper.

| Mått | Beskrivning | Dimensioner |
| ------ | ----------- | ---------- |
| Utvärderingsgrad | Antalet bearbetade målgruppsutvärderingar per sekund. | Sandlåda, datauppsättning |
| P95-fördröjning vid förtäring | Den 95:e percentilationen av lyckade händelser i publiken. | Sandlåda, datauppsättning |
| Mottagna poster | Det totala antalet poster som tagits emot från direktuppspelningsinmatning för direktuppspelningssegmentering under det valda tidsfönstret. | Datauppsättning |
| Utvärderade poster | Det totala antalet poster som **lyckades** utvärderade med direktuppspelningssegmentering under det valda tidsfönstret. | Datauppsättning |
| Misslyckade poster | Det totala antalet poster som **inte kunde utvärderas** i direktuppspelningssegmentering på grund av fel under det valda tidsfönstret. | Datauppsättning, Flödeskörning |
| Överhoppade poster | Det totala antalet poster som **hoppade över**-utvärderingen i direktuppspelningssegmentering på grund av fel under det valda tidsfönstret. | Datauppsättning, Flödeskörning |
| Profiler kvalificerade | Antalet profiler som kvalificerats för målgruppen under det valda tidsfönstret. | Sandlåda, målgrupp |
| Profiler som diskvalificerats | Antalet profiler som diskvalificerades från målgruppen under det valda tidsfönstret. | Sandlåda, målgrupp |

{style="table-layout:auto"}

## Använda kontrollpanelen för direktuppspelande målgrupper {#monitoring-dashboard}

Om du vill få åtkomst till kontrollpanelen för direktuppspelande målgrupper går du till Experience Platform-gränssnittet, väljer **[!UICONTROL Monitoring]** i den vänstra navigeringen och väljer sedan **[!UICONTROL Streaming end-to-end]**.

BILD

Överst på kontrollpanelen finns måttkortet **[!UICONTROL Audiences]**. Visar information om **Utvärderingsfrekvensen** för målgrupperna.