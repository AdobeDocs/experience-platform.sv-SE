---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: Definiera uppräkningsfält i användargränssnittet
description: Lär dig hur du definierar ett uppräkningsfält i användargränssnittet för Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f6fefda974d2ae6fd4b035ef3b5fe633311c9772
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Definiera uppräkningsfält i användargränssnittet {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enumsuggestedvalue"
>title="Uppräkning och föreslagna värden"
>abstract="En uppräkning begränsar ett strängfält så att endast data som matchar en fördefinierad uppsättning värden kan importeras. Du kan också definiera en uppsättning föreslagna värden för fältet som inte begränsar åtkomsten, utan i stället definiera de attribut du kan välja mellan i segmenteringen. Mer information finns i dokumentationen."

I Experience Data Model (XDM) representerar ett uppräkningsfält ett fält som är begränsat till en fördefinierad lista med godkända värden.

När [definiera ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt kan du ange det som ett uppräkningsfält genom att välja **[!UICONTROL Enum]** i den högra listen.

![](../../images/ui/fields/special/enum.png)

Ytterligare kontroller visas när du har markerat kryssrutan, vilket gör att du kan ange värdebegränsningar för uppräkningen. Under **[!UICONTROL Value]** måste du ange det exakta värdet som du vill begränsa fältet till. Detta värde måste uppfylla [!UICONTROL Type] du valde för uppräkningsfältet. Du kan även ange en användarvänlig **[!UICONTROL Label]** även för begränsningen.

Om du vill lägga till ytterligare begränsningar för uppräkningen väljer du **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Fortsätt med att lägga till önskade begränsningar och valfria etiketter till uppräkningen. När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringarna i schemat.

![](../../images/ui/fields/special/enum-configured.png)

Arbetsytan uppdateras för att återspegla ändringarna. När du utforskar det här schemat i framtiden kan du visa och redigera begränsningarna för uppräkningsfältet i den högra listen.

![](../../images/ui/fields/special/enum-applied.png)

## Nästa steg

I den här guiden beskrivs hur du definierar ett uppräkningsfält i användargränssnittet. Se översikten på [definiera fält i användargränssnittet](./overview.md#special) för att lära dig hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].
