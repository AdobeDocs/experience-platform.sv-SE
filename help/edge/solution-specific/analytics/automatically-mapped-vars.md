---
title: Variabler mappas automatiskt i Analytics
seo-title: Variabler mappas automatiskt i Analytics med Adobe Experience Platform Web SDK
description: Lär dig vilka variabler som automatiskt mappas i Analytics med Experience Platform Web SDK
seo-description: Lär dig vilka variabler som automatiskt mappas i Analytics med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Variabler mappas automatiskt i analyser

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Nedan finns en lista med variabler som Adobe Experience Platform Edge Network automatiskt mappar till Analytics.

| Sökväg till XDM-fält | Analytics Query String / HTTP Header | Beskrivning |
| ---------- | ------------------------- | -------- |
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
| `application.id` | `c.a.appid` | Kontextdatamappning `c.a.appid` för AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Kontextdatamappning `c.a.launches` för AppMeasurement. |
| `marketing.trackingCode` | `v0` | AppMeasurement-frågeparametern CAMPAIGN-mappning. |
| `commerce.purchaseID` | `pi` | AppMeasurement-frågeparametern PURCHASEID-mappning. |
| `commerce.currencyCode` | `cc` | AppMeasurement-frågeparameterns CURRENCY-mappning. |
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
| `identitymap.ecid.[0].id` | `mid` | Mappning av parameter-MID för AppMeasurement-fråga. |
