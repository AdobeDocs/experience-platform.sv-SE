---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 44fac57a30295b476910c0b37314eaebba175157
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Dataelementtyper

När du ställt in [åtgärdstyper](action-types.md) i [Adobe Experience Platform Web SDK-taggtillägg](web-sdk-extension-configuration.md)måste du konfigurera dina dataelementtyper. Den här sidan beskriver de tillgängliga elementtyperna.

## Identitetskarta {#identity-map}

Med en identitetskarta kan du skapa identiteter för besökaren på din webbsida. En identitetskarta består av namnutrymmen, som `CRMID`, `Phone` eller `Email`, med varje namnutrymme som innehåller en eller flera identifierare. Om personen på webbplatsen till exempel har angett två telefonnummer bör telefonens namnutrymme innehålla två identifierare.

I [!UICONTROL Identity map] dataelement kommer du att ange följande information för varje identifierare:

* **[!UICONTROL ID]**: Värdet som identifierar besökaren. Om identifieraren till exempel tillhör _telefon_ namnutrymme, [!UICONTROL ID] kan _555-555-555_. Det här värdet härleds vanligtvis från en JavaScript-variabel eller någon annan datadel på sidan, så det är bäst att skapa ett dataelement som refererar till siddata och sedan referera till dataelementet i [!UICONTROL ID] fält i [!UICONTROL Identity map] dataelement. Om ID-värdet är allt utom en ifylld sträng när du kör på sidan, tas identifieraren automatiskt bort från identitetskartan.
* **[!UICONTROL Authenticated state]**: En markering som anger om besökaren är autentiserad.
* **[!UICONTROL Primary]**: Ett urval som anger om identifieraren ska användas som primär identifierare för den enskilda personen. Om ingen identifierare är markerad som primär kommer ECID att användas som primär identifierare.

![Användargränssnittsbild som visar skärmen Redigera dataelement.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe rekommenderar att du skickar identiteter som representerar en person, till exempel `Luma CRM Id` som primär identitet.
>
>Om identitetskartan innehåller personidentifieraren (t.ex. `Luma CRM Id`) blir personidentifieraren den primära identifieraren. I annat fall `ECID` blir den primära identiteten.

Du bör inte ange en [!DNL ECID] när du skapar en identitetskarta. När du använder SDK [!DNL ECID] genereras automatiskt på servern och inkluderas i identitetskartan.

Identitetskartelementet används ofta tillsammans med [[!UICONTROL XDM object] dataelementtyp](#xdm-object) och [[!UICONTROL Set consent] åtgärdstyp](action-types.md#set-consent).

Läs mer om [Adobe Experience Platform Identity Service](../../../../identity-service/home.md).

## XDM-objekt {#xdm-object}

Det är enklare att formatera data till XDM med XDM-objektdataelementet. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![Användargränssnittsbild som visar XDM-objektstrukturen.](assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, som `web.webPageDetails.URL`, vissa objekt samlas in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.

## Variabel {#variable}

Ett annat sätt att skapa XDM-objekt är att använda **[!UICONTROL Variable]** dataelement. När XDM-objektets dataelement skapas när det refereras, till exempel inuti en `sendEvent` kommando, **[!UICONTROL Variable]** dataelement kan uppdateras via [!UICONTROL Update variable] åtgärder. Om du vill använda dataelementet markerar du rätt Adobe Experience Platform-sandlåda och -schema.

![Användargränssnittsbild som visar skärmen Skapa dataelement.](assets/variable-data-element.png)

När du har skapat detta dataelement kan du använda [Uppdatera variabel](./action-types.md#update-variable) åtgärder för att ändra dataelementet. Använd sedan variabeldataelementet för XDM-alternativet i skicka-händelseåtgärder.

## Nästa steg {#next-steps}

Läs mer om specifika användningsområden, som [komma åt ECID](accessing-the-ecid.md).
