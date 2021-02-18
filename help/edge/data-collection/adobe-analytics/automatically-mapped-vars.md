---
title: Mappade Adobe Analytics-variabler automatiskt i Adobe Experience Platform Web SDK
description: Lär dig vilka variabler som automatiskt mappas i Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig vilka variabler som automatiskt mappas i Adobe Analytics med Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# Variabler mappas automatiskt i [!DNL Analytics]

Nedan finns en lista med variabler som Adobe Experience Platform Edge Network automatiskt mappar till Adobe Analytics.

| Sökväg till XDM-fält | [!DNL Analytics Query String] / HTTP Header | Beskrivning |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | Mappning av AppMeasurement-kontextdata `c.a.appid`. |
| `application.launches.value` | `c.a.launches` | Mappning av AppMeasurement-kontextdata `c.a.launches`. |
| `commerce.checkouts.id` | `events` | `scCheckout` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.checkouts.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_CHECKOUT, med avgränsaren `,`. |
| `commerce.order.currencyCode` | `cc` | AppMeasurement-frågeparameterns CURRENCY-mappning. |
| `commerce.order.purchaseID` | `pi` | AppMeasurement-frågeparametern PURCHASEID-mappning. |
| `commerce.productListAdds.id` | `events` | `scAdd` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.productListAdds.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_ADD, med avgränsaren `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.productListOpens.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_OPEN, med avgränsaren `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.productListRemovals.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_REMOVE, med avgränsaren `,`. |
| `commerce.productListViews.id` | `events` | `scView` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.productListViews.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_VIEW, med avgränsaren `,`. |
| `commerce.productViews.id` | `events` | `prodView` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| `commerce.productViews.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PROD_VIEW, med avgränsaren `,`. |
| `commerce.purchases.value` | `events` | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PURCHASE, med avgränsaren `,`. |
| `device.colorDepth` | `c` | AppMeasurement-frågeparametern C_COLOR-mappning. |
| `device.screenHeight` | `s` | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| `device.screenWidth` | `s` | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Det här är en HTTP-huvudmappning, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-frågeparametern COOKIES-mappning med konverteringen BOOLEAN_TO_YN. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement-frågeparametern JAVA_ENABLED-mappning med konverteringen BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-frågeparametern J_JSCRIPT-mappning. |
| `environment.browserDetails.userAgent` | `User-Agent` | Det här är en HTTP-huvudmappning, HEADER_USER_AGENT. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-frågeparametern BROWSER_HEIGHT-mappning. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement-frågeparametern BROWSER_WIDTH-mappning. |
| `environment.connectionType` | `ct` | AppMeasurement-frågeparametern CT_CONNECT_TYPE-mappning. |
| `environment.ipV4` | `X-Forwarded-For` | Det här är en HTTP-huvudmappning, X-FORWARDED-FOR. |
| `identityMap.ECID.[0].id` | `mid` | Mappning av parameter-MID för AppMeasurement-fråga. |
| `marketing.trackingCode` | `v0` | AppMeasurement-frågeparametern CAMPAIGN-mappning. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mappning av AppMeasurement-kontextdata `c.a.media.federated`. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mappning av AppMeasurement-kontextdata `c.a.media.pauseTime`. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mappning av AppMeasurement-kontextdata `c.a.media.pauseCount`. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mappning av AppMeasurement-kontextdata `c.a.media.friendlyName`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mappning av AppMeasurement-kontextdata `c.a.media.episode`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mappning av AppMeasurement-kontextdata `c.a.media.season`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mappning av AppMeasurement-kontextdata `a.media.name`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mappning av AppMeasurement-kontextdata `c.a.media.show`. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-kontextdata `c.a.media.type`-mappning med konverteringen VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-kontextdata `c.a.media.type`-mappning med konvertering VIDEO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mappning av AppMeasurement-kontextdata `c.a.media.length`. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mappning av AppMeasurement-kontextdata `c.a.media.channel`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mappning av AppMeasurement-kontextdata `c.a.contentType`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mappning av AppMeasurement-kontextdata `c.a.media.network`. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mappning av AppMeasurement-kontextdata `c.a.media.segment`. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mappning av AppMeasurement-kontextdata `c.a.media.playerName`. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mappning av AppMeasurement-kontextdata `c.a.media.sdkVersion`. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mappning av AppMeasurement-kontextdata `c.a.media.feed`. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mappning av AppMeasurement-kontextdata `c.a.media.format`. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mappning av AppMeasurement-kontextdata `c.a.media.resume`. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Kontextdata för AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mappning av AppMeasurement-kontextdata `c.a.media.timePlayed`. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mappning av AppMeasurement-kontextdata `c.a.media.totalTimePlayed`. |
| `placeContext.geo.latitude` | `lat` | LATITUDE-mappning för parametern LATITUDE för AppMeasurement-fråga. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement-frågeparameter LONGITUDE-mappning. |
| `placeContext.geo.postalCode` | `zip` | ZIP-mappning för parametern för AppMeasurement-fråga. |
| `placeContext.geo.stateProvince` | `state` | Parametern STATE-mappning för AppMeasurement-fråga. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement-frågeparametern Products Merchandise Events/Evars-mappning. |
| `productlistitems.[N].name` | `products` | AppMeasurement-frågeparameter Produktnamnsmappning. |
| `productlistitems.[N].priceTotal` | `products` | AppMeasurement-frågeparametern Produkt, prismappning. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement-frågeparametern Produkt Kvantitetsmappning. |
| `web.webInteraction.URL` | `pev1` | AppMeasurement-frågeparametern PAGE_EVENT_VAR1-mappning. |
| `web.webInteraction.name` | `pev2` | AppMeasurement-frågeparametern PAGE_EVENT_VAR2-mappning. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` till  `pe=lnk_o`;  `web.webInteraction.type=download` till  `pe=lnk_d`;  `web.webInteraction.type=exit` till  `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | AppMeasurement-frågeparametern PAGE_URL-mappning. |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement-frågeparametern PAGE_TYPE_FULL-mappning med konverteringen ERROR_PAGE_TYPE. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement-frågeparametern HOMEPAGE-mappning med konverteringen BOOLEAN_TO_YN. |
| `web.webPageDetails.name` | `gn` | AppMeasurement-frågeparametern PAGENAME-mappning. |
| `web.webPageDetails.server` | `sv` | AppMeasurement-frågeparametern USER_SERVER-mappning. |
| `web.webPageDetails.siteSection` | `ch` | Mappning av parametern CHANNEL för parametern AppMeasurement-fråga. |
| `web.webReferrer.URL` | `r` | AppMeasurement-frågeparameterns REFERRER-mappning. |
