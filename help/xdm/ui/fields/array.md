---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;array;field;
solution: Experience Platform
title: Definiera matrisfält i användargränssnittet
description: Lär dig hur du definierar ett arrayfält i användargränssnittet för Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Definiera matrisfält i användargränssnittet

När du definierar ett XDM-fält (Experience Data Model) i Adobe Experience Platform-användargränssnittet kan du ange det fältet som en array.

Innehållet i arrayen beror på [!UICONTROL Type] markerat för det fältet. Om ett fält till exempel [!UICONTROL Type] är inställd på &quot;[!UICONTROL String]&quot;, om du anger det fältet som en array, kommer fältet att vara en array med strängar. Om fältet [!UICONTROL Type] är inställd på en datatyp med flera fält, till exempel &quot;[!UICONTROL Postal address]&quot;, blir det en array med postadressobjekt som överensstämmer med datatypen.

Efter att du har [definierade ett nytt fält i användargränssnittet](./overview.md#define)kan du ange det som ett arrayfält genom att välja **[!UICONTROL Array]** i den högra listen.

![](../../images/ui/fields/special/array.png)

När kryssrutan är markerad visas ytterligare kontroller i den högra listen som du kan använda för att begränsa arrayen ytterligare. Om du inte vill använda en viss begränsning lämnar du fältet tomt.

Ytterligare konfigurationskontroller för arrayer är följande:

| Fältegenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Minimum length] | Det minsta antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Maximum length] | Det maximala antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Unique items only] | Om inställt på &quot;[!UICONTROL True]&quot; måste varje objekt i arrayen vara unikt för att importen ska lyckas. |

{style="table-layout:auto"}

När du har konfigurerat fältet väljer du **[!UICONTROL Apply]** för att tillämpa ändringen på schemat.

![](../../images/ui/fields/special/array-config.png)

Arbetsytan uppdateras för att återspegla ändringar som gjorts i fältet. Observera att den datatyp som visas bredvid fältnamnet på arbetsytan har ett par hakparenteser (`[]`), vilket anger att fältet representerar en array med den datatypen.

![](../../images/ui/fields/special/array-applied.png)

## Nästa steg

I den här guiden beskrivs hur du definierar ett matrisfält i användargränssnittet. Se översikten på [definiera fält i användargränssnittet](./overview.md#special) för att lära dig hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].
