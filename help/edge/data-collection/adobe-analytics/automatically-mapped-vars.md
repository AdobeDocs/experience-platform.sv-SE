---
title: Mappade Adobe Analytics-variabler automatiskt i Adobe Experience Platform Web SDK
description: Lär dig vilka variabler som automatiskt mappas i Adobe Analytics med Experience Platform Web SDK
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 4%

---

# Variabler mappas automatiskt i [!DNL Analytics]

Nedan finns en lista med variabler som Adobe Experience Platform Edge Network automatiskt mappar till Adobe Analytics. Detaljerad information om frågeparametrar för Adobe Analytics datainsamling finns i [Implementeringshandbok för analyser](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html).

>[!NOTE]
>Informationen på den här sidan gäller även för Adobe Mobile SDK.

| Sökväg till XDM-fält | [!DNL Analytics Query String] / HTTP Header | Beskrivning |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Kontextdata för AppMeasurement `c.a.appid` mappning. |
| application.launches.value | c.a.launches | Kontextdata för AppMeasurement `c.a.launches` mappning. |
| commerce.checkouts.id | händelser | `scCheckout` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.checkouts.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_CHECKOUT, med avgränsaren `,`. |
| commerce.order.currencyCode | cc | AppMeasurement-frågeparameterns CURRENCY-mappning. |
| commerce.order.purchaseID | pi | AppMeasurement-frågeparametern PURCHASEID-mappning. |
| commerce.productListAdds.id | händelser | `scAdd` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.productListAdds.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_ADD, med avgränsaren `,`. |
| commerce.productListOpens.id | händelser | `scOpen` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.productListOpens.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_OPEN, med avgränsaren `,`. |
| commerce.productListRemovals.id | händelser | `scRemove` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.productListRemovals.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_REMOVE, med avgränsaren `,`. |
| commerce.productListViews.id | händelser | `scView` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.productListViews.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_SC_VIEW, med avgränsaren `,`. |
| commerce.productViews.id | händelser | `prodView` händelseserialisering. Om det här fältet exkluderas (dvs. för oserialiserade händelser) genereras och tilldelas entiteten ett eget ID-värde. |
| commerce.productViews.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PROD_VIEW, med avgränsaren `,`. |
| commerce.purchases.value | händelser | AppMeasurement-frågeparametern EVENT_LIST_FULL-mappning med konverteringen COMMERCE_PURCHASE, med avgränsaren `,`. |
| device.colorDepth | c | AppMeasurement-frågeparametern C_COLOR-mappning. |
| device.screenHeight | s | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| device.screenWidth | s | AppMeasurement-frågeparametern Screen Resolution-mappning. |
| environment.browserDetails.acceptLanguage | Acceptera språk | Det här är en HTTP-huvudmappning, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | AppMeasurement-frågeparametern COOKIES-mappning med konverteringen BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | AppMeasurement-frågeparametern JAVA_ENABLED-mappning med konverteringen BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement-frågeparametern J_JSCRIPT-mappning. |
| environment.browserDetails.userAgent | Användaragent | Det här är en HTTP-huvudmappning, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | AppMeasurement-frågeparametern BROWSER_HEIGHT-mappning. |
| environment.browserDetails.viewportWidth | bw | AppMeasurement-frågeparametern BROWSER_WIDTH-mappning. |
| environment.connectionType | ct | AppMeasurement-frågeparametern CT_CONNECT_TYPE-mappning. |
| environment.ipV4 | X-Forwarded-For | Det här är en HTTP-huvudmappning, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mitten | Mappning av parameter-MID för AppMeasurement-fråga. |
| marketing.trackingCode | v0 | AppMeasurement-frågeparametern CAMPAIGN-mappning. |
| media.mediaTimed.completes.value | c.a.media.complete | Kontextdata för AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Kontextdata för AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Kontextdata för AppMeasurement `c.a.media.federated` mappning. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Kontextdata för AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Kontextdata för AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Kontextdata för AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Kontextdata för AppMeasurement `c.a.media.pauseTime` mappning. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Kontextdata för AppMeasurement `c.a.media.pauseCount` mappning. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Kontextdata för AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Kontextdata för AppMeasurement `c.a.media.friendlyName` mappning. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Kontextdata för AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Kontextdata för AppMeasurement `c.a.media.episode` mappning. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Kontextdata för AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Kontextdata för AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Kontextdata för AppMeasurement `c.a.media.season` mappning. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Kontextdata för AppMeasurement `a.media.name` mappning. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Kontextdata för AppMeasurement `c.a.media.show` mappning. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Kontextdata för AppMeasurement `c.a.media.type` mappning med konverteringen VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Kontextdata för AppMeasurement `c.a.media.type` mappning med konvertering VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Kontextdata för AppMeasurement `c.a.media.length` mappning. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Kontextdata för AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Kontextdata för AppMeasurement `c.a.media.channel` mappning. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Kontextdata för AppMeasurement `c.a.contentType` mappning. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Kontextdata för AppMeasurement `c.a.media.network` mappning. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Kontextdata för AppMeasurement `c.a.media.segment` mappning. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Kontextdata för AppMeasurement `c.a.media.playerName` mappning. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Kontextdata för AppMeasurement `c.a.media.sdkVersion` mappning. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Kontextdata för AppMeasurement `c.a.media.feed` mappning. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Kontextdata för AppMeasurement `c.a.media.format` mappning. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Kontextdata för AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Kontextdata för AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Kontextdata för AppMeasurement `c.a.media.resume` mappning. |
| media.mediaTimed.starts.value | c.a.media.view | Kontextdata för AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Kontextdata för AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Kontextdata för AppMeasurement `c.a.media.timePlayed` mappning. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Kontextdata för AppMeasurement `c.a.media.totalTimePlayed` mappning. |
| placeContext.geo.latitude | lat | LATITUDE-mappning för parametern LATITUDE för AppMeasurement-fråga. |
| placeContext.geo.longitude | lon | AppMeasurement-frågeparameter LONGITUDE-mappning. |
| placeContext.geo.postalCode | zip | ZIP-mappning för parametern för AppMeasurement-fråga. |
| placeContext.geo.stateProvince | tillstånd | Parametern STATE-mappning för AppMeasurement-fråga. |
| productListItems[N].lineItemId | produkter | AppMeasurement-frågeparameter Produktkategorimappning. |
| productlistitems[N].name | produkter | AppMeasurement-frågeparameter Produktnamnsmappning. |
| productlistitems[N].priceTotal | produkter | AppMeasurement-frågeparametern Produkt, prismappning. |
| productlistitems[N].quantity | produkter | AppMeasurement-frågeparametern Produkt Kvantitetsmappning. |
| web.webInteraction.URL | pev1 | AppMeasurement-frågeparametern PAGE_EVENT_VAR1-mappning. |
| web.webInteraction.name | pev2 | AppMeasurement-frågeparametern PAGE_EVENT_VAR2-mappning. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` till `pe=lnk_o`; `web.webInteraction.type=download` till `pe=lnk_d`; `web.webInteraction.type=exit` till `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement-frågeparametern PAGE_URL-mappning. |
| web.webPageDetails.errorPage | pageType | AppMeasurement-frågeparametern PAGE_TYPE_FULL-mappning med konverteringen ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | AppMeasurement-frågeparametern HOMEPAGE-mappning med konverteringen BOOLEAN_TO_YN. |
| web.webPageDetails.name | signera | AppMeasurement-frågeparametern PAGENAME-mappning. |
| web.webPageDetails.server | sv | AppMeasurement-frågeparametern USER_SERVER-mappning. |
| web.webPageDetails.siteSection | ch | Mappning av parametern CHANNEL för parametern AppMeasurement-fråga. |
| web.webReferrer.URL | r | AppMeasurement-frågeparameterns REFERRER-mappning. |

{style="table-layout:auto"}
