---
title: Adobe Experience Platform Web Software Development Kit (SDK) - översikt
description: Läs om hur du använder Adobe Experience Platform Web SDK för att integrera Experience Platform-funktioner på din webbplats.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Webb-SDK för Adobe Experience Platform {#overview}

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud-kunder kan interagera med sina tjänster via Adobe Experience Platform Edge Network.

Du kan implementera Web SDK på två sätt:

* [Webbtaggtillägget för SDK](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Se självstudiekursen om hur du [implementerar Adobe Experience Cloud med Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=sv-SE) för mer information.
* Manuell implementering med [Web SDK JavaScript-biblioteket](install/library.md).

Den här guiden innehåller anvisningar för hur du interagerar med Experience Cloud lösningar med både Web SDK JavaScript-biblioteket och taggtillägget.

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK ingår i Adobe Experience Platform Edge Network, som innehåller

* **[Experience Platform Web SDK](#overview)**: Ett JavaScript-bibliotek och taggtillägg som underlättar driftsättningen av Adobe-teknik.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: Ett tillägg till v5 Mobile SDK för den nya distributionsmetoden.
* **[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)**: Ett serversides-API för datainsamling, personalisering, reklam och marknadsföring. Du kan använda den på servrar, IoT-enheter, digitalboxar och andra enheter.

Edge Network erbjuder datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler. Det erbjuder en enda konsoliderad SDK för webben, mobiler och kanaler på serversidan, som skickar data till en gemensam Adobe-domän (`adobedc.net`) och tar emot en enda nyttolast för data- och upplevelseleverans.

På serversidan förenklar en enhetlig edge-gateway och ett gemensamt plattformstjänstramverk driftsättningen av nya funktioner samtidigt som den ger följande fördelar:

* Minska kundens tid till värde,
* behovet av punktintegreringar upphör,
* Förbättra prestanda jämfört med de gamla biblioteken.
* Minskade driftskostnader.
* Ökad innovationshastighet.
* Skapa konkurrensfördelar för Adobe-kunder.

Med ett konsoliderat edge-system kan ni hantera annonserings-, marknadsförings- och personaliseringskampanjer i alla kanaler. Det minskar den totala ägandekostnaden och stöder olika datatyper, vilket gör att du kan mappa din datamodell för användning med flera Experience Cloud-produkter.

## Videoöversikt {#video}

I videon nedan visas en översikt över Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotek som ersätts av Web SDK {#sdks}

Web SDK är ett nytt bibliotek med öppen källkod som byggts från grunden och som integrerar funktioner i befintliga bibliotek. Den åtgärdar problem med taggaktiveringsordning, inkonsekvenser i versionerna och beroendehantering, och erbjuder ett nytt [open source](https://github.com/adobe/alloy)-sätt att implementera [!DNL Experience Cloud].

SDK ersätter

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Det introducerar också en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. Tidigare krävdes flera anrop för `Visitor.js`, `AT.js`, `DIL.js` och `AppMeasurement.js`. Nu kan ett enskilt anrop hämta ett ID, hämta en [!DNL Target]-upplevelse, skicka data till [!DNL Audience Manager] och skicka data till Adobe Experience Platform.

Titta på videon nedan för att se hur Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network] fungerar, med ett enda anrop för att skicka data till [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] och [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrera från befintliga bibliotek till Web SDK {#migrating-to-web-sdk}

Adobe erbjuder en smidig uppgradering för att förenkla din migrering från något av de [befintliga biblioteken](#sdks) till Web SDK. Du kan migrera varje sida på webbplatsen separat utan att behöva migrera hela webbplatsen samtidigt. Du kan använda Web SDK på vissa sidor medan befintliga bibliotek finns kvar på andra, vilket ger en gradvis övergång.

### Migrering av `AT.js` till Web SDK-överväganden {#considerations}

Innan du migrerar sidor med `AT.js` till Web SDK måste du aktivera följande konfigurationsalternativ för Web SDK för att se till att besökarprofilen upprätthålls vid navigering mellan sidor.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Följande målfunktioner stöds inte vid migrering från `at.js` till Web SDK:
>
>* [Omdirigeringserbjudanden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=sv-SE)
>* [Stöd för CNAME och domänövergripande](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html?lang=sv-SE)

När du har migrerat från `AT.js` till Web SDK tar du bort alternativet `targetMigrationEnabled` från din konfiguration.
