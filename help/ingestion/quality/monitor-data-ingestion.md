---
keywords: Experience Platform;hemmabruk;populära ämnen;övervakning;övervaka;dataflöden;övervaka inmatning;dataöverföring;visa poster;visa batchar;
solution: Experience Platform
title: Övervaka datainmatning
description: I den här användarhandboken beskrivs hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 9399a242b855e151e5822035bc952efa89fe4bf0
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Övervaka datainmatning

Med dataöverföring kan du importera data till Adobe Experience Platform. Du kan antingen använda gruppinmatning, vilket gör att du kan infoga data med olika filtyper (t.ex. CSV-filer), eller direktuppspelning, vilket gör att du kan importera data till [!DNL Platform] med direktuppspelande slutpunkter i realtid.

Den här användarhandboken innehåller anvisningar om hur du övervakar data i Adobe Experience Platform användargränssnitt. Den här guiden kräver att du har en Adobe ID och tillgång till Adobe Experience Platform.

## Övervaka direktuppspelning av data från början till slut {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="Inmatningshastighet"
>abstract="Antalet händelser som har bearbetats per sekund."
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html" text="Övervaka dataflöden för källor i användargränssnittet"

>[!TIP]
>
>Använd uttrycket för att beräkna det totala antalet händelser för ett visst datum: `total events / day = ingestion rate * 60 * 60 * 24`.

I [Experience Platform UI](https://platform.adobe.com), markera **[!UICONTROL Monitoring]** till vänster navigeringsmeny, följt av **[!UICONTROL Streaming end-to-end]**.

The **[!UICONTROL Streaming end-to-end]** övervakningssidan visas. Den här arbetsytan innehåller ett diagram som visar hur många direktuppspelade händelser som tas emot av [!DNL Platform], ett diagram som visar hur många direktuppspelade händelser som bearbetades av [[!DNL Real-Time Customer Profile]](../../profile/home.md)samt en detaljerad lista över inkommande data.

![](../images/quality/monitor-data-flows/list-streams.png)

Som standard visas i det övre diagrammet hur snabbt du har fått i sig något under de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att markera den markerade knappen.

![](../images/quality/monitor-data-flows/events-received.png)

I det nedre diagrammet visas antalet lyckade direktuppspelade händelser per [!DNL Profile] de senaste sju dagarna. Du kan justera datumintervallet så att olika tidsperioder visas genom att markera den markerade knappen.

>[!NOTE]
>
>För att data ska kunna visas i det här diagrammet måste data **explicit** aktiverad för [!DNL Profile]. Så här aktiverar du direktuppspelningsdata för [!DNL Profile], läsa [användarhandbok för datauppsättningar](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Under diagrammen finns en lista med alla poster för direktuppspelning som motsvarar det datumintervall som visas ovan. Varje listad batch visar sitt ID, datauppsättningens namn, när den senast uppdaterades, antalet poster i gruppen samt antalet fel (om det finns några). Du kan välja vilken som helst av posterna om du vill ha mer detaljerad information om posten.

![](../images/quality/monitor-data-flows/streams.png)

### Visa direktuppspelningsposter

När du visar information om en post som har direktuppspelats, visas information som antal poster som har importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Information om en misslyckad direktuppspelningspost visar samma information som en lyckad post.

![](../images/quality/monitor-data-flows/failed-batch.png)

Misslyckade poster innehåller dessutom information om de fel som uppstod när gruppen bearbetades. I exemplet nedan uppstod ett tolkningsfel vid konvertering eller validering av data.

>[!NOTE]
>
>Om det finns fel i inkapslade rader kommer dessa rader att **not** tas bort om inte det resulterande meddelandet resulterar i ogiltig XDM.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Övervaka dataöverföring från slutpunkt till slutpunkt

I [[!DNL Experience Platform UI]](https://platform.adobe.com), markera **[!UICONTROL Monitoring]** på den vänstra navigeringsmenyn.

The **[!UICONTROL Batch end-to-end]** övervakningssidan visas med en lista över tidigare importerade batchar. Du kan välja vilken grupp som helst för mer detaljerad information om posten.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Visa grupper

När du visar information om en slutförd grupp visas information som antal poster som importerats, filstorlek samt start- och sluttider för importen.

![](../images/quality/monitor-data-flows/successful-batch.png)

Detaljer för en misslyckad batch visar samma information som en slutförd batch, där antalet poster som misslyckades har lagts till.

![](../images/quality/monitor-data-flows/failed-batch.png)

Dessutom innehåller misslyckade batchar detaljerad information om de fel som uppstod när batchen bearbetades. I exemplet nedan uppstod ett fel med den inkapslade batchen eftersom den har det högsta antalet identiteter för personen.

>[!NOTE]
>
>Om det finns fel i inkapslade rader kommer dessa rader att **not** tas bort om inte det resulterande meddelandet resulterar i ogiltig XDM.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
