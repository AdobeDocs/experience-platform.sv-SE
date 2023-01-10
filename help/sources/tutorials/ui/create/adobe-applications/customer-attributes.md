---
keywords: Experience Platform;hem;populära ämnen;kundattribut
solution: Experience Platform
title: Skapa en källanslutning för kundattribut i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning i användargränssnittet för att överföra kundattributprofildata till Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Skapa en källanslutning för kundattribut i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en källanslutning i användargränssnittet för att hämta kundattributprofildata till Adobe Experience Platform. Mer information om kundattribut finns i [Översikt över kundattribut](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Kundattributskällan stöder för närvarande inte aktivering eller inaktivering av dataflöden.

## Skapa en källanslutning

>[!NOTE]
>
>Om du redan har upprättat en källanslutning för kundattributprofildata inaktiveras alternativet att ansluta till källan.

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa en anslutning till.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Adobe applications] kategori, välj **[!UICONTROL Customer Attributes]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Välj datakälla för kundattribut

The [!UICONTROL Add data] På skärmen visas alla tillgängliga datakällor för kundattribut. Endast en datauppsättning kan väljas per källanslutning för kundattribut.

>[!NOTE]
>
>Fältgrupper, scheman och datauppsättningar skapas som en del av flödesetableringen. De förblir oförändrade och du måste ta bort dem manuellt om det behövs.

Schemautveckling stöds inte av kundattributskällan. Om schemaindata för en kundattributdatakälla ändras blir den inte kompatibel med Platform. Som en tillfällig lösning kan du ta bort ett befintligt kundattributdataflöde, tillsammans med tillhörande datauppsättning, schema och fältgrupp, och sedan skapa ett nytt med det uppdaterade schemat och datakällan.

>[!IMPORTANT]
>
>Du kan ta bort ett kundattribut, men dess motsvarande datauppsättning behålls även efter att dataflödet har tagits bort. Se guiden [ta bort en datauppsättning](../../../../../catalog/datasets/user-guide.md) för steg om hur du tar bort en datauppsättning manuellt.

Om du vill skapa en ny anslutning väljer du en datakälla i listan och väljer sedan **[!UICONTROL Next]**.

![tilläggsdata](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Ange information om dataflöde

The [!UICONTROL Dataflow detail] visas så att du kan ange ett namn och en kort beskrivning av dataflödet. Under den här processen kan du även konfigurera inställningar för [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion]och [!UICONTROL Alerts].

[!UICONTROL Error diagnostics] möjliggör detaljerad generering av felmeddelanden för alla felaktiga poster som inträffar i dataflödet, medan [!UICONTROL Partial ingestion] gör att du kan importera data som innehåller fel, upp till ett visst tröskelvärde som du manuellt anger. Se [partiell batchingång - översikt](../../../../../ingestion/batch-ingestion/partial.md) för mer information.

Du kan aktivera varningar för att få meddelanden om status för ditt dataflöde. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på källvarningar med hjälp av användargränssnittet](../../alerts.md).

När du är klar med informationen om dataflödet väljer du **[!UICONTROL Next]**.

![dataflöde-detail](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Granska dataflöde

The [!UICONTROL Review] visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

![recension](../../../../images/tutorials/create/customer-attributes/review.png)

## Nästa steg

När anslutningen har skapats skapas ett målschema och en datauppsättning automatiskt som innehåller inkommande data. När det inledande intaget är klart kan kundattributprofildata användas av plattformstjänster längre fram i kedjan, t.ex. [!DNL Real-Time Customer Profile] och [!DNL Segmentation Service]. Mer information finns i följande dokument:

* [[!DNL Real-Time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
