---
title: edgeConfigId
description: Fastställ det datastream-ID som du vill skicka data till.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# `edgeConfigId`

Egenskapen `edgeConfigId` är en sträng som avgör vilken [datastream](../../../datastreams/overview.md) i Adobe Experience Platform du vill skicka data till. Den här egenskapen krävs när du skickar data till Adobe.

Så här hittar du ett datastream-ID:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Använd sökfältet för att hitta det önskade dataflödet och välj sedan **[!UICONTROL Copy]** ![Kopiera](../../assets/copy.png) bredvid dataström-ID:t.

Du kan också välja önskat datastream-namn så visas det dataStream-ID:t i den högra kolumnen som du vill kopiera.

## Välj ett datastream-ID med hjälp av taggtillägget Web SDK

Välj från en lista med tillgängliga datastreams eller ange ett datastream-ID direkt när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Leta reda på avsnittet [!UICONTROL Datastreams] och välj sedan önskad metod för att bestämma datastream.
   * Om du väljer från en lista markerar du sandlådan och datastream i respektive listruta.
   * Om du anger värden anger du det önskade dataStream-ID:t.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

Du kan skicka data till olika datastreams för produktions-, staging- och utvecklingstaggsmiljöer.

## Markera data-ID:t med hjälp av Web SDK JavaScript-biblioteket

Ange strängegenskapen `edgeConfigId` när du kör kommandot `configure`. Den här egenskapen krävs för alla Web SDK-implementeringar. Om du utelämnar den här egenskapen vet Web SDK inte vilket datastream som data ska skickas till, vilket gör att dessa data går förlorade permanent.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Om du konfigurerar flera instanser av Web SDK på en sida måste du konfigurera olika `edgeConfigId` för varje instans.
