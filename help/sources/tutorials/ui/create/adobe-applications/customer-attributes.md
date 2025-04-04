---
keywords: Experience Platform;hem;populära ämnen;kundattribut
solution: Experience Platform
title: Skapa ett kundattribut för Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning i användargränssnittet för att överföra kundattributprofildata till Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
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

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa en anslutning till.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Adobe applications] väljer du **[!UICONTROL Customer Attributes]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Välj datakälla för kundattribut

Skärmen [!UICONTROL Add data] visar alla tillgängliga datakällor för kundattribut. Endast en datauppsättning kan väljas per källanslutning för kundattribut.

>[!NOTE]
>
>Fältgrupper, scheman och datauppsättningar skapas som en del av flödesetableringen. De förblir oförändrade och du måste ta bort dem manuellt om det behövs.

Schemautveckling stöds inte av kundattributskällan. Om schemaindata för en kundattributdatakälla ändras blir den inte kompatibel med Experience Platform. Som en tillfällig lösning kan du ta bort ett befintligt kundattributdataflöde, tillsammans med tillhörande datauppsättning, schema och fältgrupp, och sedan skapa ett nytt med det uppdaterade schemat och datakällan.

>[!IMPORTANT]
>
>Du kan ta bort ett kundattribut, men dess motsvarande datauppsättning behålls även efter att dataflödet har tagits bort. I guiden [Ta bort en datauppsättning](../../../../../catalog/datasets/user-guide.md) finns anvisningar om hur du tar bort en datauppsättning manuellt.

Om du vill skapa en ny anslutning väljer du en datakälla i listan och sedan **[!UICONTROL Next]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Ange information om dataflöde

Steget [!UICONTROL Dataflow detail] visas så att du kan ange ett namn och en kort beskrivning av dataflödet. Under den här processen kan du även konfigurera inställningar för [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion] och [!UICONTROL Alerts].

[!UICONTROL Error diagnostics] aktiverar detaljerad generering av felmeddelanden för alla felaktiga poster som inträffar i dataflödet, medan [!UICONTROL Partial ingestion] gör att du kan importera data som innehåller fel, upp till ett visst tröskelvärde som du manuellt anger. Mer information finns i [översikten över partiell gruppöverföring](../../../../../ingestion/batch-ingestion/partial.md).

Du kan aktivera varningar för att få meddelanden om status för ditt dataflöde. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på källvarningar med användargränssnittet](../../alerts.md).

Välj **[!UICONTROL Next]** när du är klar med informationen om dataflödet.

![dataflödesdetalj](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Granska dataflöde

Steg [!UICONTROL Review] visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer.

![granskning](../../../../images/tutorials/create/customer-attributes/review.png)

## Nästa steg

När anslutningen har skapats skapas ett målschema och en datauppsättning automatiskt som innehåller inkommande data. När det inledande intaget är slutfört kan kundattributprofildata användas av Experience Platform-tjänster längre fram i kedjan som [!DNL Real-Time Customer Profile] och [!DNL Segmentation Service]. Mer information finns i följande dokument:

* [[!DNL Real-Time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
