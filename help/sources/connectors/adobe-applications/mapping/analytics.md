---
title: Mappningsfält för Adobe Analytics Source Connector
description: Mappa Adobe Analytics-fält till XDM-fält med Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 0%

---

# Mappningar av analysfält

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics-källan. Vissa data som hämtas via ADC kan mappas direkt från analysfält till XDM-fält (Experience Data Model), medan andra data kräver att omvandlingar och specifika funktioner mappas.

![En illustration av Adobe Analytics dataöverföring från Analytics till Experience Platform.](../images/analytics-data-experience-platform.png)

## Parametrar för direktuppspelande media

I följande tabell finns information om parametrar för direktuppspelningsmedia.

| Datafeed | Sökväg till XDM-fält | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | string | Videons egna (läsbara) namn. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | string | Namnet på mediets författare. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | string | Namnet på den albumartist eller grupp som utför musikinspelningen eller videon. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | string | Namnet på det album som musikinspelningen eller videon tillhör. |
| `videolength` | `mediaReporting.sessionDetails.length ` | heltal | Videons längd eller körningsmiljö. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | string |
| `video` | `mediaReporting.sessionDetails.name` | string | Videons ID. |
| `videoshow` | `mediaReporting.sessionDetails.show` | string | Namnet på programmet eller serien. Program-/serienamnet krävs bara om programmet ingår i en serie. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | string | Typ av direktuppspelningsmedia som &quot;video&quot; eller &quot;ljud&quot;. |
| `videoseason` | `mediaReporting.sessionDetails.season` | string | Det säsongsnummer som programmet tillhör. Det här värdet är bara obligatoriskt om programmet ingår i en serie. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | string | Antal avsnitt. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | sträng[] | Videons genre. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | string | En identifierare för en instans av en innehållsström som är unik för en enskild uppspelning. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | string | Namnet på videospelaren. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | string | Distributionskanalen som innehållet spelades upp från. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | string | Den typ av strömleverans som används för innehållet. Den ställs automatiskt in på &quot;Video&quot; för alla videovyer. Rekommenderade värden är: VOD, Live, Linear, UGC, DVOD, Radio, Podcast, Audiobook och Song. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | string | Nätverks- eller kanalnamnet. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | string | Typen av feed. Detta kan antingen representera faktiska matningsrelaterade data som&quot;East HD&quot; eller&quot;SD&quot;, eller källan till matningen, t.ex. en URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | string |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | boolesk | Ett booleskt värde som anger om videon har startats eller inte. Detta inträffar när användaren väljer uppspelningsknappen och kommer att räkna även om det finns pre-roll-annonser, buffring, fel osv. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | boolesk | Ett booleskt värde som anger om den första bildrutan i mediet har startats. Om användaren hoppar under någon annons eller buffringstid är&quot;innehållsstart&quot; inte berättigad. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | heltal | Varaktigheten (i sekunder) för alla händelser för `type=PLAY` i huvudinnehållet. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | boolesk | Ett booleskt värde som anger om en medieresurs med tidsåtgång har bevakats tills den har slutförts. Det här värdet behöver inte nödvändigtvis innebära att användaren har tittat på hela videon eftersom det här värdet inte tar hänsyn till att läsaren kan hoppa över det här steget. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | heltal | Den totala tid som en användare tillbringar med en viss medieresurs, inklusive den tid som tillbringats med att titta på annonser. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | heltal | Summan av de unika intervall som en användare ser på en medieresurs med tidsangivelser. Med andra ord räknas längden på uppspelningsintervall som visas flera gånger bara en gång. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | tal | Genomsnittlig innehållstid för ett visst medieobjekt. Med andra ord, den totala innehållstiden dividerad med längden för alla uppspelningssessioner. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | boolesk | Ett booleskt värde som anger om spelhuvudet för en viss video har passerat 10 %-markören för den totala videolängden. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | boolesk | Ett booleskt värde som anger om spelhuvudet för en viss video har passerat 25 %-markören för den totala videolängden. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | boolesk | Ett booleskt värde som anger om spelhuvudet för en viss video har passerat 50 %-markören för den totala videolängden. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | boolesk | Ett booleskt värde som anger om spelhuvudet för en viss video har passerat 75 %-markören för den totala videolängden. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | boolesk | Ett booleskt värde som anger om spelhuvudet för en viss video har passerat 95 %-markören för den totala videolängden. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | boolesk | Ett booleskt värde som anger om en eller flera pauser inträffade under uppspelningen av ett enda medieobjekt. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | heltal | Antalet pausperioder som inträffade under uppspelning. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | heltal | Den totala varaktighet (i sekunder) i vilken uppspelningen pausades av en användare. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | string | En MVPD-identifierare som tillhandahålls via Adobe-autentisering. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | string | Definierar att användaren har autentiserats via Adobe. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Definierar tiden på dagen då innehållet sändes eller spelades upp. |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | boolesk | Ett booleskt värde som markerar varje uppspelning som återupptogs efter mer än 30 minuters buffert, paus eller en stillastående period. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | boolesk | Ett booleskt värde som anger att minst en bildruta har visats. Den här bildrutan behöver inte vara den första. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | string | Namnet på postetiketten. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | string | Radiokanalen eller namnet som ljudet spelas upp på. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | string | Namnet på ljudinnehållsutgivaren. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | tal | Anger hur lång tid (i sekunder) som har gått mellan användarens senast kända interaktion och det ögonblick som sessionen stängdes. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | string | Den typ av annons som läses in enligt din egen interna representation. |

