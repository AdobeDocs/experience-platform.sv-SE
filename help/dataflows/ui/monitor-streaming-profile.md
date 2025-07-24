---
title: Inmatning av direktuppspelningsprofil för bildskärm
description: Lär dig hur du använder kontrollpanelen för övervakning för att övervaka inmatning av direktuppspelningsprofiler
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# Inmatning av direktuppspelningsprofil för bildskärm

Du kan använda kontrollpanelen för övervakning i Adobe Experience Platform-användargränssnittet för att utföra realtidsövervakning av hur mycket strömmande profiler som används i organisationen. Använd den här funktionen för att få bättre genomskinlighet för genomströmning, fördröjning och mätvärden för datakvalitet som omger strömningsdata. Dessutom kan du använda den här funktionen för att proaktivt larma och hämta åtgärdbara insikter för att identifiera potentiella kapacitetsöverträdelser och problem med dataimporten.

Läs följande guide för att lära dig hur du kan använda kontrollpanelen för att övervaka frekvenser och mått för direktuppspelningsprofilsmatningsjobb i organisationen.

## Om kontrollpanelen för hämtning av direktuppspelningsprofil

Du kan använda tre olika mätkategorier på kontrollpanelen för inmatning av direktuppspelningsprofiler: [!UICONTROL Throughput], [!UICONTROL Ingestion] och [!UICONTROL Latency].

* **Genomflöde**: Välj **[!UICONTROL Throughput]** om du vill visa information om mängden data som Experience Platform hanterar under en konfigurerad tidsperiod. Se den här mätningen för att utvärdera systemets effektivitet och kapacitet.
   * **Kapacitet**: Den maximala mängden data som din sandlåda kan bearbeta under definierade villkor.
   * **Begärangenomströmning**: Den hastighet med vilken händelser tas emot av matningssystemet, mätt i händelser per sekund.
   * **Bearbetningsdataflöde**: Den hastighet med vilken systemet importerar och bearbetar inkommande händelsenyttolaster, mätt i händelser per sekund.
* **Inmatning**: Välj [!UICONTROL Ingestion] om du vill visa information om Inläggning-jobben i din sandlåda. Insumtionsjobben mäts i tre olika mätvärden:
   * **Poster skapade**: Det totala antalet poster som skapats under en given tidsperiod. Det här måttet representerar lyckade datainmatningsprocesser i din sandlåda.
   * **Misslyckade poster**: Det totala antalet poster som inte har importerats på grund av fel.
   * **Borttagna poster**: Det totala antalet poster som har utelämnats på grund av överträdelse av kapacitetsbegränsningar.
* **Latens**: Välj [!UICONTROL Latency] om du vill visa information om hur lång tid det tar för Experience Platform att svara på en begäran eller slutföra en åtgärd inom en viss tidsperiod.

## Övervakningsmått för inmatning av direktuppspelningsprofil {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Inmatning av direktuppspelningsprofil för bildskärm"
>abstract="Kontrollpanelen för direktuppspelningsprofiler visar information om genomströmning, ingångsfrekvens och fördröjning. Använd den här instrumentpanelen för att visa, förstå och analysera databearbetningsstatistik. av era strömningsprofiler till Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Begär genomströmning"
>abstract="Detta mått representerar antalet händelser som kommer in i matningssystemet per sekund."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Bearbetningsflöde"
>abstract="Det här måttet visar antalet händelser som har importerats av systemet varje sekund."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95-fördröjning vid förtäring"
>abstract="Detta mått mäter den 95:e percentilfördröjningen från det ögonblick en händelse anländer till Experience Platform när den kan hämtas till profilbutiken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Maximal genomströmning"
>abstract="Det här måttet representerar det maximala antalet inkommande begäranden per sekund som matas in i direktuppspelningsprofilen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Insamlade poster"
>abstract="Det här måttet representerar det totala antalet poster som har importerats till profilarkivet under ett konfigurerat tidsfönster."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Misslyckade poster"
>abstract="Det här måttet visar det totala antalet poster som misslyckades med inmatningen i profilarkivet inom ett konfigurerat tidsfönster på grund av fel."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Överhoppade poster"
>abstract="Det här måttet representerar det totala antalet poster som släppts inom ett konfigurerat tidsfönster på grund av konfigurations- eller kapacitetsfel."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Felinformation"
>abstract="Det här måttet representerar antalet misslyckade händelser på grund av fel."
>text="Learn more in documentation"

| Mått | Beskrivning | Dimensioner | Mätfrekvens |
| --- | --- | --- | --- |
| Begär genomströmning | Detta mått representerar antalet händelser som kommer in i matningssystemet per sekund. | Sandbox/Dataflow | Övervakning i realtid med datauppdatering var 60:e sekund. |
| Bearbetningsflöde | Det här måttet visar antalet händelser som har importerats av systemet varje sekund. | Sandbox/Dataflow | Övervakning i realtid med datauppdatering var 60:e sekund. |
| P95-fördröjning vid förtäring | Detta mått mäter den 95:e percentilfördröjningen från det ögonblick en händelse anländer till Experience Platform när den kan hämtas till profilbutiken. | Sandbox/Dataflow | Övervakning i realtid med datauppdatering var 60:e sekund. |
| Maximal genomströmning |
| Insamlade poster | Det här måttet representerar det totala antalet poster som har importerats till profilarkivet under ett konfigurerat tidsfönster. | <ul><li>Sandbox/Dataflow</li><li>Dataflödeskörning</li></ul> | <ul><li>Sandbox/Dataflow: Realtidsövervakning med datauppdatering var 60:e sekund.</li><li>Dataflödeskörning: Grupperad på 15 minuter.</li></ul> |
| Misslyckade poster | Det här måttet visar det totala antalet poster som misslyckades med inmatningen i profilarkivet inom ett konfigurerat tidsfönster på grund av fel. | <ul><li>Sandbox/Dataflow</li><li>Dataflödeskörning</li></ul> | <ul><li>Sandbox/Dataflow: Realtidsövervakning med datauppdatering var 60:e sekund.</li><li>Dataflödeskörning: Grupperad på 15 minuter.</li></ul> |
| Överhoppade poster | Det här måttet representerar det totala antalet poster som släppts inom ett konfigurerat tidsfönster på grund av konfigurations- eller kapacitetsfel. | <ul><li>Sandbox/Dataflow</li><li>Dataflödeskörning</li></ul> | <ul><li>Sandbox/Dataflow: Realtidsövervakning med datauppdatering var 60:e sekund.</li><li>Dataflödeskörning: Grupperad på 15 minuter.</li></ul> |
| Felinformation | Det här måttet representerar antalet misslyckade händelser på grund av fel. | Dataflödeskörning | Grupperad i ett timfönster. |

{style="table-layout:auto"}