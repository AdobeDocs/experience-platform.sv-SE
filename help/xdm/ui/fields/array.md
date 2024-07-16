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

Innehållet i arrayen beror på den [!UICONTROL Type] som har valts för det fältet. Om till exempel ett fälts [!UICONTROL Type] är inställt på [!UICONTROL String] kommer ett värde på fältet som en matris att beteckna fältet som en matris med strängar. Om fältets [!UICONTROL Type] är inställt på en datatyp med flera fält, till exempel [!UICONTROL Postal address], blir det en matris med postadressobjekt som överensstämmer med datatypen.

När du har [definierat ett nytt fält i användargränssnittet](./overview.md#define) kan du ange det som ett matrisfält genom att markera kryssrutan **[!UICONTROL Array]** i den högra listen.

![](../../images/ui/fields/special/array.png)

När kryssrutan är markerad visas ytterligare kontroller i den högra listen som du kan använda för att begränsa arrayen ytterligare. Om du inte vill använda en viss begränsning lämnar du fältet tomt.

Ytterligare konfigurationskontroller för arrayer är följande:

| Fältegenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Minimum length] | Det minsta antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Maximum length] | Det maximala antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Unique items only] | Om värdet är [!UICONTROL True] måste varje objekt i arrayen vara unikt för att importen ska lyckas. |

{style="table-layout:auto"}

När du har konfigurerat fältet väljer du **[!UICONTROL Apply]** för att tillämpa ändringen på schemat.

![](../../images/ui/fields/special/array-config.png)

Arbetsytan uppdateras för att återspegla ändringar som gjorts i fältet. Observera att datatypen som visas bredvid fältnamnet på arbetsytan har ett par hakparenteser (`[]`), vilket anger att fältet representerar en matris av den datatypen.

![](../../images/ui/fields/special/array-applied.png)

## Nästa steg

I den här guiden beskrivs hur du definierar ett matrisfält i användargränssnittet. Mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor] finns i översikten [Definiera fält i användargränssnittet](./overview.md#special).