{style="table-layout:auto"}

## Advertising-parametrar

I följande tabell finns information om annonsparametrar.

| Datafeed | Sökväg till XDM-fält | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | string | Annonsens namn. I rapporter är&quot;annonsnamn&quot; klassificeringen och&quot;annonsnamn (variabel)&quot; eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | heltal | Indexvärdet för annonsen inuti den överordnade annonsen. Den första annonsen har index 0 och den andra har index 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | heltal | Längden på videoannonsen, mätt i sekunder. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | string | Namnet på spelaren som används för att återge annonsen. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | string | ID för annonsbrytningen. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | string | Annonsbrytningens egna (läsbara) namn. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | string | Det företag eller varumärke vars produkt visas i annonsen. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | string | ID för annonskampanjen. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | boolesk | Ett booleskt värde som anger om annonsen har startats eller inte. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | boolesk | Ett booleskt värde som anger om åtgärden har slutförts eller inte. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | heltal | Den totala tiden, mätt i sekunder, som har ägnats åt att titta på annonsen. |

{style="table-layout:auto"}

## Kapitelparametrar

I följande tabell finns information om kapitelparametrar.

| Datafeed | Sökväg till XDM-fält | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | string | Kapitelets automatiskt genererade ID. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | boolesk | Ett booleskt värde som anger om kapitlet har startats eller inte. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | boolesk | Ett booleskt värde som anger om kapitlet har slutförts eller inte. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | heltal | Den tid, mätt i sekunder, som har ägnats åt kapitlet. |

{style="table-layout:auto"}

## Parametrar för spelartillstånd

I följande tabell finns information om parametrar för spelartillstånd.

| Datafeed | Sökväg till XDM-fält | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | boolesk | Ett booleskt värde som anger om videoläget är inställt på helskärm eller inte. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | heltal | Antalet gånger som ett videoläge ställdes in på helskärm. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | heltal | Den totala längden för när videoläget ställdes in på helskärm. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | boolesk | Ett booleskt värde som anger om undertextning är aktiverad eller inte. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | heltal | Antalet gånger som undertextning har aktiverats. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | heltal | Den totala längden för när undertextning aktiverades. |
| `videostatemute` | `mediaReporting.states[].isSet` | boolesk | Ett booleskt värde som anger om videoläget är inställt på tyst läge eller inte. |
| `videostatemutecount` | `mediaReporting.states[].count` | heltal | Antalet gånger som en video har stängts av. |
| `videostatemutetime` | `mediaReporting.states[].time` | heltal | Videons totala längd i minuter. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | boolesk | Ett booleskt värde som anger om bild-i-bild-läge är aktiverat eller inte. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | heltal | Antalet gånger som bild-i-bild-läget är aktiverat. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | heltal | Den totala längden för när bild-i-bild-läget aktiverades. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | boolesk | Ett booleskt värde som anger om fokusläget är aktiverat eller inte |
| `videostateinfocuscount` | `mediaReporting.states[].count` | heltal | Antalet gånger som bildläget har aktiverats. |
| `videostateinfocustime` | `mediaReporting.states[].time` | heltal | Den totala längden för när läget i fokus var aktiverat. |

