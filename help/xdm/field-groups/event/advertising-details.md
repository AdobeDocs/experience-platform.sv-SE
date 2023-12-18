---
title: Fältgrupp för reklaminformationsschema
description: Läs mer om schemafältgruppen Advertising Details.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# [!UICONTROL Advertising Details] schemafältgrupp

[!UICONTROL Advertising Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `advertising` objekt mot ett schema, som samlar in information om annonsexponeringar, klickningar och attribuering.

![Fältgruppstruktur](../../images/field-groups/advertising-details/structure.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `adAssetReference` | Objekt | Hämtar resursinformation om annonsen. Se [underavsnitt nedan](#adAssetReference) om du vill ha mer information om objektets struktur. |
| `adAssetViewDetails` | Objekt | Hämtar visningsinformation för annonsuppspelningen. Se [underavsnitt nedan](#adAssetViewDetails) om du vill ha mer information om objektets struktur. |
| `adViewability` | Objekt | Hämtar det antal visningar som slutanvändarna ser, till exempel spelarvolym, biblioteksversion, fönsterstatus och visningsrutans dimensioner. Se [underavsnitt nedan](#adViewability) om du vill ha mer information om objektets struktur. |
| `clicks` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antal klickåtgärder i annonsen. |
| `completes` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antal gånger en medieresurs med tidsangivelse bevakades tills den slutförts. Det behöver inte innebära att slutanvändaren tittade på hela videon eftersom han/hon kanske hoppade över. |
| `conversions` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet gånger en fördefinierad åtgärd (eller åtgärder) utlöste en händelse för utvärdering av prestanda. |
| `federated` | [[!UICONTROL Measure]](../../data-types/measure.md) | Anger om en upplevelsehändelse har skapats via datafederation, t.ex. datadelning mellan kunder. |
| `firstQuartiles` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet gånger en digital videoannons har spelats upp under 25 % av dess varaktighet med normal hastighet. |
| `impressions` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet annonsvisningar som skickas till slutanvändaren och som kan visas. |
| `midpoints` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet gånger en digital videoannons har spelats upp under 50 % av dess varaktighet med normal hastighet. |
| `starts` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet gånger som en digital videoannons har börjat spelas upp. |
| `thirdQuartiles` | [[!UICONTROL Measure]](../../data-types/measure.md) | Antalet gånger en digital videoannons som har spelats upp till 75 % av sin längd med normal hastighet. |
| `timePlayed` | [[!UICONTROL Measure]](../../data-types/measure.md) | Den tid som en slutanvändare tillbringar med en viss medieresurs med tidsangivelser. |
| `downloadedPlayback` | Boolean | När inställt på `true`, anger att träffen genereras på grund av att en hämtad annonssession spelas upp. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

The `adAssetReference` -objektet hämtar resursinformation om annonsen.

![adAssetReference-struktur](../../images/field-groups/advertising-details/adAssetReference.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_dc.title` | Sträng | Annonsresursens användarvänliga och läsbara namn. |
| `_xmpDM.duration` | Heltal | Resursens längd eller varaktighet i sekunder. |
| `_id` | Sträng | En unik identifierare för annonsresursen, som följer efter [Ad-ID-standard](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Sträng | Det företag eller varumärke vars produkt visas i annonsen. |
| `campaign` | Sträng | ID för annonskampanjen. |
| `creativeID` | Sträng | Annonspersonalens ID. |
| `creativeURL` | Sträng | Webbadressen till annonsskaparen. |
| `placementID` | Sträng | Annonsens placerings-ID. |
| `siteID` | Sträng | ID för annonsplatsen. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

The `adAssetViewDetails` -objektet hämtar visningsinformation för annonsuppspelningen.

![adAssetViewDetails, struktur](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Ad break]](../../data-types/ad-break.md) | Beskriver hur en tidsbestämd annons infogas i tidsinställda medier. |
| `index` | Heltal | Indexvärdet för annonsen inuti den överordnade annonsbrytningen. Den första annonsen har till exempel index `0` och den andra annonsen har index `1`. |
| `playerName` | Sträng | Namnet på spelaren som ansvarar för att återge annonsen. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

The `adViewability` -objektet hämtar det antal visningar som slutanvändarna ser, t.ex. spelarvolym, biblioteksversion, fönsterstatus och visningsrutans dimensioner.

![adViewability-struktur](../../images/field-groups/advertising-details/adViewability.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Implementation details]](../../data-types/implementation-details.md) | Namnet på och versionen av biblioteket som är instrumenterat för att mäta visningsvärden. |
| `measuredAdNotVisible` | [[!UICONTROL Measure]](../../data-types/measure.md) | Anger att annonsen inte är synlig enligt ett visningsbibliotek vid visningstillfället. |
| `measuredMuted` | [[!UICONTROL Measure]](../../data-types/measure.md) | Anger att annonsen är avstängd enligt mätning av ett visningsbibliotek vid visningstillfället. |
| `unmeasurableIframe` | [[!UICONTROL Measure]](../../data-types/measure.md) | Anger att annonsen visas i ett inaktivt fönster enligt ett visningsbibliotek vid visningstillfället. |
| `unmeasurableOther` | [[!UICONTROL Measure]](../../data-types/measure.md) | Anger att visningsbiblioteket inte kan utföra mått korrekt på grund av att annonsen visas inuti en iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Measure]](../../data-types/measure.md) | Imponering(ar) av en annons till en slutanvändare med instrumenterat visningsbibliotek. |
| `viewabilityCompletes` | [[!UICONTROL Measure]](../../data-types/measure.md) | Slutförande(ar) av en annons till en slutanvändare som bedöms kunna visas när den är klar av ett visningsbibliotek. |
| `viewableFirstQuartiles` | [[!UICONTROL Measure]](../../data-types/measure.md) | Den första kvartilen eller de första kvartilerna i en annons till en slutanvändare som bedöms kunna visas vid första kvartilen av uppspelning i ett visningsbibliotek. |
| `viewableImpressions` | [[!UICONTROL Measure]](../../data-types/measure.md) | Imponeringar på en annons till en slutanvändare som bedöms kunna se den efter två sekunders uppspelning av ett visningsbibliotek. |
| `viewableMidpoints` | [[!UICONTROL Measure]](../../data-types/measure.md) | Mittpunkt(er) för en annons till en slutanvändare som bedöms kunna visas mitt i uppspelningen av ett visningsbibliotek. |
| `viewableThirdQuartiles` | [[!UICONTROL Measure]](../../data-types/measure.md) | Tredje kvartilen av en annons till en slutanvändare som bedöms kunna visas i tredje kvartilen av ett visningsbibliotek. |
| `activeWindow` | Boolean | Anger om annonsen visades i det aktiva fönstret på användarens enhet. |
| `adHeight` | Heltal | Antalet lodräta pixlar i spelaren, mätt vid körning. Detta kan vara större än annonsens storlek om spelaren har extra kontroller eller miniatyrbilder. |
| `adUnitDepth` | Heltal | Utgivare kan bädda in annonsenheter inuti behållare (iFrames) för att begränsa annonsens åtkomst enbart till sidans kod. Det här värdet beskriver hur många behållare annonsenheten visas i. |
| `adWidth` | Heltal | Antalet vågräta pixlar i spelaren, mätt vid körning. Detta kan vara större än annonsens storlek om spelaren har extra kontroller eller miniatyrbilder. |
| `measurementEligible` | Boolean | Huruvida annonsen var visningsbar eller inte. En annons är giltig om enheten har ett kreativt format och taggtyp som stöds. |
| `percentViewable` | Heltal | Procentandelen pixlar i annonsen som kan visas vid mättiden. |
| `playerVolume` | Heltal | Spelarens volym i procent mätt vid körning, där `0` är avstängd och `100` är högsta volym. |
| `viewable` | Boolean | Anger om annonsen kunde visas under körning. Visningsannonser kan visas när minst 50 % av annonsen är synlig i minst en sekund. Videoannonser kan visas när minst 50 % av annonsen är synlig medan videon spelas upp i minst två sekunder i följd. |
| `viewportHeight` | Heltal | Fönstrets lodräta storlek (i pixlar) som upplevelsen visades i vid körning. För en webbvyhändelse anger det här värdet höjden på webbläsarens visningsruta. |
| `viewportWidth` | Heltal | Fönstrets vågräta storlek (i pixlar) som upplevelsen visades i vid körning. För en webbvyhändelse anger det här värdet bredden på webbläsarens visningsruta. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
