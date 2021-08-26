---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# Dataelementtyper

När du har angett [åtgärdstyper](action-types.md) i [taggtillägget Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) konfigurerar du dina dataelementtyper.

Den här sidan beskriver de tillgängliga elementtyperna.


## Händelsemarkerings-ID

Det här dataelementet tillhandahåller ett ID för händelsesammanfogning när det används. Ingen konfiguration behövs för det här dataelementet. Det angivna dataelementet förblir oförändrat tills besökaren lämnar sidan eller tills åtgärdstypen Återställ händelsematerial-ID används.

## Identitetskarta

Med en identitetskarta kan du skapa identiteter för besökaren på din webbsida. En identitetskarta består av namnutrymmen, som _telefon_ eller _e-post_, där varje namnutrymme innehåller en eller flera identifierare. Om personen på webbplatsen till exempel har angett två telefonnummer bör telefonens namnutrymme innehålla två identifierare.

I [!UICONTROL Identity map]-dataelementet anger du följande information för varje identifierare:

* **[!UICONTROL ID]**: Värdet som identifierar besökaren. Om identifieraren till exempel tillhör namnutrymmet _phone_ kan [!UICONTROL ID] vara _555-555-5555_. Det här värdet härleds vanligtvis från en JavaScript-variabel eller någon annan datadel på sidan, så det är bäst att skapa ett dataelement som refererar till siddata och sedan referera till dataelementet i [!UICONTROL ID]-fältet i [!UICONTROL Identity map]-dataelementet. Om ID-värdet är allt utom en ifylld sträng när du kör på sidan, tas identifieraren automatiskt bort från identitetskartan.
* **[!UICONTROL Authenticated state]**: En markering som anger om besökaren är autentiserad.
* **[!UICONTROL Primary]**: En markering som anger om identifieraren ska användas som primär identifierare för den enskilda personen. Om ingen identifierare är markerad som primär kommer ECID att användas som primär identifierare.

Du bör inte ange ett ECID när du skapar en identitetskarta. När du använder SDK genereras ett ECID automatiskt på servern och inkluderas i identitetskartan.

Identitetsmappningens dataelement används ofta tillsammans med datamolementtypen [[!UICONTROL XDM object]](#xdm-object) och åtgärdstypen [[!UICONTROL Set consent]](action-types.md#set-consent).

Läs mer om [Adobe Experience Platform identitetstjänst](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv).

![](./assets/identity-map-data-element.png)

## XDM-objekt {#xdm-object}

Använd XDM-format för att skicka data till Adobe Experience Platform Web SDK. Det är enklare att formatera data med XDM-objektets dataelement. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![](./assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, till exempel `web.webPageDetails.URL`, samlas vissa objekt in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.
