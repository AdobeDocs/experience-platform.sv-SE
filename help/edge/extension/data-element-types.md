---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 19430906e5e97732f88bfe13501c4a75f9338a07
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Dataelementtyper

När du ställt in [åtgärdstyper](action-types.md) i [Adobe Experience Platform Web SDK-taggtillägg](web-sdk-extension-configuration.md)måste du konfigurera dina dataelementtyper. Den här sidan beskriver de tillgängliga elementtyperna.

## ID för händelsesammanfogning {#event-merge-id}

Det här dataelementet tillhandahåller ett ID för händelsesammanfogning när det används. Ingen konfiguration behövs för det här dataelementet. Det angivna dataelementet ändras inte förrän besökaren lämnar sidan eller tills **[!UICONTROL Reset Event Merge ID]** åtgärdstypen används.

## Identitetskarta {#identity-map}

Med en identitetskarta kan du skapa identiteter för besökaren på din webbsida. En identitetskarta består av namnutrymmen, som _telefon_ eller _e-post_, med varje namnutrymme som innehåller en eller flera identifierare. Om personen på webbplatsen till exempel har angett två telefonnummer bör telefonens namnutrymme innehålla två identifierare.

I [!UICONTROL Identity map] dataelement kommer du att ange följande information för varje identifierare:

* **[!UICONTROL ID]**: Värdet som identifierar besökaren. Om identifieraren till exempel tillhör _telefon_ namnutrymme, [!UICONTROL ID] kan _555-555-5555_. Det här värdet härleds vanligtvis från en JavaScript-variabel eller någon annan datadel på sidan, så det är bäst att skapa ett dataelement som refererar till siddata och sedan referera till dataelementet i [!UICONTROL ID] fält i [!UICONTROL Identity map] dataelement. Om ID-värdet är allt utom en ifylld sträng när du kör på sidan, tas identifieraren automatiskt bort från identitetskartan.
* **[!UICONTROL Authenticated state]**: En markering som anger om besökaren är autentiserad.
* **[!UICONTROL Primary]**: En markering som anger om identifieraren ska användas som primär identifierare för den enskilda personen. Om ingen identifierare är markerad som primär kommer ECID att användas som primär identifierare.

![Användargränssnittsbild som visar skärmen Redigera dataelement.](./assets/identity-map-data-element.png)

Du bör inte ange en [!DNL ECID] när du skapar en identitetskarta. När du använder SDK [!DNL ECID] genereras automatiskt på servern och inkluderas i identitetskartan.

Identitetskartelementet används ofta tillsammans med [[!UICONTROL XDM object] dataelementtyp](#xdm-object) och [[!UICONTROL Set consent] åtgärdstyp](action-types.md#set-consent).

Läs mer om [Adobe Experience Platform Identity Service](../../identity-service/home.md).

## XDM-objekt {#xdm-object}

Det är enklare att formatera data till XDM med XDM-objektdataelementet. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![Användargränssnittsbild som visar XDM-objektstrukturen.](assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, som `web.webPageDetails.URL`, vissa objekt samlas in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.

## Variabel {#variable}

>[!IMPORTANT]
>
>Detta är för närvarande en betafunktion som kan komma att ändras. Framtida versioner kan innehålla helt nya versioner.

Ett annat sätt att skapa XDM-objekt är att använda **[!UICONTROL Variable]** dataelement. När XDM-objektets dataelement skapas när det refereras, till exempel inuti en `sendEvent` kommandot, **[!UICONTROL Variable]** dataelement kan uppdateras via [!UICONTROL Update variable] åtgärder. Om du vill använda dataelementet markerar du rätt Adobe Experience Platform-sandlåda och -schema.

![Användargränssnittsbild som visar skärmen Skapa dataelement.](assets/variable-data-element.png)

När du har skapat det här dataelementet kan du använda [Uppdatera variabel](./action-types.md#update-variable) åtgärder för att ändra dataelementet. Använd sedan variabeldataelementet för XDM-alternativet i skicka-händelseåtgärder.

## Nästa steg {#next-steps}

Läs mer om specifika användningsområden, som [komma åt ECID](accessing-the-ecid.md).
