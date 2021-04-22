---
keywords: Experience Platform;hemmabruk;populära ämnen;övervakning;övervaka;dataflöden;övervaka inmatning;dataöverföring;visa poster;visa batchar;
solution: Experience Platform
title: Övervaka datainmatning
topic-legacy: overview
description: I den här användarhandboken beskrivs hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 6bedd5ec0865e858a337155deb80309a54e30892
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Övervaka datainmatning

Med dataöverföring kan du importera data till Adobe Experience Platform. Du kan antingen använda gruppinmatning, vilket gör att du kan infoga data med olika filtyper (t.ex. CSV), eller direktuppspelningsuppläsning, vilket gör att du kan importera data till [!DNL Platform] med direktuppspelningsslutpunkter i realtid.

Den här användarhandboken innehåller anvisningar om hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.

## Övervaka direktuppspelning av data från början till slut

I [användargränssnittet för Experience Platform](https://platform.adobe.com) väljer du **[!UICONTROL Monitoring]** på den vänstra navigeringsmenyn följt av **[!UICONTROL Streaming end-to-end]**.

Övervakningssidan **[!UICONTROL Streaming end-to-end]** visas. Den här arbetsytan innehåller ett diagram som visar hastigheten för direktuppspelade händelser som tas emot av [!DNL Platform], ett diagram som visar hastigheten för direktuppspelade händelser som bearbetades av [[!DNL Real-time Customer Profile]](../../profile/home.md) samt en detaljerad lista över inkommande data.

![](../images/quality/monitor-data-flows/list-streams.png)

Som standard visas i det övre diagrammet hur snabbt du har fått i sig något under de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att markera den markerade knappen.

![](../images/quality/monitor-data-flows/events-received.png)

I det nedre diagrammet visas hur snabbt det gick att bearbeta direktuppspelade händelser med [!DNL Profile] under de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att markera den markerade knappen.

>[!NOTE]
>
>För att data ska kunna visas i det här diagrammet måste data vara **explicit** aktiverat för [!DNL Profile]. Läs [användarhandboken för datauppsättningar](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile) om du vill lära dig hur du aktiverar direktuppspelningsdata för [!DNL Profile].

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Under diagrammen finns en lista med alla poster för direktuppspelning som motsvarar det datumintervall som visas ovan. Varje listad batch visar sitt ID, datauppsättningens namn, när den senast uppdaterades, antalet poster i gruppen samt antalet fel (om det finns några). Du kan välja vilken som helst av posterna om du vill ha mer detaljerad information om posten.

![](../images/quality/monitor-data-flows/streams.png)

### Visa direktuppspelningsposter

När du visar information om en post som har direktuppspelats, visas information som antal poster som har importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Information om en misslyckad direktuppspelningspost visar samma information som en lyckad post.

![](../images/quality/monitor-data-flows/failed-batch.png)

Misslyckade poster innehåller dessutom information om de fel som uppstod när gruppen bearbetades. I exemplet nedan uppstod ett tolkningsfel vid konvertering eller validering av data.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Övervaka dataöverföring från slutpunkt till slutpunkt

I [[!DNL Experience Platform UI]](https://platform.adobe.com) väljer du **[!UICONTROL Monitoring]** på den vänstra navigeringsmenyn.

Övervakningssidan för **[!UICONTROL Batch end-to-end]** visas med en lista över tidigare importerade batchar. Du kan välja vilken grupp som helst för mer detaljerad information om posten.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visa grupper

När du visar information om en slutförd grupp visas information som antal poster som importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-batch.png)

Detaljer för en misslyckad batch visar samma information som en slutförd batch, där antalet poster som misslyckades har lagts till.

![](../images/quality/monitor-data-flows/failed-batch.png)

Dessutom innehåller misslyckade batchar detaljerad information om de fel som uppstod när batchen bearbetades. I exemplet nedan uppstod ett fel med den inkapslade batchen eftersom den har det högsta antalet identiteter för personen.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
