---
title: Variabler mappas automatiskt i Adobe Analytics
seo-title: Variabler mappas automatiskt i Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig vilka variabler som automatiskt mappas i Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig vilka variabler som automatiskt mappas i Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---


# Variabler mappas automatiskt i [!DNL Analytics]

Nedan finns en lista med variabler som Adobe Experience Platform [!DNL Edge Network] automatiskt mappar till [!DNL Analytics].

| Sökväg till XDM-fält | [!DNL Analytics Query String] / HTTP Header | Beskrivning |
| ---------- | ------------------------- | -------- |
| `commerce.order.purchaseID` | `pi` | AppMeasurement-frågeparametern PURCHASEID-mappning. |
| `commerce.order.currencyCode` | `cc` | AppMeasurement-frågeparameterns CURRENCY-mappning. |
| `commerce.purchases.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PURCHASE, med avgränsare `,`. |
| `commerce.productViews.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PROD_VIEW, med avgränsaren `,`. |
| `commerce.productListOpens.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_OPEN, med avgränsaren `,`. |
| `commerce.productListViews.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_VIEW, med avgränsare `,`. |
| `commerce.checkouts.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_CHECKOUT, med avgränsaren `,`. |
| `commerce.productListAdds.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_ADD, med avgränsaren `,`. |
| `commerce.productListRemovals.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_REMOVE, med avgränsaren `,`. |
| `commerce.productViews.id` | `events` | `prodView` Händelseserialisering. |
| `commerce.productListOpens.id` | `events` | `scOpen` Händelseserialisering. |
| `commerce.productListViews.id` | `events` | `scView` Händelseserialisering. |
| `commerce.productListAdds.id` | `events` | `scAdd` Händelseserialisering. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Händelseserialisering. |
| `commerce.checkouts.id` | `events` | `scCheckout` Händelseserialisering. |
| `device.screenHeight` | `s` | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| `device.screenWidth` | `s` | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| `productlistitems.[N].lineitemid` | `products` | AppMeasurement-frågeparameter Produktkategorimappning. |
| `productlistitems.[N].name` | `products` | AppMeasurement-frågeparameter Produktnamnsmappning. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement-frågeparametern Produkt Kvantitetsmappning. |
| `productlistitems.[N].pricetotal` | `products` | AppMeasurement-frågeparametern Produkt, prismappning. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Kontextdata för AppMeasurement. |
| `environment.browserDetails.userAgent` | `User-Agent` | Det här är en HTTP-huvudmappning, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Det här är en HTTP-huvudmappning, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-frågeparametern COOKIES-mappning med konverteringen BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-frågeparametern J_JSCRIPT-mappning. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement-frågeparametern JAVA_ENABLED-mappning med konverteringen BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-frågeparametern BROWSER_HEIGHT-mappning. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement-frågeparametern BROWSER_WIDTH-mappning. |
| `environment.connectionType` | `ct` | AppMeasurement-frågeparametern CT_CONNECT_TYPE-mappning. |
| `device.colorDepth` | `c` | AppMeasurement-frågeparametern C_COLOR-mappning. |
| `placeContext.geo.stateProvince` | `state` | Parametern STATE-mappning för AppMeasurement-fråga. |
| `placeContext.geo.postalCode` | `zip` | ZIP-mappning för parametern för AppMeasurement-fråga. |
| `placeContext.geo.latitude` | `lat` | LATITUDE-mappning för parametern LATITUDE för AppMeasurement-fråga. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement-frågeparameter LONGITUDE-mappning. |
| `web.webPageDetails.server` | `sv` | AppMeasurement-frågeparametern USER_SERVER-mappning. |
| `web.webPageDetails.name` | `gn` | AppMeasurement-frågeparametern PAGENAME-mappning. |
| `web.webPageDetails.URL` | `g` | AppMeasurement-frågeparametern PAGE_URL-mappning. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement-frågeparametern HOMEPAGE-mappning med konverteringen BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | AppMeasurement-frågeparameterns REFERRER-mappning. |
| `web.webInteraction.type` | `pe` | AppMeasurement-frågeparametern PAGE_EVENT-mappning med konverteringen CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | AppMeasurement-frågeparametern PAGE_EVENT_VAR1-mappning. |
| `web.webInteraction.name` | `pev2` | AppMeasurement-frågeparametern PAGE_EVENT_VAR2-mappning. |
| `web.webPageDetails.siteSection` | `ch` | Mappning av parametern CHANNEL för parametern AppMeasurement-fråga. |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement-frågeparametern PAGE_TYPE_FULL-mappning med konverteringen ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Kontextdatamappning `c.a.appid` för AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Kontextdatamappning `c.a.launches` för AppMeasurement. |
| `marketing.trackingCode` | `v0` | AppMeasurement-frågeparametern CAMPAIGN-mappning. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Kontextdatamappning `a.media.name` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Kontextdatamappning `c.a.media.length` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Kontextdatamappning `c.a.contentType` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Kontextdatamappning `c.a.media.playerName` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Kontextdatamappning `c.a.media.channel` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Kontextdatamappning `c.a.media.segment` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Kontextdatamappning `c.a.media.friendlyName` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Kontextdatamappning `c.a.media.sdkVersion` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Kontextdatamappning `c.a.media.show` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Kontextdatamappning `c.a.media.format` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Kontextdatamappning `c.a.media.season` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Kontextdatamappning `c.a.media.episode` för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Kontextdatamappning `c.a.media.network` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Datamappning för AppMeasurement-kontext `c.a.media.type` med konverteringen VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Kontextdatamappning `c.a.media.feed` för AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Kontextdatamappning `c.a.media.timePlayed` för AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Kontextdatamappning `c.a.media.totalTimePlayed` för AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Kontextdatamappning `c.a.media.federated` för AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Kontextdatamappning `c.a.media.pauseCount` för AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Kontextdatamappning `c.a.media.pauseTime` för AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Kontextdatamappning `c.a.media.resume` för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-kontextdatamappning `c.a.media.type` med konverteringen VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | Mappning av parameter-MID för AppMeasurement-fråga. |
