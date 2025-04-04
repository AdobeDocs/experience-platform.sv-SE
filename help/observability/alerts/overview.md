---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Varningar - översikt
description: Lär dig om varningar i Adobe Experience Platform, även hur strukturen för varningsregler definieras.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 2%

---

# Översikt över aviseringar

>[!NOTE]
>
>Eftersom varningar stöds i både produktions- och utvecklingssandlådor kan du prenumerera på dem i alla sandlådor. När en sandlåda återställs återställs även alla prenumerationsaviseringar, och när en sandlåda tas bort tas alla prenumerationsaviseringar bort.

Med Adobe Experience Platform kan du prenumerera på händelsebaserade aviseringar om Adobe Experience Platform-aktiviteter. Varningar minskar eller eliminerar behovet av att avfråga [[!DNL Observability Insights] API](../api/overview.md) för att kontrollera om ett jobb har slutförts, om en viss milstolpe i ett arbetsflöde har nåtts eller om fel har uppstått.

När vissa villkor i Experience Platform-åtgärderna är uppfyllda (t.ex. ett eventuellt problem när ett tröskelvärde överskrids) kan Experience Platform skicka varningsmeddelanden till användare i organisationen som prenumererat på dem. Dessa meddelanden kan upprepas under ett fördefinierat tidsintervall tills varningen har lösts.

Det här dokumentet innehåller en översikt över varningar i Adobe Experience Platform, inklusive strukturen för hur varningsregler definieras.

## Engångsvarningar jämfört med upprepade varningar

Experience Platform-varningar kan skickas en gång eller upprepas under ett fördefinierat intervall tills de är lösta. Användningsexemplen för dessa alternativ är avsedda att skilja sig på följande sätt:

| Engångsvarning | Upprepad varning |
| --- | --- |
| Betyder inte nödvändigtvis något problem. | Anger ett potentiellt oönskat tillstånd. |
| Upprepa inte. | Kan upprepas om det avvikande tillståndet kvarstår. |
| Exempel:<ul><li>Inmatningen av data har slutförts.</li><li>En frågekörning har slutförts.</li><li>Data har tagits bort.</li></ul> | Exempel:<ul><li>Inmatningstiden är längre än serviceavtalet (SLA).</li><li>Dagligt intag har inte skett under de senaste 24 timmarna.</li><li>Strömprocessorns felfrekvens är över det konfigurerade tröskelvärdet.</li><li>Det totala antalet profiler överskrider berättigandet.</li></ul> |

{style="table-layout:auto"}

## Anatomi för en avisering

En varning kan delas upp i följande komponenter:

| Komponent | Beskrivning |
| --- | --- |
| **Mått** | Observeringsvärdet [metrisk](../api/metrics.md#available-metrics) vars värde utlöser aviseringen, t.ex. antalet misslyckade batchingshändelser (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Villkor** | Ett villkor relaterat till mätvärdet som utlöser varningen om det blir true, till exempel ett räkningsmått som överskrider ett visst tal. Det här villkoret kan kopplas till ett fördefinierat tidsfönster. |
| **Fönster** | (Valfritt) Villkoret för en varning kan begränsas till ett fördefinierat tidsfönster. En varning kan till exempel utlösas beroende på antalet misslyckade batchar under de senaste fem minuterna. |
| **Åtgärd** | När en varning utlöses utförs en åtgärd. I synnerhet skickas meddelanden till tillämpliga mottagare via en leveranskanal, som en förkonfigurerad webkrok eller Experience Platform-gränssnittet. |
| **Frekvens** | (Valfritt) En varning kan konfigureras för att upprepa sin åtgärd vid ett angivet intervall om dess villkor är sant eller på annat sätt är olöst. |

{style="table-layout:auto"}

## Ta emot och hantera aviseringar

Varningar kan tas emot och hanteras via två kanaler:

* [Adobe I/O Events](#events)
* [Experience Platform UI](#ui)

### I/O-händelser {#events}

Varningar kan skickas till en konfigurerad webkrok för att underlätta effektiv automatisering av aktivitetsövervakning. Om du vill få aviseringar via webkrok måste du registrera din webkrok för Experience Platform-aviseringar i Adobe Developer Console. Mer information finns i guiden om att [prenumerera på Adobe I/O-händelsemeddelanden](./subscribe.md).

### Experience Platform UI {#ui}

Med Experience Platform-gränssnittet kan du visa mottagna aviseringar och hantera aviseringsregler. I följande video ges en introduktion till dessa funktioner.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Om du vill arbeta med aviseringar i Experience Platform UI måste du ha följande åtkomstkontrollbehörighet aktiverat via Adobe Admin Console:

| Behörighet | Beskrivning |
| --- | --- |
| Visa aviseringar | Gör att du kan visa mottagna varningsmeddelanden. |
| Visa aviseringshistorik* | Gör att du kan visa en historik över mottagna aviseringar via fliken [!UICONTROL Alerts]. |
| Hantera aviseringar* | Gör att du kan aktivera och inaktivera varningsregler via fliken [!UICONTROL Alerts]. |
| Lös aviseringar* | Gör att du kan lösa utlösta aviseringar via fliken [!UICONTROL Alerts]. |

{style="table-layout:auto"}

**För att få åtkomst till fliken [!UICONTROL Alerts] måste du även få behörigheten Visa aviseringar i kombination med en av de andra behörigheterna.*

>[!NOTE]
>
>Mer information om hur du hanterar behörigheter i Experience Platform finns i [åtkomstkontrollsdokumentationen](../../access-control/ui/overview.md).

Med behörigheten Visa aviseringar kan du visa mottagna aviseringar genom att välja klockikonen (![Bellikon](/help/images/icons/bell.png)) i det övre högra hörnet.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Välj en avisering om du vill navigera till en relaterad kontrollpanel för mer detaljerad information om varför aviseringen har utlösts.

Dessutom tillåter fliken [!UICONTROL Alerts] i användargränssnittet enskilda användare att prenumerera på specifika aviseringstyper och administratörer kan aktivera eller inaktivera aviseringsregler helt och hållet. Mer information om hur du hanterar aviseringar finns i [gränssnittshandboken](./ui.md).

## Nästa steg

Genom att läsa det här dokumentet har du lagts till Experience Platform-varningar och deras roll i Experience Platform ekosystem. Läs mer i den processdokumentation som är länkad till i den här översikten om hur du tar emot och hanterar aviseringar.
