---
keywords: Experience Platform;hem;populära ämnen;datainsamling;starta;web sdk
solution: Experience Platform
title: Real-time Customer Data Platform Connections Overview
topic-legacy: overview
description: Läs mer om de olika tekniker som används för att samla in data om kundupplevelser i Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 3%

---

# Real-time Customer Data Platform Connections overview

Real-time Customer Data Platform (RTCDP) Connections innehåller en serie tekniker som gör att du kan samla in kundupplevelsedata från källor på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till mål på Adobe eller utanför Adobe på några sekunder.

RTCDP-anslutningar stöds för följande källor på klientsidan:

* Webbaserade program
* Inbyggda mobilappar
* OTT-program (Over-the-top)

RTCDP Connections fokuserar på identifierbarhet och tillgänglighet för kapslade datauppsättningar, vilket innefattar följande:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Taggar](../tags/home.md)
* [Datastreams](../edge/datastreams/overview.md)
* [Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md)
* [Webb-SDK för Adobe Experience Platform](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

Den här guiden ger en introduktion på hög nivå med RTCDP Connections och hur den fungerar för att skicka data till Adobe Experience Cloud-produkter och program utanför Adobe via Platform Edge Network.

## Taggar, Web SDK och Mobile SDK

Platform Web SDK och Platform Mobile SDK komprimerar och komprimerar alla Adobe-produktbibliotek till ett enda utvecklingspaket för webb- respektive mobilplattformar. Dessa kan implementeras med råkod eller med [taggar](../tags/home.md) via användargränssnittet för datainsamling.

Komprimering av dessa bibliotek snabbar upp datainsamlingen och konsoliderar åtgärder till en enda ström från klientenheter till Platform Edge Network.

![Taggar, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network och datastreams {#edge}

Platform Edge Network är ett globalt, snabbt och tillförlitligt nätverk av servrar som kan ta emot och bearbeta data i otrolig skala. Med taggar kan du konfigurera [datastreams](../edge/datastreams/overview.md) för produkter som Adobe Target, Adobe Audience Manager och Adobe Analytics, som gör att du kan aktivera dessa produkter på serversidan utan att ändra klientkoden.

![Datastreams and Adobe solutions](./images/home/adobe-solutions.png)

>[!NOTE]
>
>En introduktion på hög nivå till Platform Edge Network finns i följande [interaktiv produktdemo](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Vidarebefordran av händelser

[Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md) kan utnyttja valfri datastream för Experience Platform så att du kan omvandla, berika och skicka data till andra mål än Adobe med extrem låg latens och utan att lägga till någon kod från tredje part till klientenheten.

![Vidarebefordran av händelser](./images/home/event-forwarding.png)

>[!NOTE]
>
>Vidarebefordran av händelser är en betalfunktion som endast ingår i Real-time Customer Data Platform Connections-erbjudandet.

## Nästa steg

Det här dokumentet innehåller en översikt på hög nivå över hur RTCDP Connections kan automatisera processen för att skicka insamlade kundupplevelsedata till Adobe-produkter och tredjepartsdestinationer.

![Ramverk för datainsamling](./images/home/collection.png)

Mer information om det allmänna arbetsflödet för att skicka händelsedata via Edge-nätverket finns i [end-to-end overview](./e2e.md).
