---
title: edgeConfigId
description: Fastställ det datastream-ID som du vill skicka data till.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# `edgeConfigId`

The `edgeConfigId` egenskap är en sträng som avgör vilken [datastream](../../../datastreams/overview.md) i Adobe Experience Platform som du vill skicka data till. Den här egenskapen krävs när du skickar data till Adobe.

Så här hittar du ett datastream-ID:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Använd sökfältet för att hitta det önskade dataflödet och välj sedan **[!UICONTROL Copy]** ![Kopiera](../../assets/copy.png) bredvid datastream-ID:t.

Du kan också välja önskat datastream-namn så visas det dataStream-ID:t i den högra kolumnen som du vill kopiera.

## Välj ett datastream-ID med hjälp av taggtillägget Web SDK

Välj från en lista över tillgängliga datastreams eller ange ett datastream-ID direkt när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Leta reda på [!UICONTROL Datastreams] väljer du sedan den metod som du vill använda för att bestämma datastream.
   * Om du väljer från en lista markerar du sandlådan och datastream i respektive listruta.
   * Om du anger värden anger du det önskade dataStream-ID:t.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

Du kan skicka data till olika datastreams för produktions-, staging- och utvecklingstaggsmiljöer.

## Välj data-ID:t med JavaScript-biblioteket för Web SDK

Ange `edgeConfigId` string-egenskap när den körs `configure` -kommando. Den här egenskapen krävs för alla Web SDK-implementeringar. Om du utelämnar den här egenskapen vet Web SDK inte vilket datastream som data ska skickas till, vilket gör att dessa data går förlorade permanent.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Om du konfigurerar flera instanser av Web SDK på en sida måste du konfigurera en annan `edgeConfigId` för varje instans.