{style="table-layout:auto"}

## Kvalitetsparametrar

I följande tabell finns information om kvalitetsparametrar.

| Datafeed | Sökväg till XDM-fält | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | tal | Genomsnittlig bithastighet (i kbit/s, heltal). Det här måttet beräknas som ett vägt genomsnitt av alla bithastighetsvärden som är relaterade till uppspelningens varaktighet som inträffade under en uppspelningssession. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | boolesk | Ett booleskt värde som anger antalet strömmar i vilka bithastighetsändringar inträffade. Det här måttet anges till true endast om minst en bithastighetsändringshändelse inträffade under en uppspelningssession. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | heltal |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | string | Antalet bithastighetsändringar. Detta värde beräknas som summan av alla bithastighetsändringshändelser som inträffade under en uppspelningssession. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | heltal | Varaktigheten, mätt i sekunder, som passerat mellan videoinläsning och videostart. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | boolesk | Ett booleskt värde som anger antalet strömmar i vilka bildrutor släpptes. Det här måttet är bara true om minst en bildruta släpptes under en uppspelningssession. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | heltal | Antalet bildrutor som utelämnas under uppspelning av huvudinnehållet. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | heltal | Antalet bufferthändelser. Detta mått beräknas som antalet olika buffertlägen som inträffade under en uppspelningssession. Detta är antalet gånger spelaren försätts i ett buffertläge från andra lägen, till exempel uppspelning eller pausning. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | heltal | Den totala tiden, mätt i sekunder, för buffring. Det här värdet beräknas som summan av alla bufferthändelsevaraktigheter som inträffade under en uppspelningssession. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | boolesk | Ett booleskt värde som anger antalet strömmar som påverkas av buffring. Det här måttet är bara true om minst en bufferthändelse inträffade under en uppspelningssession. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | boolesk | Ett booleskt värde som anger antalet strömmar där en felhändelse inträffade. Om till exempel ett trackError anropades under uppspelningssessionen och ett type=error-pulsslagsanrop genererades. Det här måttet anges till true endast om minst ett fel uppstod under uppspelningen. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | heltal | Antalet fel som uppstod. Detta värde beräknas som summan av alla felhändelser som inträffade under en uppspelningssession. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | strängmatris | Unika fel-ID:n som genereras av spelaren SDK. Du måste ange felkoder eller ID:n vid implementeringen via de angivna felprogrammeringsgränssnitten. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | strängmatris | Unika fel-ID:n från externa källor, till exempel CDN-fel. Du måste ange felkoder eller ID:n vid implementeringen via de angivna felprogrammeringsgränssnitten. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | boolesk | De unika fel-ID:n som genereras av Media SDK under uppspelningen. |

{style="table-layout:auto"}

## Föråldrade fält

Läs det här avsnittet för information om inaktuella analysmappningsfält.

### Direktmappningsfält

+++Välj för att visa en tabell med inaktuella direktmappningsfält

