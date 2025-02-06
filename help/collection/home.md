---
keywords: Experience Platform;hem;populära ämnen;datainsamling;starta;web sdk
solution: Experience Platform
title: Översikt över datainsamling
description: Läs mer om de olika tekniker som används för att samla in data om kundupplevelser i Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: b8332686043311c4dd3afeff12300fbd2827498c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 3%

---

# Översikt över datainsamling

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata från källor på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller icke-Adobe på bara några sekunder.

Datainsamling stöds för följande källor på klientsidan:

* Webbaserade program
* Inbyggda mobilappar
* OTT-program (Over-the-top)

Datainsamlingen fokuserar på att upptäcka och göra inkapslade datauppsättningar tillgängliga, vilket innefattar följande:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Taggar](../tags/home.md)
* [Dataströmmar](../datastreams/overview.md)
* [Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md)
* [Webb-SDK för Adobe Experience Platform](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Server-API för Edge Network](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Den här guiden ger en introduktion på hög nivå till datainsamling och hur den fungerar för att skicka data till Adobe Experience Cloud-produkter och program utanför Adobe via Platform Edge Network.

## Taggar, Web SDK och Mobile SDK

Platform Web SDK och Platform Mobile SDK komprimerar och komprimerar alla Adobe produktbibliotek till ett enda utvecklingsverktyg för webb- och mobilplattformar. Dessa kan implementeras med råkod eller med [tags](../tags/home.md) via användargränssnittet för datainsamling eller Adobe Experience Platform-gränssnittet.

Komprimering av dessa bibliotek snabbar upp datainsamlingen och konsoliderar operationer till en enda ström från klientenheter till Platform Edge Network.

![Taggar, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network och datastreams {#edge}

Platform Edge Network är ett globalt, snabbt och tillförlitligt nätverk av servrar som kan ta emot och bearbeta data i otrolig skala. Med hjälp av taggar kan du konfigurera [datastreams](../datastreams/overview.md) för produkter som Adobe Target, Adobe Audience Manager och Adobe Analytics, så att du kan aktivera de här produkterna på serversidan utan att ändra klientkoden.

Dessutom är datastreams integrerade med flera plattformsfunktioner som säkerställer att känsliga data som du skickar hanteras på rätt sätt med hänsyn till organisationens policyer och rättsliga bestämmelser. Mer information finns i avsnittet [Hantera känsliga data](../datastreams/overview.md#sensitive) i datastreams-dokumentationen.

![Datastreams och Adobe solutions](./images/home/adobe-solutions.png)

## Vidarebefordran av händelser

[Vidarebefordring av händelser](../tags/ui/event-forwarding/overview.md) kan utnyttja valfri dataström i Experience Platform, vilket gör att du kan omforma, berika och skicka data till andra mål än Adobe med extrem låg latens och utan att lägga till någon tredjepartskod till klientenheten.

![Vidarebefordran av händelser](./images/home/event-forwarding.png)

>[!NOTE]
>
>Vidarebefordran är en betalfunktion som ingår i Adobe Real-time Customer Data Platform Connections, Prime eller Ultimate.

## Nästa steg

Detta dokument innehåller en översikt på hög nivå över hur datainsamling fungerar för att automatisera processen för att skicka insamlade kundupplevelsedata till Adobe-produkter och tredjepartsdestinationer.

![Ramverk för datainsamling](./images/home/collection.png)

Mer information om det allmänna arbetsflödet för att skicka händelsedata via Edge Network finns i översikten [från början till slut](./e2e.md).
