---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics-mappningsfält
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '3328'
ht-degree: 0%

---


# Analytics-mappningsfält

Med Adobe Experience Platform kan du importera Adobe Analytics-data via Analytics Data Connector (ADC). Vissa data som hämtas via ADC kan mappas direkt från Analytics-fält till XDM-fält (Experience Data Model), medan andra data kräver omformningar och specifika funktioner för att kunna mappas.

![](../images/analytics-data-experience-platform.png)

## Direktmappningsfält

Utvalda fält mappas direkt från Adobe Analytics till Experience Data Model (XDM).

Följande tabell innehåller kolumner som visar namnet på Analytics-fältet (*Analytics-fältet*), motsvarande XDM-fält (*XDM-fält*) och dess typ (*XDM-typ*) samt en beskrivning av fältet (*Beskrivning*).

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Analytics | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | En anpassad variabel som kan ligga mellan 1 och 250. Varje organisation kommer att använda dessa anpassade eVars på olika sätt. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Anpassade trafikvariabler, som kan variera mellan 1 och 75. |
| m_browser | _experience.analytics.environment.browserID | heltal | Webbläsarens nummer-ID. |
| m_browser_height | environment.browserDetails.viewportHeight | heltal | Webbläsarens höjd i pixlar. |
| m_browser_width | environment.browserDetails.viewportWidth | heltal | Webbläsarens bredd i pixlar. |
| m_campaign | marketing.trackingCode | string | Variabeln som används i spårningskoddimensionen. |
| m_kanal | web.webPageDetails.siteSection | string | Variabeln som används i dimensionen Platsavsnitt. |
| m_domän | environment.domain | string | Variabeln som används i domändimensionen. Detta baseras på användarens internetleverantör. |
| m_geo_city | placeContext.geo.city | string | Namnet på träffens stad. Detta baseras på träffens IP-adress. |
| m_geo_dma | placeContext.geo.dmaID | heltal | Det numeriska ID:t för det demografiska området för träffen. Detta baseras på träffens IP-adress. |
| m_geo_region | placeContext.geo.stateProvince | string | Namnet på antingen delstat eller region för träffen. Detta baseras på träffens IP-adress. |
| m_geo_zip | placeContext.geo.postalCode | string | Träffens postnummer. Detta baseras på träffens IP-adress. |
| m_nyckelord | search.keywords | string | Variabeln som används i nyckelordsdimensionen. |
| m_os | _experience.analytics.environment.operatingSystemID | heltal | Det numeriska ID som representerar besökarens operativsystem. Detta baseras på kolumnen user_agent. |
| m_page_url | web.webPageDetails.URL | string | URL:en för sidträffen. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | En variabel som används för att fylla siddimensionen. |
| m_reference | web.webReferrer.URL | string | Föregående sidas URL. |
| m_search_page_num | search.pageDepth | heltal | Används av dimensionen Rankning för alla söksidor. Anger vilken sida av sökresultat din webbplats hade innan användaren klickade igenom till din webbplats. |
| m_state | _experience.analytics.customDimensions.stateProvince | string | State-variabel. |
| m_user_server | web.webPageDetails.server | string | En variabel som används i serverdimensionen. |
| m_zip | _experience.analytics.customDimensions.mailCode | string | En variabel som används för att fylla i postkodsdimensionen. |
| accept_language | environment.browserDetails.acceptLanguage | string | Visar alla godkända språk enligt HTTP-huvudet Accept-Language. |
| hemsida | web.webPageDetails.isHomePage | boolesk | Används inte längre. Anger om den aktuella URL:en är webbläsarens hemsida. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | Den version av JavaScript som stöds av webbläsaren. |
| user_agent | environment.browserDetails.userAgent | string | Användaragentsträngen som skickas i HTTP-huvudet. |
| mobileappid | program.</span>name | string | Mobilapp-ID:t som lagras i följande format: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | Namnet på den mobila enheten. I iOS lagras den som en kommaavgränsad 2-siffrig sträng. Det första talet representerar enhetsgenereringen och det andra numret representerar enhetsfamiljen. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Används av mobiltjänster. Representerar intressepunkten. |
| pointränteavstånd | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | tal | Används av mobiltjänster. Representerar räntepunktens avstånd. |
| mobileplaceprecision | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | tal | Samlas in från kontextdatavariabeln a.loc.acc. Anger GPS-noggrannheten i meter vid insamlingen. |
| mobileplaceccategory | placeContext.POIinteraction.POIDetail.category | string | Samlas in från kontextdatavariabeln a.loc.category. Beskriver kategorin för en viss plats. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Samlas in från kontextdatavariabeln a.loc.id. Identifierare för en viss intressepunkt. |
| video | media.mediaTimed.primaryAssetReference._id | string | Namnet på videon. |
| video | advertising.adAssetReference._id | string | Identifierare för annonstillgången. |
| videoinnehålltyp | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | Videoinnehållstypen. Den ställs automatiskt in på &quot;Video&quot; för alla videovyer. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | Den ruta där videobandspelaren finns. |
| videoadinpod | advertising.adAssetViewDetails.index | heltal | Positionen för Video Ad är i poden. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | Namnet på videospelaren. |
| videochchannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | Videokanalen. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | Namnet på Video Ad-spelaren. |
| videokort | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | Namnet på videokapitlet |
| videonamn | media.mediaTimed.primaryAssetReference._dc.title | string | Videonamnet. |
| videoadname | advertising.adAssetReference._dc.title | string | Namnet på Video Ad. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Videoprogram. |
| videosäsong | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Videosäsong. |
| videoavsnitt | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | string | Videoavsnitt. |
| videonätverk | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Videonätverk. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Videovisningstyp. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Videoannonser läses in. |
| videofeedtyp | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Typ av videofeed. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | tal | Mobiltjänster är en viktig del. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | tal | Mobiltjänster är mindre. |
| mobilebeaconuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | Mobiltjänster är UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID för videosession. |
| videogener | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Videogenre. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objekt | Detta utlöses vid den första körningen efter installation eller ominstallation | {id (sträng), value (number)} |
| mobileupgrades | application.upgrades | Objekt | Rapporterar antalet appuppgraderingar. Utlösare vid första körningen efter uppgraderingen eller när som helst när versionsnumret ändras. | {id (sträng), value (number)} |
| mobilenheter | application.launches | Objekt | Antalet gånger som appen har startats. | {id (sträng), value (number)} |
| mobilkrascher | application.crashes | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| mobilemessageclicks | directMarketing.clicks | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videotid | media.mediaTimed.timePlayed | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videostart | media.mediaTimed.impressions | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoslutförd | media.mediaTimed.completes | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videosegmentvyer | media.mediaTimed.mediaSegmentViews | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoadstart | advertising.impressions | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoadcomplete | advertising.completes | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoadtime | advertising.timePlayed | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videospela | media.mediaTimed.starts | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoqoetimetstart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objekt | Den tid det tar att starta videokvaliteten. | {id (sträng), value (number)} |
| videoQuoedropförstart | media.mediaTimed.dropBeforeStarts | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoqoebuffcount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objekt | Buffertantal för videokvalitet | {id (sträng), value (number)} |
| videoqoebufftime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objekt | Bufferttid för videokvalitet | {id (sträng), value (number)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objekt | Antal ändringar av videokvalitet | {id (sträng), value (number)} |
| videoqoebitrateGenomsnitt | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objekt | Genomsnittlig bithastighet för videokvalitet | {id (sträng), value (number)} |
| videoinspelningsfel | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objekt | Antal fel för videokvalitet | {id (sträng), value (number)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoprogress10 | media.mediaTimed.progress10 | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoprogress25 | media.mediaTimed.progress25 | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoprogress50 | media.mediaTimed.progress50 | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoprogress75 | media.mediaTimed.progress75 | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoprogress95 | media.mediaTimed.progress95 | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videoresume | media.mediaTimed.resumes | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videopausecount | media.mediaTimed.pauses | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videopausetime | media.mediaTimed.pauseTime | Objekt | <!-- MISSING --> | {id (sträng), value (number)} |
| videosekunderIncelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | heltal |

## Dela mappningsfält

Dessa fält har en enda källa, men mappas till **flera** XDM-platser.

| Analytics | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | heltal | Numeriskt ID som representerar bildskärmens upplösning. |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | string | Mobil operativsystemversion. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | heltal | Längd på videoreklam. |

## Genererade mappningsfält

Utvalda fält från ADC måste omformas, vilket kräver logik utöver en direkt kopia från Adobe Analytics för att kunna genereras i XDM.

Följande tabell innehåller kolumner som visar namnet på Analytics-fältet (*Analytics-fältet*), motsvarande XDM-fält (*XDM-fält*) och dess typ (*XDM-typ*) samt en beskrivning av fältet (*Beskrivning*).

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Analytics | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Anpassade trafikvariabler, från 1 till 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarkies.hier5 | Objekt | Används av hierarkivariabler. Den innehåller en | avgränsad lista med värden. | {values (array), delimiter (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementeringen | {value (string), key (string)} |
| m_color | device.colorDepth | heltal | ID för färgdjup, som baseras på värdet för kolumnen c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | boolesk | En variabel som används i Cookie-supportdimensionen. |
| m_event_list | commerce.purchasing, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objekt | Standardhändelser för e-handel utlöste träffen. | {id (sträng), value (number)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event300 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event55 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objekt | Anpassade händelser som utlöses vid träffen. | {id (Object), value (Object)} |
| m_geo_country | placeContext.geo.countryCode | string | Förkortning av det land varifrån träffen kom, vilket baseras på undersökningsperioden. |
| m_geo_latitude | placeContext.geo._schema.latitude | tal | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitud | tal | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | boolesk | En flagga som anger om Java är aktiverat. |
| m_latitude | placeContext.geo._schema.latitude | tal | <!-- MISSING --> |
| m_longitud | placeContext.geo._schema.longitud | tal | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | string | En variabel som bara används för bildbegäran för länkspårning. Den här variabeln innehåller URL:en för den nedladdningslänk, den avslutningslänk eller anpassade länk som du klickat på. |
| m_page_event_var2 | web.webInteraction.name | string | En variabel som bara används för bildbegäran för länkspårning. Här visas länkens egna namn, om det har angetts. |
| m_page_type | web.webPageDetails.isErrorPage | boolesk | En variabel som används för att fylla i dimensionen Ej hittade sidor. Variabeln ska antingen vara tom eller innehålla ErrorPage. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | tal | Namnet på sidan (om den har angetts). Om ingen sida har angetts är det här värdet tomt. |
| m_paid_search | search.isPaid | boolesk | En flagga som anges om träffen matchar betalsökningsidentifiering. |
| m_product_list | productListItems[].items | array | Produktlistan, som den skickas via variabeln products. | {SKU (sträng), quantity (heltal), priceTotal (tal)} |
| m_ref_type | web.webReferrer.type | string | Ett numeriskt ID som representerar typen av referens för träffen. 1 betyder inom er webbplats, 2 betyder andra webbplatser, 3 betyder sökmotorer, 4 betyder hårddisk, 5 betyder USENET, 6 betyder Typed/Bookmarked (ingen referent), 7 betyder e-post, 8 betyder Inget JavaScript och 9 betyder Sociala nätverk. |
| m_search_engine | search.searchEngine | string | Det numeriska ID som representerar sökmotorn som refererade besökaren till din webbplats. |
| post_currency | commerce.order.currencyCode | string | Valutakoden som användes under transaktionen. |
| post_cust_hit_time_gmt | tidsstämpel | string | Detta används endast i tidsstämpelaktiverade datauppsättningar. Det här är den tidsstämpel som skickas med den, baserat på Unix-tid. |
| post_cust_visid | identityMap | object | Kundens besökar-ID. |
| post_cust_visid | endUserID:n._experience.acustomid.primär | boolesk | Kundens besökar-ID. |
| post_cust_visid | endUserID:n._experience.acustomid.namespace.code | string | Kundens besökar-ID. |
| post_visid_high + visid_low | identityMap | object | En unik identifierare för ett besök. |
| post_visid_high + visid_low | endUserID:n._experience.aaid.id | string | En unik identifierare för ett besök. |
| post_visid_high | endUserID:n._experience.aaid.primär | boolesk | Används tillsammans med visid_low för att unikt identifiera ett besök. |
| post_visid_high | endUserID:n._experience.aaid.namespace.code | string | Används tillsammans med visid_low för att unikt identifiera ett besök. |
| post_visid_low | identityMap | object | Används tillsammans med visid_high för att unikt identifiera ett besök. |
| hit_time_gmt | receiveTimestamp | string | Tidsstämpeln för träffen, baserad på Unix-tid. |
| hitid_high + hitid_low | _id | string | En unik identifierare som identifierar en träff. |
| hitid_low | _id | string | Används tillsammans med hitid_high för att unikt identifiera en träff. |
| ip | environment.ipV4 | string | IP-adressen, baserad på HTTP-huvudet i bildbegäran. |
| j_jscript | environment.browserDetails.javaScriptEnabled | boolesk | Den version av JavaScript som används. |
| mcvisid_high + mcvisid_low | identityMap | object | Experience Cloud Visitor-ID. |
| mcvisid_high + mcvisid_low | endUserID:n._experience.mcid.id | string | Experience Cloud Visitor-ID. |
| mcvisid_high | endUserID:n._experience.mcid.primär | boolesk | Experience Cloud Visitor-ID. |
| mcvisid_high | endUserID:n._experience.mcid.namespace.code | string | Experience Cloud Visitor-ID. |
| mcvisid_low | identityMap | object | Experience Cloud Visitor-ID. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | string | Tryck på Stitching ID. Analysfältet sdid_high och sdid_low är det kompletterande data-id som används för att sammanfoga två (eller flera) inkommande träffar. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Mobiltjänster är nära. |
| videokort | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | heltal | Namnet på videokapitlet. |
| videolängd | media.mediaTimed.primaryAssetReference._xmpDM.duration | heltal | Videons längd. |

## Avancerade mappningsfält

Markera fält (så kallade postvärden) kräver mer avancerade omvandlingar innan de kan mappas från Adobe Analytics-fält till Experience Data Model (XDM). För dessa avancerade omvandlingar används Adobe Experience Platfrom Query Service och fördefinierade funktioner (som kallas Adobe-definierade funktioner) för sessioner, attribuering och borttagning av dubbletter.

Mer information om hur du utför dessa omvandlingar med hjälp av Query Service finns i dokumentationen för [Adobes definierade funktioner](../../../../query-service/sql/adobe-defined-functions.md) .

Följande tabell innehåller kolumner som visar namnet på Analytics-fältet (*Analytics-fältet*), motsvarande XDM-fält (*XDM-fält*) och dess typ (*XDM-typ*) samt en beskrivning av fältet (*Beskrivning*).

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Analytics | XDM-fält | XDM-typ | Beskrivning |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | En anpassad variabel som kan ligga mellan 1 och 250. Varje organisation kommer att använda dessa anpassade eVars på olika sätt. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Anpassade trafikvariabler, som kan variera mellan 1 och 75. |
| post_browser_height | environment.browserDetails.viewportHeight | heltal | Webbläsarens höjd i pixlar. |
| post_browser_width | environment.browserDetails.viewportWidth | heltal | Webbläsarens bredd i pixlar. |
| post_campaign | marketing.trackingCode | string | Variabeln som används i spårningskoddimensionen. |
| post_channel | web.webPageDetails.siteSection | string | Variabeln som används i dimensionen Platsavsnitt. |
| post_cust_visid | endUserID:n._experience.acustomid.id | string | Anpassat besökar-ID, om det är angivet. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | URL:en för den första sidan som besökaren når. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | En variabel som används i dimensionen Ursprungligt på startsidan. Sidnamnet på besökarens startsida. |
| post_keywords | search.keywords | string | Nyckelorden som samlades in för träffen. |
| post_page_url | web.webPageDetails.URL | string | URL:en för sidträffen. |
| post_pagename_no_url | web.webPageDetails.name | string | En variabel som används för att fylla siddimensionen. |
| post_purchase_eid | commerce.order.purchaseID | string | Variabel som används för att unikt identifiera inköp. |
| post_reference | web.webReferrer.URL | string | Föregående sidas URL. |
| post_state | _experience.analytics.customDimensions.stateProvince | string | State-variabel. |
| post_user_server | web.webPageDetails.server | string | En variabel som används i serverdimensionen. |
| post_zip | _experience.analytics.customDimensions.mailCode | string | En variabel som används för att fylla i postkodsdimensionen. |
| webbläsare | _experience.analytics.environment.browserID | heltal | Webbläsarens numeriska ID. |
| domän | environment.domain | string | Variabeln som används i domändimensionen. Detta baseras på användarens internetleverantör. |
| first_hit_reference | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | Den första refererande URL:en för besökaren. |
| geo_city | placeContext.geo.city | string | Namnet på träffens stad. Detta baseras på träffens IP-adress. |
| geo_dma | placeContext.geo.dmaID | heltal | Det numeriska ID:t för det demografiska området för träffen. Detta baseras på träffens IP-adress. |
| geo_region | placeContext.geo.stateProvince | string | Namnet på antingen delstat eller region för träffen. Detta baseras på träffens IP-adress. |
| geo_zip | placeContext.geo.postalCode | string | Träffens postnummer. Detta baseras på träffens IP-adress. |
| os | _experience.analytics.environment.operatingSystemID | heltal | Det numeriska ID som representerar besökarens operativsystem. Detta baseras på kolumnen user_agent. |
| search_page_num | search.pageDepth | heltal | Den här variabeln används av dimensionen Rankning för alla söksidor, och anger vilken sida av sökresultaten för webbplatsen | visades innan användaren klickade igenom till din plats. |
| besök_nyckelord | _experience.analytics.session.search.keywords | string | En variabel som används i dimensionen Sök nyckelord. |
| besök_num | _experience.analytics.session.num | heltal | En variabel som används i dimensionen Besöksnummer. Detta börjar vid 1 och ökar stegvis varje gång ett nytt besök startar (per användare). |
| besök_sidnummer | _experience.analytics.session.depth | heltal | En variabel som används i dimensionen Träff. Värdet ökar med 1 för varje träff som användaren skapar och återställs efter varje besök. |
| visit_reference | _experience.analytics.session.web.webReferrer.URL | string | Den första referenten till besöket. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | heltal | Besökets första sidnamn. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Anpassade trafikvariabler 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarkies.hier5 | Objekt | Används av hierarkivariabler och innehåller en avgränsad lista med värden. | {values (array), delimiter (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | En lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. | {value (string), key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | boolesk | Variabel som används i Cookie-supportdimensionen. |
| post_event_list | commerce.purchasing, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objekt | Standardhändelser för e-handel utlöste träffen. | {id (sträng), value (number)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event300 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event55 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objekt | Anpassade händelser som utlöses vid träffen. | {id (Object), value (Object)} |
| post_java_enabled | environment.browserDetails.javaEnabled | boolesk | En flagga som anger om Java är aktiverat. |
| post_latitude | placeContext.geo._schema.latitude | tal | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitud | tal | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | string | Den typ av träff som skickas i bildbegäran (standardträff, nedladdningslänk, slutlänk eller anpassad länk som klickats). |
| post_page_event | web.webInteraction.linkClicks.value | tal | Den typ av träff som skickas i bildbegäran (standardträff, nedladdningslänk, slutlänk eller anpassad länk som klickats). |
| post_page_event_var1 | web.webInteraction.URL | string | Den här variabeln används bara för förfrågningar om länkspårningsbilder. Det här är URL:en för den nedladdningslänk, avslutningslänk eller anpassade länk som du klickat på. |
| post_page_event_var2 | web.webInteraction.name | string | Den här variabeln används bara för förfrågningar om länkspårningsbilder. Det här blir länkens egna namn. |
| post_page_type | web.webPageDetails.isErrorPage | boolesk | Detta används för att fylla i dimensionen Sidor som inte hittades. Variabeln ska antingen vara tom eller innehålla &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | tal | Namnet på sidan (om den har angetts). Om ingen sida har angetts är det här värdet tomt. |
| post_product_list | productListItems[].items | array | Produktlistan, som den skickas via variabeln products. | {SKU (sträng), quantity (heltal), priceTotal (tal)} |
| post_search_engine | search.searchEngine | string | Det numeriska ID som representerar sökmotorn som refererade besökaren till din webbplats. |
| mvvar1_instances | .list.items[] | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
| mvvar2_instances | .list.items[] | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
|  | mvvar3_instances | .list.items[] | Objekt | Lista med variabelvärden. Innehåller en avgränsad lista med anpassade värden, beroende på implementering. |
| färg | device.colorDepth | heltal | ID för färgdjup, baserat på värdet för kolumnen c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | Det numeriska ID:t som representerar referenstypen för besökarens allra första referent. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | heltal | Tidsstämpel för besökarens första träff i Unix-tid. |
| geo_country | placeContext.geo.countryCode | string | Förkortning av det land som träffen kom från, baserat på IP. |
| geo_latitude | placeContext.geo._schema.latitude | tal | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitud | tal | <!-- MISSING --> |
| paid_search | search.isPaid | boolesk | En flagga som anges om träffen matchar betalsökningsidentifiering. |
| ref_type | web.webReferrer.type | string | Ett numeriskt ID som representerar typen av referens för träffen. |
| visit_paid_search | _experience.analytics.session.search.isPaid | boolesk | En flagga (1=betald, 0=inte betald) som anger om besökets första träff kom från en betald sökträff. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | string | Numeriskt ID som representerar referenstypen för besökets första referent. |
| besök_search_engine | _experience.analytics.session.search.searchEngine | string | Numeriskt ID för besökets första sökmotor. |
| besök_start_time_gmt | _experience.analytics.session.timestamp | heltal | Tidsstämpel för besökets första träff i Unix-tid. |
