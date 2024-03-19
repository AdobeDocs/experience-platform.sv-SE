---
title: Definiera kartfält i användargränssnittet
description: Lär dig hur du definierar ett kartfält i användargränssnittet för Experience Platform.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Definiera kartfält i användargränssnittet

Med Adobe Experience Platform kan ni helt anpassa strukturen för era anpassade Experience Data Model-klasser (XDM), schemafältgrupper och datatyper.

Du kan också definiera mappningsfält i Schemaredigeraren för att modellera flexibla och dynamiska datastrukturer eller lagra en samling nyckelvärdepar. Kartdatastrukturen gör det möjligt att snabbt och effektivt söka efter, infoga och ta bort information som är ordnad och tillgänglig baserat på unika identifierare.

När du definierar ett nytt fält i användargränssnittet för plattformen använder du **[!UICONTROL Type]** listruta och välj &quot;**[!UICONTROL Map]**&quot; i listan.

![Schemaredigeraren med listrutan Typ och kartvärdet markerat.](../../images/ui/fields/special/map.png)

A [!UICONTROL Map value type] visas. Detta värde krävs för [!UICONTROL Map] datatyper. Tillgängliga värden för kartan är [!UICONTROL String] och [!UICONTROL Integer]. Välj ett värde i listrutan med tillgängliga alternativ.

![Schemaredigeraren med [!UICONTROL Map value type] listrutan är markerad.](../../images/ui/fields/special/map-value-type.png)

När du har konfigurerat delfältet måste du tilldela det till en fältgrupp. Använd **[!UICONTROL Field Group]** nedrullningsbar meny eller sökfält och välj **[!UICONTROL Apply]**. Du kan fortsätta lägga till fält i objektet med samma process, eller välja **[!UICONTROL Save]** för att bekräfta inställningarna.

![En inspelning av fältgruppsvalet och inställningar som används.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>Plattformsgränssnittet har begränsningar för hur nycklarna för mappningsfält kan extraheras. Objekttypsfält kan expanderas, men kartor visas i stället som ett enda fält. Mappningsfält som skapats med API:t för schemaregister och som inte är sträng- eller heltalsdatatyper visas som[!UICONTROL Complex]&quot; datatyper.

## Nästa steg

När du har läst det här dokumentet kan du nu definiera kartfält i plattformsgränssnittet. Kom ihåg att du bara kan använda klasser och fältgrupper för att lägga till fält i scheman. Om du vill veta mer om hur du hanterar de här resurserna i användargränssnittet läser du i handböckerna om hur du skapar och redigerar [klasser](../resources/classes.md) och [fältgrupper](../resources/field-groups.md).

Mer information om funktionerna i [!UICONTROL Schemas] arbetsytan, se [[!UICONTROL Schemas] arbetsyta - översikt](../overview.md).
