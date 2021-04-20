---
keywords: Experience Platform;hem;populära ämnen;kundattribut
solution: Experience Platform
title: Skapa en källanslutning för kundattribut i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning i användargränssnittet för att samla in kundattributprofildata till Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Skapa en källanslutning för kundattribut i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en källanslutning i användargränssnittet för att samla in kundattributprofildata till Adobe Experience Platform. Mer information om kundattribut finns i översikten [Kundattribut](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Funktionerna för att inaktivera, aktivera och ta bort dataflöden stöds för närvarande inte för källan för kundattribut.

## Skapa en källanslutning

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa en anslutning med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Adobe applications] väljer du **[!UICONTROL Customer Attributes]** och sedan **[!UICONTROL Add data]**.

>[!NOTE]
>
>Om du redan har upprättat en källanslutning för kundattributprofildata inaktiveras alternativet att ansluta till källan.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

Skärmen [!UICONTROL Add data] visar alla tillgängliga datakällor för kundattribut. Om du vill skapa en ny anslutning markerar du en datakälla i listan och väljer **[!UICONTROL Next]**.

>[!NOTE]
>
>Endast en datauppsättning kan väljas per källanslutning för kundattribut.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

Steget [!UICONTROL Dataflow detail] visas så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Under den här processen kan du även aktivera [!UICONTROL Partial ingestion] och [!UICONTROL Error diagnostics]. [!UICONTROL Partial ingestion] ger möjlighet att importera data som innehåller fel, upp till ett visst tröskelvärde som du kan ange, och samtidigt  [!UICONTROL Error diagnostics] ge information om felaktiga data som grupperas separat. Mer information finns i [översikten över partiell gruppöverföring](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

[!UICONTROL Review]-steget visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nästa steg

När anslutningen har skapats skapas ett målschema och en datauppsättning automatiskt som innehåller inkommande data. När det inledande intaget är klart kan kundattributprofildata användas av plattformstjänster längre fram i kedjan, till exempel [!DNL Real-time Customer Profile] och [!DNL Segmentation Service]. Mer information finns i följande dokument:

* [[!DNL Real-time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
