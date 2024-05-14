---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '574'
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

Du kan skapa nyttolastobjekt med **[!UICONTROL Variable]** dataelement. Båda [!UICONTROL XDM] och [!UICONTROL Data] objekt stöds.

* När du väljer [!UICONTROL XDM]markerar du [!UICONTROL Sandbox] och [!UICONTROL Schema].
* När du väljer [!UICONTROL Data]väljer du önskade lösningar. Tillgängliga lösningar inkluderar [!UICONTROL Adobe Analytics] och [!UICONTROL Adobe Target].

![Bild av tagggränssnittet som visar dataelementalternativen.](assets/variable-data-element.png)

När du har skapat detta dataelement kan du använda [Uppdatera variabel](./action-types.md#update-variable) åtgärd för att ändra den. När det är klart kan du inkludera det här dataelementet i [Skicka händelse](./action-types.md#send-event) åtgärd för att skicka data till en datastream.

## Nästa steg {#next-steps}

Läs mer om specifika användningsområden, som [komma åt ECID](accessing-the-ecid.md).
