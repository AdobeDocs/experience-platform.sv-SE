---
keywords: Experience Platform;home;popular topics;monitoring;monitor;data flows
solution: Experience Platform
title: Övervaka datainmatning
topic: overview
description: I den här användarhandboken beskrivs hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Övervaka datainmatning

Med dataöverföring kan du importera data till Adobe Experience Platform. Du kan antingen använda gruppinmatning, vilket gör att du kan infoga data med olika filtyper (t.ex. CSV-filer), eller direktuppspelning, vilket gör att du kan importera data till [!DNL Platform] direktuppspelningsslutpunkter i realtid.

I den här användarhandboken beskrivs hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.

## Övervaka direktuppspelning av data från början till slut

I användargränssnittet [för](https://platform.adobe.com)Experience Platform klickar du **[!UICONTROL Monitoring]** på den vänstra navigeringsmenyn och sedan på **[!UICONTROL Streaming end-to-end]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Övervakningssidan visas *[!UICONTROL Streaming end-to-end]* . Den här arbetsytan innehåller ett diagram som visar hur många direktuppspelade händelser som tas emot av [!DNL Platform], ett diagram som visar hur många direktuppspelade händelser som bearbetades av [[!DNL Real-time Customer Profile]](../../profile/home.md)samt en detaljerad lista över inkommande data.

![](../images/quality/monitor-data-flows/list-streams.png)

Som standard visas i det övre diagrammet hur snabbt du har fått i sig något under de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att klicka på den markerade knappen.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

I det nedre diagrammet visas antalet lyckade direktuppspelningshändelser [!DNL Profile] under de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att klicka på den markerade knappen.

>[!NOTE]
>
>För att data ska kunna visas i det här diagrammet måste data vara **explicit** aktiverade för [!DNL Profile]. Läs användarhandboken för [!DNL Profile]datauppsättningar om du vill lära dig hur du aktiverar direktuppspelande [data för](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Under diagrammen finns en lista med alla poster för direktuppspelning som motsvarar det datumintervall som visas ovan. Varje listad batch visar sitt ID, datauppsättningens namn, när den senast uppdaterades, antalet poster i gruppen samt antalet fel (om det finns några). Du kan klicka på en av posterna om du vill ha mer detaljerad information om posten.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Visa direktuppspelningsposter

När du visar information om en post som har direktuppspelats, visas information som antal poster som har importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Information om en misslyckad direktuppspelningspost visar samma information som en lyckad post.

![](../images/quality/monitor-data-flows/failed-batch.png)

Misslyckade poster innehåller dessutom information om de fel som uppstod när gruppen bearbetades. I exemplet nedan uppstod ett systemfel när dataId validerades från katalogen.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Övervaka dataöverföring från slutpunkt till slutpunkt

I gränssnittet för [[!DNL Experience Platform]](https://platform.adobe.com)klickar du **[!UICONTROL Monitoring]** på den vänstra navigeringsmenyn.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Övervakningssidan **[!UICONTROL Batch end-to-end]** visas med en lista över tidigare importerade batchar. Du kan klicka på valfri grupp om du vill ha mer detaljerad information om den posten.

![](../images/quality/monitor-data-flows/list-batches.png)

### Visa grupper

När du visar information om en slutförd grupp visas information som antal poster som importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-batch.png)

Detaljer för en misslyckad batch visar samma information som en slutförd batch, där antalet poster som misslyckades har lagts till.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Dessutom innehåller misslyckade batchar detaljerad information om de fel som uppstod när batchen bearbetades. I exemplet nedan uppstod ett fel med den inkapslade batchen eftersom ett okänt fält av `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)