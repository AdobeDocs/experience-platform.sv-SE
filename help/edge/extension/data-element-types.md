---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i Adobe Experience Platform Web SDK-tillägget i Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Dataelementtyper

När du har angett [åtgärdstyper](action-types.md) i [Adobe Experience Platform Web SDK-tillägget](web-sdk-extension.md) för [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfigurerar du dina dataelementtyper.

Den här sidan beskriver de tillgängliga elementtyperna.

## Händelsemarkerings-ID

Det här dataelementet tillhandahåller ett ID för händelsesammanfogning när det används. Ingen konfiguration behövs för det här dataelementet. Det angivna dataelementet förblir oförändrat tills besökaren lämnar sidan eller tills åtgärdstypen Återställ händelsematerial-ID används.

## Identitetskarta

Med data från identitetskartan kan du skapa identiteter från andra dataelement eller andra värden som du anger. Alla identiteter som du skapar måste vara knutna till ett motsvarande namnutrymme. Det här dataelementet innehåller en listruta som visar alla standardnamnutrymmen och alla som du har skapat.

![](./assets/identity-map-data-element.png)

## XDM-objekt

Använd XDM-format för att skicka data till Adobe Experience Platform Web SDK. Det är enklare att formatera data med XDM-objektets dataelement. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![](./assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, som `web.webPageDetails.URL`, samlas vissa objekt in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.
