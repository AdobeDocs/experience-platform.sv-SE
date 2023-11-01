---
title: Utveckling från Audience Manager till Real-Time CDP
description: Förstå vad du bör tänka på innan du planerar en migrering från Audience Manager till Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# Utveckling från Audience Manager till Real-Time CDP

I takt med att ni börjar använda Adobe Real-Time CDP bör ni ta hänsyn till dessa faktorer för att ta fram data och bli medvetna om viktiga skillnader mellan de båda teknikerna. Den här artikeln riktar sig till en praktiserande publik.

![Audience Manager till Real-Time CDP evolutionsdiagram](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Överväg dataarkitekturen i Audience Manager

När du ser på utvecklingen från Audience Manager till Real-Time CDP är det dags att analysera [Audience Manager segment](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html) och avgöra vad [signaler](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [traits](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html)och [regler](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section) är de som utgör de segmenten.

Tänk dessutom på de datakällor som du för närvarande använder i Audience Manager.

Adobe rekommenderar att du kategoriserar dina segment enligt följande:

* Segment som kan skickas till Experience Platform via [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), eftersom de inte har några databeroenden, inga mål- eller aktiveringsproblem och deras segmenteringsregler kan skapas via Real-Time CDP [segmentbyggare](/help/segmentation/ui/segment-builder.md) senare.
* Segment som har regler som kan stödjas men som kan innehålla data som inte är tillgängliga i Real-Time CDP.
* Segment som inte kan skapas i Real-Time CDP och som saknar funktioner.

>[!TIP]
>
>Adobe Real-Time CDP erbjuder [tre typer av segmentutvärdering](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming]och [!UICONTROL Edge]. Kunder som använder realtidssegment i Audience Manager kan begränsas av den nuvarande begränsningen på 500 direktuppspelningssegment i Real-Time CDP. Läs mer om [skyddsräcken för segmentering](/help/profile/guardrails.md).

## 2. Vilka segment som är viktiga att skicka via [!UICONTROL Audience Manager Source Connector]?

Baserat på sina utvärderingskriterier kan segment som inte har några databeroenden, inga mål- eller aktiveringsproblem och deras segmenteringsregler skapas genom Real-Time CDP datainsamling som [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) vid ett senare datum skickas via Audience Manager Source Connector.

## 3. Kommer du att använda [!UICONTROL Experience Cloud Audiences] för att återföra data till Audience Manager?

Segment som har regler som kan stödjas i Real-Time CDP men som har aktiveringsberoenden till Audience Manager kan skickas till Audience Manager via [Experience Cloud målgrupper](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinationskort.

## 4. Vilka destinationer har du i Audience Manager idag på plats och kan börja flytta till Real-Time CDP?

Adobe rekommenderar starkt att segment aktiveras i Audience Manager till [personbaserade mål](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=sv) få push till Real-Time CDP via [!UICONTROL Audience Manager Source Connector], för att sedan aktivera via Real-Time CDP.

Alla personbaserade destinationer är tillgängliga i Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - finns också i Real-Time CDP.

Ytterligare partners inom data- och mediestrategi som [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md)och [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) är tillgängliga.

Real-Time CDP har för närvarande stöd för fler än 60 destinationer internt i [katalog](/help/destinations/catalog/overview.md), varav över 20 är annonser eller sociala destinationer som stöder förstahandsmatchning av målgrupper.

## Nästa steg

När du har läst den här sidan har du nu en första uppsättning funderingar att gå igenom när du börjar utveckla från Audience Manager till Real-Time CDP.