| Datafeed | XDM-fält | XDM-typ | Beskrivning |
| --- | --- | --- | --- |
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
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | string | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | tal | Mobiltjänster är en viktig del. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | tal | Mobiltjänster är mindre. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | string | Mobiltjänster är UUID. |
| `mobileinstalls` | `application.firstLaunches` | Objekt | Detta utlöses första gången efter installation eller ominstallation | {id (sträng), value (number)} |
| `mobileupgrades` | `application.upgrades` | Objekt | Rapporterar antalet appuppgraderingar. Utlösare vid första körningen efter uppgraderingen eller när som helst när versionsnumret ändras. | {id (sträng), value (number)} |
| `mobilelaunches` | `application.launches` | Objekt | Antalet gånger som appen har startats. | {id (sträng), value (number)} |
| `mobilecrashes` | `application.crashes` | Objekt |  | {id (sträng), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objekt |  | {id (sträng), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objekt | | {id (sträng), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objekt | | {id (sträng), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objekt | Den tid det tar att starta videokvaliteten. | {id (sträng), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objekt | | {id (sträng), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objekt | Buffertantal för videokvalitet | {id (sträng), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objekt | Bufferttid för videokvalitet | {id (sträng), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objekt | Antal ändringar av videokvalitet | {id (sträng), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objekt | Genomsnittlig bithastighet för videokvalitet | {id (sträng), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objekt | Antal fel för videokvalitet | {id (sträng), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objekt | | {id (sträng), value (number)} |

{style="table-layout:auto"}

+++

## Genererade mappningsfält

Markera fält som kommer från ADC måste omformas, vilket kräver logik utöver en direkt kopia från Adobe Analytics för att kunna genereras i XDM.

+++Välj för att visa en tabell med borttagna genererade mappningsfält

| Datafeed | XDM-fält | XDM-typ | Beskrivning |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objekt | Anpassade analysprops, konfigurerade som listprops. Den innehåller en avgränsad lista med värden. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objekt | Används av hierarkivariabler. Den innehåller en avgränsad lista med värden. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Listvariabler för anpassade analyser. Innehåller en avgränsad lista med värden. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | heltal | ID för färgdjup, som baseras på värdet för kolumnen c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | boolesk | En variabel som används i Cookie-supportdimensionen. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objekt | Standardhändelser för e-handel utlöste träffen. | {id (sträng), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Anpassade händelser som utlöses vid träffen. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | string | Förkortning av det land där träffen kom från, vilket baseras på undersökningsperioden. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | tal | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | tal | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | boolesk | En flagga som anger om Java™ är aktiverat. |
| `m_latitude` | `placeContext.geo._schema.latitude` | tal | |
| `m_longitude` | `placeContext.geo._schema.longitude` | tal | |
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

{style="table-layout:auto"}

+++

## Fält för delad mappning

Dessa fält har en enda källa, men mappas till **flera** XDM-platser.

+++Välj för att visa en tabell med inaktuella fält för delad mappning

| Datafeed | XDM-fält | XDM-typ | Beskrivning |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | heltal | Numeriskt ID som representerar bildskärmens upplösning. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | string | Mobil operativsystemversion. |

{style="table-layout:auto"}

+++

## Avancerade mappningsfält

Markera fält (så kallade&quot;postvärden&quot;) innehåller data efter att Adobe har justerat deras värden med bearbetningsregler, VISTA-regler och uppslagstabeller. De flesta postvärden har en förbearbetad motsvarighet.

Analysens källanslutning skickar förbearbetade data till en datauppsättning i Experience Platform. Du kan omvandla dessa data till dess efterbearbetade motsvarighet med hjälp av omformningar. Mer information om hur du utför dessa omformningar med hjälp av frågetjänsten finns i [Adobe-definierade funktioner](/help/query-service/sql/adobe-defined-functions.md) i användarhandboken för frågetjänsten.

Mer information om hur du utför dessa omformningar med hjälp av frågetjänsten finns i [Adobe-definierade funktioner](/help/query-service/sql/adobe-defined-functions.md) i användarhandboken för frågetjänsten.

+++Välj för att visa en tabell med inaktuella avancerade mappningsfält

| Datafeed | XDM-fält | XDM-typ | Beskrivning |
| — | — | — | — ||
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
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string |  State-variabel. |
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
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Anpassade händelser som utlöses vid träffen.| {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | boolesk | En flagga som anger om Java™ är aktiverat. |
| `post_latitude` | `placeContext.geo._schema.latitude` | tal |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | tal |   |
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
| `geo_latitude` | `placeContext.geo._schema.latitude` | tal |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | tal |  |
| `paid_search` | `search.isPaid` | boolesk | En flagga som anges om träffen matchar betalsökningsidentifiering. |
| `ref_type` | `web.webReferrer.type` | string | Ett numeriskt ID som representerar typen av referens för träffen. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | boolesk | En flagga (1=betald, 0=inte betald) som anger om besökets första träff kom från en betald sökträff. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | string | Numeriskt ID som representerar referenstypen för besökets första referent. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | string | Numeriskt ID för besökets första sökmotor. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | heltal | Tidsstämpel för första besöket på UNIX®-tid. |

+++