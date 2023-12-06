---
title: Adobe Experience Platform Web Software Development Kit (SDK) - översikt
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att integrera plattformsfunktioner på din webbplats.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---


# Webb-SDK för Adobe Experience Platform {#overview}

Adobe Experience Platform Web Software Development Kit (SDK) är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med sina tjänster via Adobe Experience Platform Edge Network. Adobe har två metoder för att implementera Web SDK:

* Manuell implementering med `alloy.js` JavaScript-bibliotek. Den här användarhandboken innehåller dokumentation om den här implementeringsmetoden.
* The [SDK-taggtillägg för webben](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Se [Implementera Adobe Experience Cloud med Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) för mer information.

## Experience Platform Edge Network {#edge-network}

Experience Platform Web SDK ingår i en samling verktyg som utgör Adobe Experience Platform Edge Network. Edge Network består av följande komponenter:

* **[Experience Platform Web SDK](#overview):** JavaScript SDK och kodtillägg som dramatiskt förenklar driftsättningen av Adobe-tekniker.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/):** Ett tillägg till v5 Mobile SDK så att kunderna kan använda den nya distributionsmetoden
* **[Experience Platform Edge Network Server API](../server-api/overview.md):** Ett API som kan användas för olika typer av datainsamling, personalisering, annonsering och marknadsföring. Server-API:t kan användas på servrar, IoT-enheter, digitalboxar och andra enheter.

Edge Network är ett ramverk för datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler. Den ger en enda konsoliderad SDK för alla kanaler (JavaScript, Mobile, Server-side), som skickar data till en gemensam Adobe-domän (`adobedc.net`) och får en enda nyttolast för data- och upplevelseleverans.

På serversidan gör en enhetlig edge-gateway och ett gemensamt ramverk för plattformstjänster det enkelt att driftsätta nya funktioner i den här realtidsmiljön. Arkitekturen:

* Minskar kundens tid till värde
* Ändrar behovet av punktintegreringar
* Förbättrar prestanda jämfört med gamla bibliotek
* Minskar kostnaderna
* Ökar innovationstakten
* Skapar hållbara konkurrensfördelar för Adobe-kunder

Med ett enda konsoliderat edge-system kan kunderna hantera sina annonserings-, marknadsförings- och personaliseringskampanjer i alla kanaler som en integrerad upplevelse. Adobe kan också leverera tjänster med lägre total ägandekostnad för kunderna. Kantsystemet är utformat för att rymma de flesta typer av data, så att du kan mappa din egen datamodell så att den kan hämtas av flera Experience Cloud-produkter.

## Videoöversikt {#video}

I följande videofilm visas en översikt över Adobe Experience Platform [!DNL Web SDK] och Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotek som ersätts av Web SDK {#sdks}

Web SDK är inte bara en wrapper runt befintliga bibliotek. Det är ett nytt bibliotek som skrivits från grunden för att införliva funktioner i befintliga bibliotek. Syftet är att klara utmaningar med taggar som måste aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera [!DNL Experience Cloud] och det [öppen källkod](https://github.com/adobe/alloy).

Web SDK ersätter följande SDK:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. Före, `Visitor.js` skickade ett blockeringsanrop till besökar-ID-tjänsten och sedan `AT.js` har ringt Adobe Target, `DIL.js` skickade ett samtal till Adobe Audience Manager och slutligen `AppMeasurement.js` har ringt Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en [!DNL Target] upplevelse, skicka data till [!DNL Audience Manager]och skicka data till Adobe Experience Platform via ett enda samtal.

I följande video visas Adobe Experience Platform [!DNL Web SDK] och Adobe Experience Platform [!DNL Edge Network] in action. I videoexemplet används ett enda anrop till Adobe som skickar data till [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]och [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrera från befintliga bibliotek till Web SDK {#migrating-to-web-sdk}

För att förenkla migreringen från någon av [befintliga bibliotek](#sdks) till Web SDK erbjuder Adobe en smidig uppgradering. Med den här sökvägen kan du migrera varje enskild sida på webbplatsen till Web SDK utan att behöva migrera hela webbplatsen samtidigt. Du kan använda Web SDK på en viss sida medan befintliga bibliotek finns på andra sidor. När du är klar kan du migrera även de andra sidorna.

### Migrering av `AT.js` till Web SDK-överväganden {#considerations}

Före migrering av sidor som använder `AT.js` till Web SDK, se till att aktivera följande Web SDK-konfigurationsalternativ. Dessa alternativ säkerställer att besökarprofilen behålls när du navigerar från sidor med `AT.js` till sidor med Web SDK.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Följande Target-funktioner stöds inte vid migrering från at.js till Web SDK:
>
>* [Omdirigeringserbjudanden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [Stöd för CNAME och domänövergripande](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Efter migrering från `AT.js` till Web SDK, ta bort `targetMigrationEnabled` från din konfiguration.
