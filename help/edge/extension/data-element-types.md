---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 2f9ff95529c907cfc28bc98198eca9fcfc21e9b9
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Dataelementtyper

När du har angett [åtgärdstyper](action-types.md) i [taggtillägget Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) konfigurerar du dina dataelementtyper.

Den här sidan beskriver de tillgängliga elementtyperna.


## Händelsemarkerings-ID

Det här dataelementet tillhandahåller ett ID för händelsesammanfogning när det används. Ingen konfiguration behövs för det här dataelementet. Det angivna dataelementet förblir oförändrat tills besökaren lämnar sidan eller tills åtgärdstypen Återställ händelsematerial-ID används.

## Identitetskarta

Med data från identitetskartan kan du skapa identiteter från andra dataelement eller andra värden som du anger. Alla identiteter som du skapar måste vara knutna till ett motsvarande namnutrymme. Det här dataelementet innehåller en listruta som visar alla standardnamnutrymmen och alla som du har skapat.

![](./assets/identity-map-data-element.png)

## XDM-objekt {#xdm-object}

Använd XDM-format för att skicka data till Adobe Experience Platform Web SDK. Det är enklare att formatera data med XDM-objektets dataelement. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![](./assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, till exempel `web.webPageDetails.URL`, samlas vissa objekt in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.
