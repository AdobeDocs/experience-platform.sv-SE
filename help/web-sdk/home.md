---
title: Adobe Experience Platform Web Software Development Kit (SDK) - översikt
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att integrera plattformsfunktioner på din webbplats.
source-git-commit: ac8bb272a8af26f90a866541d513e50bf2dfa8b0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---


# Webb-SDK för Adobe Experience Platform {#overview}

>[!IMPORTANT]
>
>I slutet av april 2024 kommer Adobe Experience Platform Web SDK att ta bort stöd för alla versioner av Internet Explorer.

Adobe Experience Platform Web Software Development Kit (SDK) är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med sina tjänster via Adobe Experience Platform Edge Network.

Adobe har två metoder för att implementera Web SDK:

* [Web SDK-taggtillägget](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Se självstudiekursen om hur du [implementerar Adobe Experience Cloud med Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) för mer information.
* Manuell implementering med JavaScript-biblioteket för Web SDK.

Användarhandboken innehåller anvisningar om hur du interagerar med Experience Cloud genom både Web SDK JavaScript-biblioteket och taggtillägget, där det är tillämpligt.

## Experience Platform Edge Network {#edge-network}

Experience Platform Web SDK ingår i en verktygsuppsättning som Adobe Experience Platform Edge Network består av.

Edge Network består av följande komponenter:

* **[Experience Platform Web SDK](#overview):** Ett JavaScript-bibliotek och ett taggtillägg som hjälper dig att förenkla distributionen av Adobe-tekniker.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/):** Ett tillägg till v5 Mobile SDK som gör att du kan använda den nya distributionsmetoden.
* **[Edge Network Server-API](../server-api/overview.md):** En serversides-API som du kan använda för olika typer av datainsamling, personalisering, reklam och marknadsföring. Server-API:t kan användas på servrar, IoT-enheter, digitalboxar och andra enheter.

Edge Network är ett ramverk för datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler. Den tillhandahåller en enda konsoliderad SDK för varje kanal (webb, mobil, på serversidan) som skickar data till en gemensam Adobe-domän (`adobedc.net`) och tar emot en enda nyttolast för data- och upplevelseleverans.

På serversidan gör en enhetlig edge-gateway och ett gemensamt ramverk för plattformstjänster det enkelt att driftsätta nya funktioner i den här realtidsmiljön. Arkitekturen:

* Minskar kundens tid till värde
* Ändrar behovet av punktintegreringar
* Förbättrar prestanda jämfört med gamla bibliotek
* Minskar kostnaderna
* Ökar innovationstakten
* Skapar hållbara konkurrensfördelar för Adobe-kunder

Med ett enda, konsoliderat edge-system kan ni hantera annonserings-, marknadsförings- och personaliseringskampanjer i alla kanaler som en integrerad upplevelse. Adobe kan också leverera tjänster med lägre total ägandekostnad för kunderna. Kantsystemet är utformat för att rymma de flesta typer av data, så att du kan mappa din egen datamodell så att den kan hämtas av flera Experience Cloud-produkter.

## Videoöversikt {#video}

I videon nedan visas en översikt över Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotek som ersätts av Web SDK {#sdks}

Web SDK är inte bara en wrapper runt befintliga bibliotek. Det är ett nytt bibliotek som skrivits från grunden för att införliva funktioner i befintliga bibliotek. Syftet är att klara utmaningar med taggar som måste aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera [!DNL Experience Cloud] och det är [öppen källkod](https://github.com/adobe/alloy).

Web SDK ersätter följande SDK:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. `Visitor.js` skickade tidigare ett blockerande anrop till besökar-ID-tjänsten, `AT.js` skickade sedan ett samtal till Adobe Target, `DIL.js` skickade ett samtal till Adobe Audience Manager och slutligen `AppMeasurement.js` skickade ett samtal till Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en [!DNL Target]-upplevelse, skicka data till [!DNL Audience Manager] och skicka data till Adobe Experience Platform i ett enda anrop.

I följande video visas Adobe Experience Platform [!DNL Web SDK] och Adobe Experience Platform [!DNL Edge Network] in action. I videoexemplet används ett enda anrop till Adobe som skickar data till [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] och [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrera från befintliga bibliotek till Web SDK {#migrating-to-web-sdk}

För att förenkla migreringen från något av de [befintliga biblioteken](#sdks) till Web SDK erbjuder Adobe en smidig uppgraderingsväg. Med den här sökvägen kan du migrera varje enskild sida på webbplatsen till Web SDK utan att behöva migrera hela webbplatsen samtidigt. Du kan använda Web SDK på en viss sida medan befintliga bibliotek finns på andra sidor. När du är klar kan du migrera även de andra sidorna.

### Migrering av `AT.js` till Web SDK-överväganden {#considerations}

Innan du migrerar sidor som använder `AT.js` till Web SDK måste du aktivera följande konfigurationsalternativ för Web SDK. Dessa alternativ säkerställer att besökarprofilen behålls när du navigerar från sidor med `AT.js` till sidor med Web SDK.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>Följande Target-funktioner stöds inte vid migrering från at.js till Web SDK:
>
>* [Omdirigeringserbjudanden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [Stöd för CNAME och domänövergripande](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

När du har migrerat från `AT.js` till Web SDK tar du bort alternativet `targetMigrationEnabled` från din konfiguration.
