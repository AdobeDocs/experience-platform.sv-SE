---
title: Dataelementtyper i Adobe Experience Platform Web SDK-tillägget
description: Lär dig mer om de olika dataelementtyperna i taggtillägget Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: fbca8a47c500e89d82cf636e8cb639f2bb59c2e6
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Dataelementtyper

När du har angett dina [åtgärdstyper](action-types.md) i [Adobe Experience Platform Web SDK-taggtillägget](web-sdk-extension-configuration.md) måste du konfigurera dina dataelementtyper. Den här sidan beskriver de tillgängliga elementtyperna.

## Identitetskarta {#identity-map}

Med en identitetskarta kan du skapa identiteter för besökaren på din webbsida. En identitetskarta består av namnutrymmen, som `CRMID`, `Phone` eller `Email`, där varje namnutrymme innehåller en eller flera identifierare. Om personen på webbplatsen till exempel har angett två telefonnummer bör telefonens namnutrymme innehålla två identifierare.

I dataelementet [!UICONTROL Identity map] anger du följande information för varje identifierare:

* **[!UICONTROL ID]**: Värdet som identifierar besökaren. Om identifieraren till exempel tillhör namnutrymmet _phone_ kan [!UICONTROL ID] vara _555-555-5555_. Det här värdet härleds vanligtvis från en JavaScript-variabel eller någon annan datadel på sidan, så det är bäst att skapa ett dataelement som refererar till siddata och sedan referera till dataelementet i [!UICONTROL ID]-fältet i [!UICONTROL Identity map]-dataelementet. Om ID-värdet är allt utom en ifylld sträng när du kör på sidan, tas identifieraren automatiskt bort från identitetskartan.
* **[!UICONTROL Authenticated state]**: En markering som anger om besökaren är autentiserad.
* **[!UICONTROL Primary]**: En markering som anger om identifieraren ska användas som primär identifierare för individen. Om ingen identifierare är markerad som primär kommer ECID att användas som primär identifierare.

![Gränssnittsbild som visar skärmen Redigera dataelement.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe rekommenderar att du skickar identiteter som representerar en person, till exempel `Luma CRM Id`, som primär identitet.
>
>Om identitetskartan innehåller personidentifieraren (t.ex. `Luma CRM Id`) blir personidentifieraren den primära identifieraren. Annars blir `ECID` den primära identiteten.

Du bör inte ange [!DNL ECID] när du skapar en identitetskarta. När du använder SDK genereras [!DNL ECID] automatiskt på servern och inkluderas i identitetskartan.

Identitetsmappningsdataelementet används ofta tillsammans med dataelementtypen [[!UICONTROL XDM object] ](#xdm-object) och åtgärdstypen [[!UICONTROL Set consent] ](action-types.md#set-consent).

Läs mer om [Adobe Experience Platform identitetstjänst](../../../../identity-service/home.md).

## XDM-objekt {#xdm-object}

Det är enklare att formatera data till XDM med XDM-objektdataelementet. När du först öppnar det här dataelementet väljer du rätt Adobe Experience Platform-sandlåda och -schema. När du har valt ditt schema ser du strukturen för ditt schema, som du enkelt kan fylla i.

![Gränssnittsbild som visar XDM-objektstrukturen.](assets/XDM-object.png)

Observera att när du öppnar vissa fält i schemat, till exempel `web.webPageDetails.URL`, samlas vissa objekt in automatiskt. Även om flera objekt samlas in automatiskt kan du skriva över dem om det behövs. Alla värden kan fyllas i manuellt eller med andra dataelement.

>[!NOTE]
>
>Fyll bara i de uppgifter du är intresserad av att samla in. Allt som inte fylls i utelämnas när data skickas till lösningarna.

## Variabel {#variable}

Du kan skapa nyttolastobjekt med dataelementet **[!UICONTROL Variable]**. Både [!UICONTROL XDM]- och [!UICONTROL Data]-objekt stöds.

* När du väljer [!UICONTROL XDM] markerar du önskad [!UICONTROL Sandbox] och [!UICONTROL Schema].
* Välj önskade lösningar när du väljer [!UICONTROL Data]. Tillgängliga lösningar är [!UICONTROL Adobe Analytics] och [!UICONTROL Adobe Target].

![Bild av tagggränssnitt som visar dataelementalternativen.](assets/variable-data-element.png)

När du har skapat det här dataelementet kan du ändra det med åtgärden [Uppdatera variabel](./action-types.md#update-variable) . När det är klart kan du inkludera det här dataelementet i åtgärden [Skicka händelse](./action-types.md#send-event) för att skicka data till ett datastream.

## Media: Experience Quality {#quality-experience}

Ett **[!UICONTROL Quality of Experience]**-dataelement är användbart när du skickar direktuppspelade mediehändelser till Adobe Experience Platform. Du kan lägga till det här elementet när du skapar en mediesession och följande mediahändelser kommer att innehålla uppdaterade kvalitetsdata för upplevelsen.

![Användargränssnittsbild som visar skärmen Skapa kvalitetsdataelement för upplevelse.](assets/qoe-data-element.png)

## Nästa steg {#next-steps}

Lär dig mer om specifika användningsfall som [åtkomst till ECID](accessing-the-ecid.md).
