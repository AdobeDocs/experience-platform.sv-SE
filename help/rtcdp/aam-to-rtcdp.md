---
title: Utveckling från Audience Manager till Real-Time CDP
description: Förstå vad du bör tänka på innan du planerar en migrering från Audience Manager till Adobe Real-Time CDP.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Utveckling från Audience Manager till Real-Time CDP

I takt med att ni börjar använda Adobe Real-Time CDP bör ni ta hänsyn till dessa faktorer för att ta fram data och bli medvetna om viktiga skillnader mellan de båda teknikerna. Den här artikeln riktar sig till en praktiserande publik.

![Audience Manager till Real-Time CDP evolutionsdiagram](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Överväg dataarkitekturen i Audience Manager

När du ser på utvecklingen från Audience Manager till Real-Time CDP är det nu en avgörande tidpunkt att analysera dina [Audience Manager segment](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=sv-SE) och avgöra vilka [signalerna](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=sv-SE), [egenskaperna](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=sv-SE) och [reglerna](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=sv-SE#segment-builder-section) är som tillsammans utgör dessa segment.

Tänk dessutom på de datakällor som du för närvarande använder i Audience Manager.

Adobe rekommenderar att du kategoriserar dina segment enligt följande:

* Segment som kan skickas till Experience Platform via [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), eftersom de inte har några databeroenden, inga mål- eller aktiveringsproblem och deras segmenteringsregler kan skapas via Real-Time CDP [segmentbyggare](/help/segmentation/ui/segment-builder.md) senare.
* Segment som har regler som kan stödjas men som kan innehålla data som inte är tillgängliga i Real-Time CDP.
* Segment som inte kan skapas i Real-Time CDP och som saknar funktioner.

>[!TIP]
>
>Adobe Real-Time CDP erbjuder [tre typer av segmentutvärdering](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming] och [!UICONTROL Edge]. Kunder som använder realtidssegment i Audience Manager kan begränsas av den nuvarande begränsningen på 500 direktuppspelningssegment i Real-Time CDP. Läs mer om [segmenteringsskyddsutkast](/help/profile/guardrails.md).

## 2. Vilka segment är viktiga att skicka via [!UICONTROL Audience Manager Source Connector]?

Baserat på sina utvärderingskriterier ska segment som inte har några databeroenden, inga mål- eller aktiveringsproblem och deras segmenteringsregler skapas via Real-Time CDP datainsamling som [Adobe Experience Platform Web SDK](/help/web-sdk/faq.md) vid ett senare datum skickas via Audience Manager Source Connector.

## 3. Kommer du att använda målet [!UICONTROL Experience Cloud Audiences] för att hämta data tillbaka till Audience Manager?

Segment som har regler som kan stödjas i Real-Time CDP men som har aktiveringsberoenden till Audience Manager kan skickas till Audience Manager via målkortet [Experience Cloud Publiker](/help/destinations/catalog/adobe/experience-cloud-audiences.md).

## 4. Vilka destinationer har du i Audience Manager idag på plats och kan börja flytta till Real-Time CDP?

Adobe rekommenderar starkt att segment som aktiveras i Audience Manager till [personbaserade mål](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=sv) skickas till Real-Time CDP via [!UICONTROL Audience Manager Source Connector] för att sedan aktiveras via Real-Time CDP.

Alla personbaserade mål som är tillgängliga i Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - är också tillgängliga i Real-Time CDP.

Ytterligare partners för förstahandsdata och mediestrategi som [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) och [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) finns tillgängliga.

Real-Time CDP stöder för närvarande fler än 60 mål internt i [katalogen](/help/destinations/catalog/overview.md), varav över 20 är annonser eller sociala mål som stöder matchning av förstapartsmålgrupper.

## Nästa steg

När du har läst den här sidan har du nu en första uppsättning funderingar att gå igenom när du börjar utveckla från Audience Manager till Real-Time CDP.
