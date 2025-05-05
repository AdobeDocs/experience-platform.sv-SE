---
keywords: Experience Platform;home;populära topics;data collection;launch;web sdk
solution: Experience Platform
title: Översikt över datainsamling
description: Läs mer om de olika tekniker som används för att samla in data om kundupplevelser i Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Översikt över datainsamling

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata från källor på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra mål på några sekunder.

Datainsamling stöds för följande källor på klientsidan:

* Webbaserade program
* Inbyggda mobilappar
* OTT-program (Over-the-top)

Datainsamlingen fokuserar på att upptäcka och göra inkapslade datauppsättningar tillgängliga, vilket innefattar följande:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=sv-SE)
* [Taggar](../tags/home.md)
* [Dataströmmar](../datastreams/overview.md)
* [Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md)
* [Webb-SDK för Adobe Experience Platform](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Den här guiden ger en introduktion på hög nivå till datainsamling och hur den fungerar för att skicka data till Adobe Experience Cloud-produkter och andra program än Adobe via Experience Platform Edge Network.

## Taggar, Web SDK och Mobile SDK

Experience Platform Web SDK och Experience Platform Mobile SDK komprimerar och komprimerar alla Adobe produktbibliotek till ett enda utvecklingsverktyg för webb- och mobilplattformar. Dessa kan implementeras med råkod eller med [tags](../tags/home.md) via användargränssnittet för datainsamling eller Adobe Experience Platform-gränssnittet.

Komprimering av dessa bibliotek snabbar upp datainsamlingen och konsoliderar operationer till en enda ström från klientenheter till Experience Platform Edge Network.

![Taggar, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Experience Platform Edge Network och datastreams {#edge}

Experience Platform Edge Network är ett globalt, snabbt och tillförlitligt nätverk av servrar som kan ta emot och bearbeta data i otrolig skala. Med hjälp av taggar kan du konfigurera [datastreams](../datastreams/overview.md) för produkter som Adobe Target, Adobe Audience Manager och Adobe Analytics, så att du kan aktivera de här produkterna på serversidan utan att ändra klientkoden.

Dessutom är datastreams integrerade med flera Experience Platform-funktioner som säkerställer att känsliga data som du skickar hanteras på rätt sätt med hänsyn till organisationens policyer och rättsliga bestämmelser. Mer information finns i avsnittet [Hantera känsliga data](../datastreams/overview.md#sensitive) i datastreams-dokumentationen.

![Datastreams och Adobe solutions](./images/home/adobe-solutions.png)

## Vidarebefordran av händelser

[Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md) kan utnyttja alla Experience Platform-datastream så att du kan omforma, berika och skicka data till alla icke-Adobe-mål med extrem låg latens och utan att lägga till någon tredjepartskod till klientenheten.

![Vidarebefordran av händelser](./images/home/event-forwarding.png)

>[!NOTE]
>
>Vidarebefordran är en betalfunktion som ingår i Adobe Real-Time Customer Data Platform Connections, Prime eller Ultimate.

## Nästa steg

Det här dokumentet innehåller en översikt på hög nivå över hur datainsamling fungerar för att automatisera processen med att skicka insamlade kundupplevelsedata till Adobe-produkter och tredjepartsdestinationer.

![Ramverk för datainsamling](./images/home/collection.png)

Mer information om det allmänna arbetsflödet för att skicka händelsedata via Edge Network finns i översikten [från början till slut](./e2e.md).
