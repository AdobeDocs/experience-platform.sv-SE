---
keywords: Analysmappningsfält;analysmappning
solution: Experience Platform
title: Mappningsfält för Adobe Analytics Source Connector
description: Mappa Adobe Analytics-fält till XDM-fält med Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: ae8a54f8e9fafe782cb24e54e5b638d83d468e3a
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 0%

---

# Mappningar av analysfält

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics-källan. Vissa data som hämtas via ADC kan mappas direkt från analysfält till XDM-fält (Experience Data Model), medan andra data kräver att omvandlingar och specifika funktioner mappas.

![](../images/analytics-data-experience-platform.png)

## Direktmappningsfält

Markerade fält mappas direkt från Adobe Analytics till Experience Data Model (XDM).

| Analysfält | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | eVars för anpassade analyser. Varje organisation kan använda eVars på olika sätt. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | string | Custom Analytics-proppar. Varje organisation kan använda olika uttryck. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | heltal | Webbläsarens nummer-ID. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | heltal | Webbläsarens höjd i pixlar. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | heltal | Webbläsarens bredd i pixlar. |
| `m_campaign` | `marketing.trackingCode` | string | Variabeln som används i spårningskoddimensionen. |
| `m_channel` | `web.webPageDetails.siteSection` | string | Variabeln som används i dimensionen Platsavsnitt. |
| `m_domain` | `environment.domain` | string | Variabeln som används i domändimensionen. Den baseras på användarens internetleverantör. |
| `m_geo_city` | `placeContext.geo.city` | string | Namnet på träffens stad. Detta baseras på träffens IP-adress. |
| `m_geo_dma` | `placeContext.geo.dmaID` | heltal | Numeriskt ID för det demografiska området för träffen. Detta baseras på träffens IP-adress. |
| `m_geo_region` | `placeContext.geo.stateProvince` | string | Namnet på antingen delstat eller region för träffen. Detta baseras på träffens IP-adress. |
| `m_geo_zip` | `placeContext.geo.postalCode` | string | Träffens postnummer. Detta baseras på träffens IP-adress. |
| `m_keywords` | `search.keywords` | string | Variabeln som används i nyckelordsdimensionen. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | heltal | Det numeriska ID som representerar besökarens operativsystem. Detta baseras på kolumnen user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | string | URL:en för sidträffen. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | string | Lika med 1 i träffar som har ett sidnamn. Detta liknar måttet för Adobe Analytics sidvisning. |
| `m_referrer` | `web.webReferrer.URL` | string | Föregående sidas URL. |
| `m_search_page_num` | `search.pageDepth` | heltal | Används av dimensionen Rankning för alla söksidor. Anger vilken sida av sökresultat din webbplats hade innan användaren klickade igenom till din webbplats. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string | State-variabel. |
| `m_user_server` | `web.webPageDetails.server` | string | En variabel som används i serverdimensionen. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | string | En variabel som används för att fylla i postkodsdimensionen. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | string | Visar alla godkända språk enligt HTTP-huvudet Accept-Language. |
| `homepage` | `web.webPageDetails.isHomePage` | boolesk | Används inte längre. Anger om den aktuella URL:en är webbläsarens hemsida. |
| `ipv6` | `environment.ipV6` | string |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | string | Den version av JavaScript som stöds av webbläsaren. |
| `user_agent` | `environment.browserDetails.userAgent` | string | Användaragentsträngen som skickas i HTTP-huvudet. |
| `mobileappid` | `application.name` | string | Mobilapp-ID:t som lagras i följande format: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | string | Namnet på den mobila enheten. I iOS lagras den som en kommaavgränsad tvåsiffrig sträng. Det första talet representerar enhetsgenereringen och det andra numret representerar enhetsfamiljen. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | string | Används av mobiltjänster. Representerar intressepunkten. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | tal | Används av mobiltjänster. Representerar räntepunktens avstånd. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | tal | Samlas in från kontextdatavariabeln a.loc.acc. Anger GPS-noggrannheten i meter vid insamlingen. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | string | Samlas in från kontextdatavariabeln a.loc.category. Beskriver kategorin för en viss plats. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | string | Samlas in från kontextdatavariabeln a.loc.id. Identifierare för en viss intressepunkt. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | string | Namnet på videon. |
| `videoad` | `advertising.adAssetReference._id` | string | Identifierare för annonstillgången. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | string | Videoinnehållstypen. Den ställs automatiskt in på &quot;Video&quot; för alla videovyer. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | string | Den ruta där videobandspelaren finns. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | heltal | Positionen för Video Ad är i poden. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | string | Namnet på videospelaren. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | string | Videokanalen. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | string | Namnet på Video Ad Player. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | string | Namnet på videokapitlet |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | string | Videonamnet. |
| `videoadname` | `advertising.adAssetReference._dc.title` | string | Namnet på Video Ad. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | string | Videoprogram. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | string | Videosäsong. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | string | Videoavsnitt. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | string | Videonätverk. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | string | Videovisningstyp. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | string | Videoannonser läses in. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | string | Typ av videofeed. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | tal | Mobiltjänster är en viktig del. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | tal | Mobiltjänster är mindre. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | string | Mobiltjänster är UUID. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | string | ID för videosession. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | array | Videogenre. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| `mobileinstalls` | `application.firstLaunches` | Objekt | Detta utlöses första gången efter installation eller ominstallation | {id (sträng), value (number)} |
| `mobileupgrades` | `application.upgrades` | Objekt | Rapporterar antalet appuppgraderingar. Utlösare vid första körningen efter uppgraderingen eller när som helst när versionsnumret ändras. | {id (sträng), value (number)} |
| `mobilelaunches` | `application.launches` | Objekt | Antalet gånger som appen har startats. | {id (sträng), value (number)} |
| `mobilecrashes` | `application.crashes` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videotime` | `media.mediaTimed.timePlayed` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videostart` | `media.mediaTimed.impressions` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videocomplete` | `media.mediaTimed.completes` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoadstart` | `advertising.impressions` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoadcomplete` | `advertising.completes` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoadtime` | `advertising.timePlayed` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoplay` | `media.mediaTimed.starts` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objekt | Den tid det tar att starta videokvaliteten. | {id (sträng), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objekt | Buffertantal för videokvalitet | {id (sträng), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objekt | Bufferttid för videokvalitet | {id (sträng), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objekt | Antal ändringar av videokvalitet | {id (sträng), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objekt | Genomsnittlig bithastighet för videokvalitet | {id (sträng), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objekt | Antal fel för videokvalitet | {id (sträng), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videoresume` | `media.mediaTimed.resumes` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videopausecount` | `media.mediaTimed.pauses` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | heltal |

{style="table-layout:auto"}

## Fält för delad mappning

Dessa fält har en enda källa, men mappas till **flera** XDM-platser.

| Analysfält | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | heltal | Numeriskt ID som representerar bildskärmens upplösning. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | string | Mobil operativsystemversion. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | heltal | Längd på videoreklam. |

{style="table-layout:auto"}

## Genererade mappningsfält

Markera fält som kommer från ADC måste omformas, vilket kräver logik utöver en direkt kopia från Adobe Analytics för att kunna genereras i XDM.

| Analysfält | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objekt | Anpassade analysprops, konfigurerade som listprops. Den innehåller en avgränsad lista med värden. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objekt | Används av hierarkivariabler. Den innehåller en avgränsad lista med värden. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Listvariabler för anpassade analyser. Innehåller en avgränsad lista med värden. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | heltal | ID för färgdjup, som baseras på värdet för kolumnen c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | boolesk | En variabel som används i Cookie-supportdimensionen. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objekt | Standardhändelser för e-handel utlöste träffen. | {id (sträng), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Anpassade händelser som utlöses vid träffen. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | string | Förkortning av det land där träffen kom från, vilket baseras på undersökningsperioden. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | tal | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | tal | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | boolesk | En flagga som anger om Java™ är aktiverat. |
| `m_latitude` | `placeContext.geo._schema.latitude` | tal | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | tal | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | string | En variabel som bara används för bildbegäran för länkspårning. Den här variabeln innehåller URL:en för den nedladdningslänk, den avslutningslänk eller anpassade länk som du klickat på. |
| `m_page_event_var2` | `web.webInteraction.name` | string | En variabel som bara används för bildbegäran för länkspårning. Här visas länkens egna namn, om det har angetts. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | boolesk | En variabel som används för att fylla i dimensionen Sidor som inte hittades. Variabeln ska antingen vara tom eller innehålla ErrorPage. |
| `m_pagename_no_url` | `web.webPageDetails.name` | tal | Namnet på sidan (om den har angetts). Om ingen sida anges lämnas värdet tom. |
| `m_paid_search` | `search.isPaid` | boolesk | En flagga som anges om träffen matchar betalsökningsidentifiering. |
| `m_product_list` | `productListItems[].items` | array | Produktlistan, som den skickas via variabeln products. | {SKU (sträng), quantity (heltal), priceTotal (tal)} |
| `m_ref_type` | `web.webReferrer.type` | string | Ett numeriskt ID som representerar typen av referens för träffen.<br/>`1`: Inuti din webbplats<br/>`2`: Andra webbplatser<br/>`3`: Sökmotorer<br/>`4`: Hårddisk<br/>`5`: USENET<br/>`6`: Typed/Bookmarked (ingen referent)<br/>`7`: e-post<br/>`8`: Ingen JavaScript<br/>`9`: Sociala nätverk |
| `m_search_engine` | `search.searchEngine` | string | Det numeriska ID som representerar sökmotorn som refererade besökaren till din webbplats. |
| `post_currency` | `commerce.order.currencyCode` | string | Valutakoden som användes under transaktionen. |
| `post_cust_hit_time_gmt` | `timestamp` | string | Detta används endast i tidsstämpelaktiverade datauppsättningar. Det här är den tidsstämpel som skickas med träffen, baserat på UNIX®-tid. |
| `post_cust_visid` | `identityMap` | object | Kundens besökar-ID. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | boolesk | Kundens besökar-ID. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | string | Kundens besökar-ID. |
| `post_visid_high` + `visid_low` | `identityMap` | object | En unik identifierare för ett besök. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | string | En unik identifierare för ett besök. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | boolesk | Används med `visid_low` för att unikt identifiera ett besök. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | string | Används med `visid_low` för att unikt identifiera ett besök. |
| `post_visid_low` | `identityMap` | object | Används med visid_high för att unikt identifiera ett besök. |
| `hit_time_gmt` | `receivedTimestamp` | string | Tidsstämpeln för träffen, baserad på UNIX®-tid. |
| `hitid_high` + `hitid_low` | `_id` | string | En unik identifierare som identifierar en träff. |
| `hitid_low` | `_id` | string | Används med hitid_high för att unikt identifiera en träff. |
| `ip` | `environment.ipV4` | string | IP-adressen, baserad på HTTP-huvudet i bildbegäran. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | boolesk | Den version av JavaScript som användes. |
| `mcvisid_high` + `mcvisid_low` | identityMap | object | Experience Cloud Visitor-ID. |
| `mcvisid_high` + `mcvisid_low` | endUserID:n._experience.mcid.id | string | Experience Cloud-id (ECID) kallas även MCID och används ibland i namnutrymmen. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | boolesk | Experience Cloud-id (ECID) kallas även MCID och används ibland i namnutrymmen. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | string | Experience Cloud-id (ECID) kallas även MCID och används ibland i namnutrymmen. |
| `mcvisid_low` | `identityMap` | object | Experience Cloud Visitor-ID. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | string | Tryck på Stitching ID. Analysfältet sdid_high och sdid_low är det kompletterande data-id som används för att sammanfoga två (eller flera) inkommande träffar. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | string | Mobiltjänster är nära. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | heltal | Namnet på videokapitlet. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | heltal | Videons längd. |

{style="table-layout:auto"}

## Avancerade mappningsfält

Markera fält (så kallade&quot;postvärden&quot;) innehåller data efter att Adobe har justerat deras värden med bearbetningsregler, VISTA-regler och uppslagstabeller. De flesta postvärden har en förbearbetad motsvarighet.

Analysens källanslutning skickar förbearbetade data till en datauppsättning i Experience Platform. Du kan omvandla dessa data till dess efterbearbetade motsvarighet med hjälp av omformningar. Mer information om hur du utför dessa omformningar med hjälp av frågetjänsten finns i [Adobe-definierade funktioner](/help/query-service/sql/adobe-defined-functions.md) i användarhandboken för frågetjänsten.

Mer information om hur du utför dessa omformningar med hjälp av frågetjänsten finns i [Adobe-definierade funktioner](/help/query-service/sql/adobe-defined-functions.md) i användarhandboken för frågetjänsten.

| Analysfält | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | eVars för anpassade analyser. Varje organisation kan använda eVars på olika sätt. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | string | Custom Analytics-proppar. Varje organisation kan använda olika uttryck. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | heltal | Webbläsarens höjd i pixlar. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | heltal | Webbläsarens bredd i pixlar. |
| `post_campaign` | `marketing.trackingCode` | string | Variabeln som används i spårningskoddimensionen. |
| `post_channel` | `web.webPageDetails.siteSection` | string | Variabeln som används i dimensionen Platsavsnitt. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | string | Anpassat besökar-ID, om det är angivet. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | string | URL:en för den första sidan som besökaren når. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | string | En variabel som används i dimensionen Ursprungligt på startsidan. Sidnamnet på besökarens startsida. |
| `post_keywords` | `search.keywords` | string | Nyckelorden som samlades in för träffen. |
| `post_page_url` | `web.webPageDetails.URL` | string | URL:en för sidträffen. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | string | Lika med 1 i träffar som har ett sidnamn. Detta liknar måttet för Adobe Analytics sidvisning. |
| `post_purchaseid` | `commerce.order.purchaseID` | string | Variabel som används för att unikt identifiera inköp. |
| `post_referrer` | `web.webReferrer.URL` | string | Föregående sidas URL. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string | State-variabel. |
| `post_user_server` | `web.webPageDetails.server` | string | En variabel som används i serverdimensionen. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | string | En variabel som används för att fylla i postkodsdimensionen. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | heltal | Webbläsarens numeriska ID. |
| `domain` | `environment.domain` | string | Variabeln som används i domändimensionen. Den baseras på användarens internetleverantör. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | string | Den första refererande URL:en för besökaren. |
| `geo_city` | `placeContext.geo.city` | string | Namnet på träffens stad. Detta baseras på träffens IP-adress. |
| `geo_dma` | `placeContext.geo.dmaID` | heltal | Numeriskt ID för det demografiska området för träffen. Detta baseras på träffens IP-adress. |
| `geo_region` | `placeContext.geo.stateProvince` | string | Namnet på antingen delstat eller region för träffen. Detta baseras på träffens IP-adress. |
| `geo_zip` | `placeContext.geo.postalCode` | string | Träffens postnummer. Detta baseras på träffens IP-adress. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | heltal | Det numeriska ID som representerar besökarens operativsystem. Detta baseras på kolumnen user_agent. |
| `search_page_num` | `search.pageDepth` | heltal | Den här variabeln används av dimensionen Rankning för alla söksidor, och anger vilken sida av sökresultaten för webbplatsen | visades innan användaren klickade igenom till din plats. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | string | En variabel som används i söknyckelordsdimensionen. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | heltal | En variabel som används i dimensionen Besöksnummer. Detta börjar vid 1 och ökar stegvis varje gång ett nytt besök startar (per användare). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | heltal | En variabel som används i dimensionen Träff. Värdet ökar med 1 för varje träff som användaren skapar och återställs efter varje besök. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | string | Den första referenten till besöket. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | heltal | Besökets första sidnamn. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objekt | Anpassade analysprops, konfigurerade som listprops. Den innehåller en avgränsad lista med värden. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objekt | Används av hierarkivariabler och innehåller en avgränsad lista med värden. | {values (array), delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | En lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | boolesk | Variabel som används i Cookie-supportdimensionen. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objekt | Standardhändelser för e-handel utlöste träffen. | {id (sträng), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Anpassade händelser som utlöses vid träffen. | {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | boolesk | En flagga som anger om Java™ är aktiverat. |
| `post_latitude` | `placeContext.geo._schema.latitude` | tal | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | tal | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | string | Den typ av träff som skickas i bildbegäran (standardträff, nedladdningslänk, slutlänk eller anpassad länk som klickats). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | tal | Lika med 1 om träffen är ett länkklick. Detta liknar måttet för sidhändelser i Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | string | Den här variabeln används bara för förfrågningar om länkspårningsbilder. Det är URL:en för den nedladdningslänk, avslutningslänk eller anpassade länk som du klickar på. |
| `post_page_event_var2` | `web.webInteraction.name` | string | Den här variabeln används bara för förfrågningar om länkspårningsbilder. Det är länkens egna namn. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | boolesk | Detta används för att fylla i dimensionen Sidor som inte hittades. Variabeln ska antingen vara tom eller innehålla &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | tal | Namnet på sidan (om den har angetts). Om ingen sida anges lämnas värdet tom. |
| `post_product_list` | `productListItems[].items` | array | Produktlistan, som den skickas via variabeln products. | {SKU (sträng), quantity (heltal), priceTotal (tal)} |
| `post_search_engine` | `search.searchEngine` | string | Det numeriska ID som representerar sökmotorn som refererade besökaren till din webbplats. |
| `mvvar1_instances` | `.list.items[]` | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
| `mvvar2_instances` | `.list.items[]` | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
| `mvvar3_instances` | `.list.items[]` | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
| `color` | `device.colorDepth` | heltal | ID för färgdjup, baserat på värdet för kolumnen c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | string | Det numeriska ID:t som representerar referenstypen för besökarens första referent. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | heltal | Tidsstämpel för besökarens första träff i UNIX®-tid. |
| `geo_country` | `placeContext.geo.countryCode` | string | Förkortning av det land som träffen kom från, baserat på IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | tal | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | tal | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | boolesk | En flagga som anges om träffen matchar betalsökningsidentifiering. |
| `ref_type` | `web.webReferrer.type` | string | Ett numeriskt ID som representerar typen av referens för träffen. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | boolesk | En flagga (1=betald, 0=inte betald) som anger om besökets första träff kom från en betald sökträff. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | string | Numeriskt ID som representerar referenstypen för besökets första referent. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | string | Numeriskt ID för besökets första sökmotor. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | heltal | Tidsstämpel för första besöket på UNIX®-tid. |

{style="table-layout:auto"}