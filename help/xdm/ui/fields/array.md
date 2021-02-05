---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;array;field;
solution: Experience Platform
title: Definiera matrisfält i användargränssnittet
description: Lär dig hur du definierar ett arrayfält i användargränssnittet för Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Definiera matrisfält i användargränssnittet

När du definierar ett XDM-fält (Experience Data Model) i Adobe Experience Platform-användargränssnittet kan du ange det fältet som en array.

Innehållet i arrayen beror på [!UICONTROL Type] som är markerat för det fältet. Om till exempel ett fälts [!UICONTROL Type] är inställt på [!UICONTROL String], kommer fältets inställning som en matris att beteckna fältet som en matris med strängar. Om fältets [!UICONTROL Type] är inställt på en datatyp med flera fält, till exempel &quot;[!UICONTROL Postal address]&quot;, blir det en array med postadressobjekt som överensstämmer med datatypen.

När du har [definierat ett nytt fält i användargränssnittet](./overview.md#define) kan du ange det som ett matrisfält genom att markera kryssrutan **[!UICONTROL Array]** i den högra listen.

![](../../images/ui/fields/special/array.png)

När kryssrutan är markerad visas ytterligare kontroller i den högra listen som du kan använda för att begränsa arrayen ytterligare. Om du inte vill använda en viss begränsning lämnar du fältet tomt.

Ytterligare konfigurationskontroller för arrayer är följande:

| Fältegenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Minimum length] | Det minsta antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Maximum length] | Det maximala antalet objekt som matrisen måste innehålla för att importen ska lyckas. |
| [!UICONTROL Unique items only] | Om den anges till [!UICONTROL True] måste varje objekt i arrayen vara unikt för att importen ska lyckas. |

När du har konfigurerat fältet väljer du **[!UICONTROL Apply]** för att tillämpa ändringen i schemat.

![](../../images/ui/fields/special/array-config.png)

Arbetsytan uppdateras för att återspegla ändringar som gjorts i fältet. Observera att datatypen som visas bredvid fältnamnet på arbetsytan har en kombination av hakparenteser (`[]`), vilket anger att fältet representerar en array med den datatypen.

![](../../images/ui/fields/special/array-applied.png)

## Nästa steg

I den här guiden beskrivs hur du definierar ett arrayfält i användargränssnittet. I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].