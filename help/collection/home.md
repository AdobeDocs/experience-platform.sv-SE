---
keywords: Experience Platform;hem;populära ämnen;datainsamling;starta;web sdk
solution: Experience Platform
title: Översikt över datainsamling
topic-legacy: overview
description: Läs mer om de olika tekniker som används för att samla in data om kundupplevelser i Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# Översikt över datainsamling

Adobe Experience Platform erbjuder en serie tekniker som gör att ni kan samla in kundupplevelsedata från källor på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra mål på några sekunder.

Datainsamling stöds för följande källor på klientsidan:

* Webbaserade program
* Inbyggda mobilappar
* OTT-program (Over-the-top)

De datainsamlingstekniker som tillhandahålls av Experience Platform fokuserar på identifierbarheten och tillgängligheten för kapslade datamängder. Dessa tekniker omfattar följande:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Taggar](../tags/home.md)
* [Vidarebefordran av händelser](../tags/ui/event-forwarding/overview.md)
* [Webb-SDK för Adobe Experience Platform](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

<!-- (Outdated terminology)
![](./images/Collection.png)
-->

## Enklare implementeringar, snabbare prestanda på klientsidan

Adobe Experience Platform SDK för webb och mobiler komprimerar och komprimerar alla produktbibliotek i Adobe till ett enda utvecklingsverktyg för webb- och mobilplattformar. Komprimering av dessa bibliotek snabbar upp datainsamlingen och konsoliderar operationer till en enda ström från klientenheter till Adobe Experience Platform Edge Network.

## Växlingsprocess för att driftsätta Adobe-teknik {#edge}

Platform Edge Network är ett globalt, snabbt och tillförlitligt nätverk av servrar som kan ta emot och bearbeta data i otrolig skala. Med taggar kan du konfigurera [datastreams](../edge/fundamentals/datastreams.md) för produkter som Adobe Target, Adobe Audience Manager och Adobe Analytics, som gör att du kan aktivera dessa produkter på serversidan utan att ändra klientkoden.

<!-- (Outdated terminology)
![](./images/deploy.png)
-->

>[!NOTE]
>
>En introduktion på hög nivå till Platform Edge Network finns i följande [interaktiv produktdemo](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Omvandla, berika och skicka data snabbt och säkert

[Vidarebefordran av händelser i Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) kan utnyttja alla plattformsdataströmmar. Du kan omvandla, berika och skicka data till andra mål än Adobe med extremt låg latens utan att lägga till någon kod från tredje part till klientenheten, vilket ger snabbare och säkrare datainsamling och distribution.

<!-- (Outdated terminology)
![](./images/launch.png)
-->