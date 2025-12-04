---
title: datastreamId
description: Fastställ det datastream-ID som du vill skicka data till.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---

# `datastreamId`

Egenskapen `datastreamId` är en sträng som avgör vilken [datastream](/help/datastreams/overview.md) i Adobe Experience Platform du vill skicka data till. Den här egenskapen krävs när du skickar data till Adobe. SDK 2.20.0 eller tidigare använder `edgeConfigId` i stället.

Så här hittar du ett datastream-ID:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Använd sökfältet för att hitta det önskade dataflödet och välj sedan **[!UICONTROL Copy]** ![Kopiera](../../assets/copy.png) bredvid dataström-ID:t.

Du kan också välja önskat datastream-namn och det datastream-ID som ska kopieras visas i den högra kolumnen.

## Exempel på kod

Ange strängegenskapen `datastreamID` när du kör kommandot `configure`. Den här egenskapen krävs för alla Web SDK-implementeringar. Om du utelämnar den här egenskapen vet inte Web SDK vilka data som ska skickas till, vilket gör att dessa data går förlorade permanent.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Om du konfigurerar flera instanser av Web SDK på en sida måste du konfigurera olika `datastreamId` för varje instans.

## Markera datastream-ID:t med hjälp av taggtillägget Web SDK

Läs [Konfigurationsinställningar för dataström](/help/tags/extensions/client/web-sdk/configure/datastreams.md) i dokumentationen för SDK-taggtillägget för webben om du vill veta hur du anger önskat dataström för varje miljö med hjälp av taggar. Du kan skicka data till olika datastreams för produktions-, staging- och utvecklingstaggsmiljöer.
