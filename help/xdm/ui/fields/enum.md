---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: Definiera uppräkningsfält i användargränssnittet
description: Lär dig hur du definierar ett uppräkningsfält i användargränssnittet för Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Definiera uppräkningsfält i användargränssnittet

I Experience Data Model (XDM) representerar ett uppräkningsfält ett fält som är begränsat till en fördefinierad lista med godkända värden.

När [du definierar ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt kan du ange det som ett uppräkningsfält genom att markera kryssrutan **[!UICONTROL Enum]** i den högra listen.

![](../../images/ui/fields/special/enum.png)

Ytterligare kontroller visas när du har markerat kryssrutan, vilket gör att du kan ange värdebegränsningar för uppräkningen. Under kolumnen **[!UICONTROL Value]** måste du ange det exakta värde som du vill begränsa fältet till. Detta värde måste motsvara [!UICONTROL Type] som du har valt för uppräkningsfältet. Du kan även ange en användarvänlig **[!UICONTROL Label]** för begränsningen.

Om du vill lägga till ytterligare begränsningar för uppräkningen väljer du **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Fortsätt med att lägga till önskade begränsningar och valfria etiketter till uppräkningen. När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringarna på schemat.

![](../../images/ui/fields/special/enum-configured.png)

Arbetsytan uppdateras för att återspegla ändringarna. När du utforskar det här schemat i framtiden kan du visa och redigera begränsningarna för uppräkningsfältet i den högra listen.

![](../../images/ui/fields/special/enum-applied.png)

## Nästa steg

I den här guiden beskrivs hur du definierar ett uppräkningsfält i användargränssnittet. I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].