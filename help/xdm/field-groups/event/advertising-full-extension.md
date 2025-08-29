---
title: Adobe Advertising Cloud ExperienceEvent Full Extension Schema Field Group
description: Läs mer om schemafältgruppen Adobe Advertising Cloud ExperienceEvent Full Extension.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]

>[!AVAILABILITY]
>
>Fältgruppen [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md), som samlar in vanliga mått som samlas in av Adobe Advertising (kallades tidigare [!DNL Advertising Cloud]).

Det här dokumentet beskriver strukturen och användningsfallet för tilläggsfältgruppen [!DNL Advertising Cloud].

>[!NOTE]
>
>Du kan också söka efter den här fältgruppen [i Experience Platform-gränssnittet](../../ui/explore.md) eller visa hela schemat i den [publika XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Fältgruppstruktur

Fältgruppen tillhandahåller ett enskilt `_experience`-objekt till ett schema, som i sin tur innehåller ett enskilt `adcloud`-objekt.

![Fält på översta nivån för [!DNL Advertising Cloud]-fältgruppen](../../images/field-groups/advertising-full-extension/full-schema.png "Fält på översta nivån för  [!DNL Advertising Cloud] fältgruppen")

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `adDeliveryDetails` | Objekt | Information om annonsleverans. Mer information om innehållet i det här objektet finns i [underavsnittet nedan för `adDeliveryDetails` object](#adDeliveryDetails). |
| `advertisement` | Objekt | Information om digital annonsering. Mer information om innehållet i det här objektet finns i [underavsnittet nedan i annonsobjektet](#advertisement). |
| `campaign` | Objekt | Information om kampanjhierarki. Mer information om innehållet i det här objektet finns i [underavsnittet nedan för kampanjobjektet](#campaign-campaign). |
| `conversionDetails` | Objekt | Konverteringsinformation för en annons. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#conversionDetails). |
| `eventType` | Sträng | Händelsetypen för Adobe Advertising. |
| `fees` | Objekt | Avgiftsinformation för Advertising. Mer information om innehållet i det här objektet finns i [underavsnittet nedan om avgiftsobjektet](#fees). |
| `inventory` | Objekt | Lagerinformation. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#inventory). |
| `productDetails` | Objekt | Produktannonsinformation. Mer information om innehållet i det här objektet finns i [underavsnittet nedan för objektet productDetails](#productDetails). |
| `stitchId` | Sträng | ID från Adobe Advertising annonsservrar för att spåra klickkonverteringar i webbläsare som blockerar cookies från tredje part. |

## `adDeliveryDetails` {#adDeliveryDetails}

Objektet adDeliveryDetails ger information om var och hur annonsen levererades, inklusive placeringswebbplatser och platsidentifierare.

![Diagram som visar `adDeliveryDetails`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `placementWebsite` | Sträng | Webbplatsen där annonsen visades. |
| `siteLinkText` | Sträng | Den faktiska webbplatslänken som valts i annonsen. |
| `interestLocationID` | Sträng | Platsen som härleds från sökfrågan. En fråga för&quot;Hotel i Goa&quot; returnerar till exempel ID:t för Goa, oavsett användarens faktiska surfplats. |
| `physicalLocationID` | Sträng | Användarens surfplats, som representeras av ett referens-ID från annonsnätverket. Detta ID är inte ett läsbart platsnamn (till exempel en ort eller ett land) utan en kod som har tilldelats av annonsnätverket för att identifiera ett geografiskt mål. |

## `advertisement` {#advertisement}

Annonsobjektet beskriver detaljer om den digitala annonsen, till exempel dess identifierare, typ, kreativ, målgruppsanpassning och associerade nyckelord.

![Diagram som visar `advertisement`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `adId` | Sträng | Identifieraren för annonsen som är associerad med den här händelsen. Detta ID är inte relaterat till branschstandarden för ID. |
| `runtime` | Sträng | Annonsenhetens körningsmiljö, som skiljer sig från webbläsarens eller operativsystemets körningsmiljö. Möjliga värden är: `unknown` och `HTML5`. |
| `adClass` | Sträng | Annonsklassen för körningshändelsen: `display`, `video` eller `social`. |
| `adUnitType` | Sträng | Identifieraren för koden som återger annonsen i en webbläsare eller enhet. Möjliga värden är:<ul><li>`linearVideo`: Linjär video</li><li>`interactiveVideo`: Interaktiv video</li><li>`banner`: Banner,</li><li>`richMediaBanner`: Banderoll för multimedia,</li><li>`newsFeedVideo`: News feed-video,</li><li>`newsFeedDisplay`: News feed display,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: I sidvideo,</li><li>`inPageDisplay`: I sidvisning,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: Linjär TV,</li><li>`vod`: Video on Demand</li></ul> |
| `promotedAssetId` | Sträng | Identifieraren för resursen som befordras i annonsen som är associerad med den här händelsen. |
| `creativeID` | Sträng | Identifieraren för annonsen (till exempel en banner, video eller social annons) som är associerad med den här händelsen. |
| `keywordID` | Sträng | Identifieraren för nyckelordet som anges av användaren i en sökfråga som utlöste den här händelsen. |
| `keyword` | Sträng | Det listnyckelord som kunden lade bud på. |
| `isDynamicSearchAd` | Boolean | Anger om händelsen kommer från en dynamisk sökannons. |
| `audienceID` | Sträng | Identifieraren för målgruppssegmentet som annonsen riktar sig till. |
| `adGroupID` | Sträng | Identifieraren för annonsgruppen som är associerad med annonsen som utlöste den här händelsen. |
| `campaignID` | Sträng | Identifieraren för kampanjen som är associerad med annonsen som utlöste den här händelsen. |
| `networkType` | Sträng | Nätverkstypen där händelsen inträffade. Möjliga värden är: <ul><li>`search`: Annonsen visades i söknätverket.</li><li>`content`: Annonsen visades i innehållsnätverket.</li></ul> |
| `matchType` | Sträng | Nyckelordsmatchningstypen. Möjliga värden är: <ul><li>`exact`: Exakt matchning av nyckelordet</li><li>`broad`: Stor matchning av nyckelordet</li><li>`phrase`: Nyckelordets frasmatchning</li></ul> |

## `campaign` {#campaign}

Kampanjobjektet definierar annonskampanjens hierarki, inklusive konto-, annonserings-, placerings- och paketidentifierare, tillsammans med valutadetaljer.

![Diagram som visar `campaign`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/campaign.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountId` | Sträng | Kontots identifierare. |
| `dspId` | Sträng | Identifieraren för den Demand Side Platform (DSP) som kampanjen är definierad i. Vanligtvis är den här identifieraren ID:t för Adobe Advertising Cloud DSP. |
| `campaignId` | Sträng | Identifieraren för kampanjen. |
| `placementId` | Sträng | Identifieraren för placeringen. |
| `packageId` | Sträng | Identifieraren för Advertising DSP-paketet. |
| `advertiserId` | Sträng | Identifieraren för annonsören. |
| `experimentId` | Sträng | Identifieraren för experimentet. |
| `sampleGroupId` | Sträng | Identifieraren för exempelgruppen. |
| `currency` | Sträng | Kontots ISO 4217-faktureringsvalutakod. Använder mönstret för det reguljära uttrycket ^[A-Z]{3}$ (tre versaler). Exempel: USD, EUR. |

## `conversionDetails` {#conversionDetails}

Objektet conversionDetails samlar in spårningsinformation för annonskonverteringar, inklusive spårningskoder, identiteter och konverteringsegenskaper.

![Schema som visar `conversionDetails`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/conversionDetails.png "fältet för konverteringDetaljer")

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `trackingCode` | Sträng | Koden för konverteringsspårning för händelsen. En lista över möjliga format finns i [AMO ID-format](https://experienceleague.adobe.com/sv/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | Sträng | EF-ID:t eller identitetsinformation för spårning för en händelse. En lista över möjliga format finns i [EF ID-format](https://experienceleague.adobe.com/sv/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Objekt | En karta över konverteringsegenskaper, som representeras av en matris med nyckelvärdepar (till exempel `subscriptions=253`). |

## `fees` {#fees}

Avgiftsobjektet samlar in medie-, data- och andra annonskostnader, uppdelade efter Advertising DSP, konto och annonsörer.

![Diagram som visar `fees`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/fees.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `DSPMediaFees` | Nummer | Medieavgifter som debiteras av Advertising DSP. |
| `DSPDataFees` | Nummer | De datarvoden som debiteras av Advertising DSP. |
| `DSPOtherFees` | Nummer | Andra avgifter som kan debiteras av Advertising DSP. |
| `accountMediaFees` | Nummer | Medieavgifter för kontot, men inte fakturerbara av Advertising DSP. |
| `accountDataFees` | Nummer | Dataavgifter för kontot, men inte fakturerbara av Advertising DSP. |
| `accountOtherFees` | Nummer | Andra avgifter för kontot, men inte fakturerbara av Advertising DSP. |
| `advertiserMediaFees` | Nummer | De medieannonsöraravgifter som debiteras annonsören från kontot. |
| `advertiserDataFees` | Nummer | Andra avgifter som debiteras annonsören från kontot. |
| `advertiserOtherFees` | Nummer | Andra avgifter som debiteras annonsören från kontot. |
| `billableMediaNetSpend` | Nummer | De fakturerbara nettoutgifterna för mediereklam. |
| `totalMediaNetSpend` | Nummer | De totala nettoutgifterna för mediereklam. |
| `billableDataNetSpend` | Nummer | Den fakturerbara nettokostnaden för datarklam. |
| `billableOtherNetSpend` | Nummer | De fakturerbara nettoutgifterna för andra typer av annonser. |
| `totalBillableNetSpend` | Nummer | Den totala fakturerbara nettokostnaden. |
| `totalNonBillableNetSpend` | Nummer | De totala icke fakturerbara nettoutgifterna. |
| `totalNetSpend` | Nummer | Den totala nettokostnaden. |

## `inventory` {#inventory}

Inventeringsobjektet registrerar detaljer om annonslagermöjligheten, inklusive sessionsdata, partnerkoder, plats-ID, kostnadsvaluta och segmenteringsregler.

![Diagram som visar `inventory`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/inventory.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `sessionId` | Sträng | Sessions-ID som är associerat med en upplevelsehändelse, som används för att länka oberoende händelser som inträffade i samma session. |
| `feedID` | Sträng | Ett sammansatt ID för utgivaren, annonsutbytet och andra funktioner. |
| `sspPartnerCode` | Sträng | Den partner (utbyte) genom vilken Adobe Advertising Cloud tar emot lagermöjligheten. |
| `siteID` | Sträng | Identifieraren för den webbplats där annonsintrycket skickades. |
| `costCurrency` | Sträng | ISO 4217-valutakoden som används för att betala en partner för en annonsmöjlighet. Värdet måste följa mönstret för det reguljära uttrycket ^[A-Z]{3}$ (tre versaler). Exempel: USD, EUR. |
| `inventorySourceId` | Sträng | ID för Adobe Advertising Cloud-inventeringskällan som affärsmöjligheten levererades på. |
| `segment` | Objekt | Information som är kopplad till regler för användarsegmentering. Dess egenskaper är:<ul><li>`attributablePartnerId` (String): Identifieraren för segmentprovidern som äger allomentSegmentId.</li><li>`attributableSegmentId` (sträng): Segmentet som har krediterats för användarmål i placeringens målregel. Detta används för att spåra kostnader och betalande partner.</li><li>`segments` (String): Skärningspunkten mellan användarsegmenten a\) som användaren tillhör och b\) som annonsen var riktad mot. Detta är inte den fullständiga listan över segment som användaren tillhörde vid tidpunkten för auktionen.</li></ul> |
| `optimizationTag` | Sträng | Taggen för optimering. |
| `attributableDeviceGraphId` | Sträng | Identifieraren för enhetsgrafen som är kopplad till en konverteringshändelse. |

## `productDetails` {#productDetails}

Objektet `productDetails` innehåller information om produkter som finns i shoppingannonser för [!DNL Adobe Advertising Search, Social, & Commerce], inklusive produktidentifierare, land, språk, partition, titel och annonstyp.

![Diagram som visar `productDetails`-objektet och dess fält.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `productID` | Sträng | Identifieraren för den produkt som visas i annonsen som är associerad med den här händelsen. |
| `country` | Sträng | Försäljningslandet för den produkt som visas i annonsen som är associerad med evenemanget. |
| `language` | Sträng | Språket för produktinformationen, enligt vad som anges i kundens Merchant Center-datafeed. |
| `partitionID` | Sträng | Identifieraren för den produktgrupp som är associerad med annonsen i den här händelsen. |
| `title` | Sträng | Produkttiteln som visas i annonsen. |
| `adType` | Sträng | Annonstypen för produkten som används i [!DNL Google] shoppingkampanjer. Möjliga värden är:<ul><li>`pla_with_pog`: När evenemanget kom från ett köp via en shoppingannons</li><li>`pla`: När evenemanget kom från en shoppingannons.</li><li>`pla_multichannel`: När evenemanget från en shoppingannons innehöll alternativ för både &quot;online&quot; och &quot;lokal&quot; shoppingkanaler.</li><li>`pla_with_promotion`: När händelsen från en shoppingannons visade en marknadsföringskampanj.</li></ul> |

## Nästa steg

Det här dokumentet innehöll struktur och användningsfall för fältgruppen [!DNL Advertising Cloud]. Mer information om själva fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Om du använder den här fältgruppen för att samla in [!DNL Advertising]-data med Adobe Experience Platform Web SDK kan du läsa guiden [Konfigurera ett datastream](../../../datastreams/overview.md) för att lära dig hur du mappar data till XDM på serversidan.
