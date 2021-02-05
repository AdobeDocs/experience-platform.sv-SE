---
keywords: Experience Platform;hem;populära ämnen;kundattribut
solution: Experience Platform
title: Skapa en källanslutning för kundattribut i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning i användargränssnittet för att samla in kundattributprofildata till Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Skapa en källanslutning för kundattribut i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en källanslutning i användargränssnittet för att samla in kundattributprofildata till Adobe Experience Platform. Mer information om kundattribut finns i [översiktsdokumentet](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

## Skapa en källanslutning

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt källarbetsytan. Skärmen **[!UICONTROL Catalog]** visar tillgängliga källor för att skapa inkommande anslutningar med, och varje källa visar antalet befintliga anslutningar som är kopplade till dem. Välj alternativet för **[!UICONTROL Customer Attributes]** och välj sedan **[!UICONTROL Add data]**. Tillåt en stund innan anslutningen upprättas, så kommer du att omdirigeras om anslutningen lyckas.

>[!NOTE]
>
>Om du redan har etablerat en källkoppling för kundattributprofildata inaktiveras alternativet att ansluta till källan.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

På skärmen **Källaktivitet** visas alla tidigare upprättade anslutningar för kundattributprofildata. Du kan skapa en ny anslutning genom att klicka på **Välj data**.

>[!NOTE]
>
>Flera inkommande anslutningar till en källa kan göras för att hämta olika data.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

I listan över tillgängliga kundattributprofildatauppsättningar väljer du den du vill hämta till [!DNL Platform] och klickar på **Nästa**.

>[!NOTE]
>
>Endast en datauppsättning kan väljas per kundattributkällanslutning.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

**Granskningssteget** visas, så att du kan granska din nya inkommande anslutning innan den skapas. Detaljerna om anslutningen är grupperade efter kategorier, inklusive:

* **Källinformation**: Visar typen av källanslutning och valda källdata.
* **Målinformation**: När du skapar andra källanslutningar visar den här behållaren vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer. Kundattributprofildata mappas automatiskt och hämtas in i kundprofiler i realtid.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nästa steg

När anslutningen har skapats skapas ett målschema och en datauppsättning automatiskt som innehåller inkommande data. När det inledande intaget är klart kan kundattributprofildata användas av underordnade [!DNL Platform]-tjänster som [!DNL Real-time Customer Profile] och [!DNL Segmentation Service]. Mer information finns i följande dokument:

* [[!DNL Real-time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Segmentation Service] översikt](../../../../../segmentation/home.md)
