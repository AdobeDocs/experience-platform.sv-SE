---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Varningar - översikt
description: Lär dig om varningar i Adobe Experience Platform, även hur strukturen för varningsregler definieras.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: cb889a169aa42b761b0eeff5aa7fb771ad6ed4be
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 2%

---

# Översikt över aviseringar

>[!NOTE]
>
>Varningar stöds inte i icke-produktionssandlådor. För att kunna prenumerera på varningar måste du se till att du använder en produktionssandlåda. Alla prenumerationsaviseringar återställs när sandlådan återställs. Alla prenumerationsaviseringar raderas också när en sandlåda tas bort.

Med Adobe Experience Platform kan du prenumerera på händelsebaserade aviseringar om Adobe Experience Platform-aktiviteter. Varningar minskar eller eliminerar behovet av att avfråga [[!DNL Observability Insights] API](../api/overview.md) för att kontrollera om ett jobb har slutförts, om en viss milstolpe i ett arbetsflöde har nåtts eller om fel har uppstått.

När en viss uppsättning villkor för plattformsåtgärder har nåtts (t.ex. ett potentiellt problem när systemet överskrider ett tröskelvärde) kan Platform leverera varningsmeddelanden till alla användare i organisationen som har prenumererat på dem. Dessa meddelanden kan upprepas under ett fördefinierat tidsintervall tills varningen har lösts.

Det här dokumentet innehåller en översikt över varningar i Adobe Experience Platform, inklusive strukturen för hur varningsregler definieras.

## Engångsvarningar jämfört med upprepade varningar

Plattformsaviseringar kan skickas en gång eller upprepas under ett fördefinierat intervall tills de är lösta. Användningsexemplen för dessa alternativ är avsedda att skilja sig på följande sätt:

| Engångsvarning | Upprepad varning |
| --- | --- |
| Betyder inte nödvändigtvis något problem. | Anger ett potentiellt oönskat tillstånd. |
| Upprepa inte. | Kan upprepas om det avvikande tillståndet kvarstår. |
| Exempel:<ul><li>Inmatningen av data har slutförts.</li><li>En frågekörning har slutförts.</li><li>Data har tagits bort.</li></ul> | Exempel:<ul><li>Inmatningstiden överskrider serviceavtalet (SLA).</li><li>Dagligt intag har inte skett under de senaste 24 timmarna.</li><li>Strömprocessorns felfrekvens är över det konfigurerade tröskelvärdet.</li><li>Det totala antalet profiler överskrider berättigandet.</li></ul> |

{style="table-layout:auto"}

## Anatomi för en avisering

En varning kan delas upp i följande komponenter:

| Komponent | Beskrivning |
| --- | --- |
| **Mått** | Observeringsvärdet [metrisk](../api/metrics.md#available-metrics) vars värde utlöser aviseringen, t.ex. antalet misslyckade batchingshändelser (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Villkor** | Ett villkor relaterat till mätvärdet som utlöser varningen om det blir true, till exempel ett räkningsmått som överskrider ett visst tal. Det här villkoret kan kopplas till ett fördefinierat tidsfönster. |
| **Fönster** | (Valfritt) Villkoret för en varning kan begränsas till ett fördefinierat tidsfönster. En varning kan till exempel utlösas beroende på antalet misslyckade batchar under de senaste fem minuterna. |
| **Åtgärd** | När en varning utlöses utförs en åtgärd. I synnerhet skickas meddelanden till tillämpliga mottagare via en leveranskanal, till exempel en förkonfigurerad webkrok eller användargränssnittet i Experience Platform. |
| **Frekvens** | (Valfritt) En varning kan konfigureras för att upprepa sin åtgärd vid ett angivet intervall om dess villkor är sant eller på annat sätt är olöst. |

{style="table-layout:auto"}

## Ta emot och hantera aviseringar

Varningar kan tas emot och hanteras via två kanaler:

* [Adobe I/O Events](#events)
* [Plattformsgränssnitt](#ui)

### I/O-händelser {#events}

Varningar kan skickas till en konfigurerad webkrok för att underlätta effektiv automatisering av aktivitetsövervakning. Om du vill få meddelanden via webkrok måste du registrera din webkrok för plattformsaviseringar i Adobe Developer Console. Mer information finns i guiden om att [prenumerera på Adobe I/O-händelsemeddelanden](./subscribe.md).

### Plattformsgränssnitt {#ui}

Med plattformsgränssnittet kan du visa mottagna aviseringar och hantera varningsregler. I följande video ges en introduktion till dessa funktioner.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Om du vill arbeta med aviseringar i plattformsgränssnittet måste du ha följande åtkomstkontrollbehörighet aktiverat via Adobe Admin Console:

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
>Mer information om hur du hanterar behörigheter i plattformen finns i [åtkomstkontrollsdokumentationen](../../access-control/ui/overview.md).

Med behörigheten Visa aviseringar kan du visa mottagna aviseringar genom att välja klockikonen (![Bellikon](../images/alerts/overview/icon.png)) i det övre högra hörnet.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Välj en avisering om du vill navigera till en relaterad kontrollpanel för mer detaljerad information om varför aviseringen har utlösts.

Dessutom tillåter fliken [!UICONTROL Alerts] i användargränssnittet enskilda användare att prenumerera på specifika aviseringstyper och administratörer kan aktivera eller inaktivera aviseringsregler helt och hållet. Mer information om hur du hanterar aviseringar finns i [gränssnittshandboken](./ui.md).

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till plattformsaviseringar och deras roll i plattformens ekosystem. Läs mer i den processdokumentation som är länkad till i den här översikten om hur du tar emot och hanterar aviseringar.
