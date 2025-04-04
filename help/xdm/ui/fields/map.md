---
title: Definiera kartfält i användargränssnittet
description: Lär dig hur du definierar ett kartfält i Experience Platform användargränssnitt.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Definiera kartfält i användargränssnittet

Med Adobe Experience Platform kan ni helt anpassa strukturen för era anpassade Experience Data Model-klasser (XDM), schemafältgrupper och datatyper.

Du kan också definiera mappningsfält i Schemaredigeraren för att modellera flexibla och dynamiska datastrukturer eller lagra en samling nyckelvärdepar.

När du definierar ett nytt fält i Experience Platform användargränssnitt använder du listrutan **[!UICONTROL Type]** och väljer **[!UICONTROL Map]** i listan.

![Schemaredigeraren med listrutan Typ och kartvärdet markerat.](../../images/ui/fields/special/map.png)

En [!UICONTROL Map value type]-egenskap visas. Det här värdet krävs för datatyperna [!UICONTROL Map]. Tillgängliga värden för kartan är [!UICONTROL String] och [!UICONTROL Integer]. Välj ett värde i listrutan med tillgängliga alternativ.

![Schemaredigeraren med listrutan [!UICONTROL Map value type] markerad.](../../images/ui/fields/special/map-value-type.png)

När du har konfigurerat delfältet måste du tilldela det till en fältgrupp. Använd listrutan **[!UICONTROL Field Group]** eller sökfältet och välj **[!UICONTROL Apply]**. Du kan fortsätta att lägga till fält i objektet med samma process eller välja **[!UICONTROL Save]** för att bekräfta inställningarna.

![En inspelning av fältgruppsvalet och inställningar som används.](../../images/ui/fields/special/assign-to-field-group.gif)

## Användningsbegränsningar {#restrictions}

XDM har följande begränsningar för användning av den här datatypen:

* Karttyperna MÅSTE vara av typen `object`.
* Karttyper FÅR INTE ha egenskaper definierade (de definierar med andra ord tomma objekt).
* Karttyperna MÅSTE innehålla ett `additionalProperties.type`-fält som beskriver de värden som kan placeras i kartan, antingen `string` eller `integer`.
* Segmentering för flera enheter kan bara definieras baserat på kartnycklarna och inte på värdena.
* Kartor stöds inte för kontomålgrupper.

Se till att du bara använder karttypsfält när det är absolut nödvändigt, eftersom de har följande prestandanackdelar:

* Svarstiden från [Adobe Experience Platform Query Service](../../../query-service/home.md) försämras från tre sekunder till tio sekunder för 100 miljoner poster.
* Kartor måste ha färre än 16 tangenter, annars riskerar de att försämras ytterligare.

>[!NOTE]
>
>Experience Platform-gränssnittet har begränsningar för hur nycklarna för mappningsfält kan extraheras. Objekttypsfält kan expanderas, men kartor visas i stället som ett enda fält. Kartfält som skapats med API:t för schemaregister och som inte är sträng- eller heltalsdatatyper visas som [!UICONTROL Complex]-datatyper.

## Nästa steg

När du har läst det här dokumentet kan du nu definiera kartfält i Experience Platform användargränssnitt. Kom ihåg att du bara kan använda klasser och fältgrupper för att lägga till fält i scheman. Mer information om hur du hanterar de här resurserna i användargränssnittet finns i handböckerna om hur du skapar och redigerar [klasser](../resources/classes.md) och [fältgrupper](../resources/field-groups.md).

Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] finns i översikten för arbetsytan [[!UICONTROL Schemas] ](../overview.md).
