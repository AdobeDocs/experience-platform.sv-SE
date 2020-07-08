---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en källkoppling för kundattribut i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---


# Skapa en källkoppling för kundattribut i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en källkoppling i användargränssnittet för att samla in kundattributprofildata i Adobe Experience Platform. Mer information om kundattribut finns i [översiktsdokumentet](https://docs.adobe.com/content/help/sv-SE/core-services/interface/customer-attributes/attributes.html).

## Skapa en källanslutning

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På *katalogskärmen* visas tillgängliga källor för att skapa inkommande anslutningar och varje källa visar antalet befintliga anslutningar som är kopplade till dem. Välj alternativet för **kundattribut** och klicka sedan på **Anslut källa**. Tillåt en stund innan anslutningen upprättas, så kommer du att omdirigeras om anslutningen lyckas.

>[!NOTE]
>
>Om du redan har etablerat en källkoppling för kundattributprofildata inaktiveras alternativet att ansluta till källan.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

På skärmen *Källaktivitet* visas alla tidigare upprättade anslutningar för kundattributprofildata. Du kan skapa en ny anslutning genom att klicka på **Välj data**.

>[!NOTE]
>
>Flera inkommande anslutningar till en källa kan göras för att hämta olika data.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

I listan över tillgängliga kundattributprofildatauppsättningar väljer du den du vill hämta till Platform och klickar på **Nästa**.

>[!NOTE]
>
>Endast en datauppsättning kan väljas per kundattributkällanslutning.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

Steget *Granska* visas så att du kan granska den nya inkommande anslutningen innan den skapas. Detaljerna om anslutningen är grupperade efter kategorier, inklusive:

* *Källinformation*: Visar typen av källanslutning och valda källdata.
* *Target-information*: När du skapar andra källanslutningar visar den här behållaren vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer. Kundattributprofildata mappas automatiskt och hämtas in i kundprofiler i realtid.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## Nästa steg

När anslutningen har skapats skapas ett målschema och en datauppsättning automatiskt som innehåller inkommande data. När det första intaget är klart kan kundattributprofildata användas av Platform-tjänster längre fram i kedjan, t.ex. kundprofil i realtid och segmenteringstjänst. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../../profile/home.md)
* [Översikt över segmenteringstjänsten](../../../../../segmentation/home.md)
