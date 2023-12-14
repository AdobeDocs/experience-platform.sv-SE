---
title: Datatyp för sessionsinformation
description: Läs mer om datatypen XDM (Session Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# [!UICONTROL Session Details Information] datatyp

[!UICONTROL Session Details Information] är en XDM-datatyp (Standard Experience Data Model) som spårar data som är relaterade till mediespelningssessioner. Schemat omfattar ett brett urval av egenskaper som ger insikter om hur mediematerial konsumeras. Använd [!UICONTROL Session Details Information] datatyp för att fånga användarengagemanget genom att logga uppspelningshändelser, annonsinteraktioner, förloppsmarkörer, pauser och andra mätvärden. Detta ger värdefulla insikter om användarbeteenden och mönster för innehållskonsumtion.

+++Välj om du vill visa ett diagram över datatypen Sessionsinformation.
![Ett diagram över datatypen Sessionsinformation.](../images/data-types/session-details-information.png)
+++

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Media Session ID] | `ID` | string | The [!UICONTROL Media Session ID] identifierar en instans av en innehållsström som är unik för en enskild uppspelning. |
| [!UICONTROL Content ID] | `name` | string | **Obligatoriskt** The [!UICONTROL Content ID] är en unik identifierare av innehållet. Den kan användas för att länka tillbaka till andra branschs- eller CMS-ID:n. |
| [!UICONTROL Content Name] | `friendlyName` | Sträng | The [!UICONTROL Content Name] är det&quot;vänliga&quot; (läsbara) namnet på innehållet. |
| [!UICONTROL Media Content Length] | `length` | Heltal | **Obligatoriskt** The [!UICONTROL Media Content Length] innehåller klippets längd/körningsmiljö - Detta är den maximala längden (eller längden) på det innehåll som används (i sekunder). |
| [!UICONTROL Broadcast Content Type] | `contentType` | Sträng | **Obligatoriskt** The [!UICONTROL Broadcast Content Type] av strömleveransen. Tillgängliga värden per [!UICONTROL Stream Type] inkludera:<br>Ljud: &quot;låt&quot;, &quot;poddsändning&quot;, &quot;ljudbok&quot; och &quot;radio&quot;.<br>Video: VoD, Live, Linear, UGC och DVoD.<br>Kunder kan ange anpassade värden för den här parametern. |
| [!UICONTROL Content Player Name] | `playerName` | Sträng | **Obligatoriskt** Namnet på innehållsspelaren. |
| [!UICONTROL Content Channel] | `channel` | Sträng | **Obligatoriskt** The [!UICONTROL Content Channel] är distributionskanalen som innehållet spelades upp från. |
| [!UICONTROL Version] | `appVersion` | Sträng | SDK-versionen som används av spelaren. Detta kan ha vilket värde som helst som passar din spelare. |
| [!UICONTROL Series Name] | `show` | Sträng | Program-/serienamnet. Programnamnet krävs bara om programmet ingår i en serie. |
| [!UICONTROL Season Number] | `season` | Sträng | The [!UICONTROL Season Number] som föreställningen tillhör. Säsongsserie krävs bara om programmet ingår i en serie. |
| [!UICONTROL Episode Number] | `episode` | Sträng | Antal avsnitt. |
| [!UICONTROL Asset ID] | `assetID` | Sträng | The [!UICONTROL Asset ID] är den unika identifieraren för medieresursens innehåll, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system. |
| [!UICONTROL Genre] | `genre` | Sträng | Typ eller gruppering av innehåll enligt innehållsproducentens definition. Värdena ska vara kommaavgränsade vid variabel implementering. |
| [!UICONTROL First Air Date] | `firstAirDate` | Sträng | Det datum då innehållet först skrevs på tv. Alla datumformat kan accepteras, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [!UICONTROL First Digital Date] | `firstDigitalDate` | Sträng | Det datum då innehållet först skrevs på en digital kanal eller plattform. Alla datumformat kan användas, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [!UICONTROL Rating Value] | `rating` | Sträng | Betyg enligt definitionen i TV:s föräldrariktlinjer. |
| [!UICONTROL  Creator Name] | `originator` | Sträng | Namnet på innehållsskaparen. |
| [!UICONTROL Broadcast Network] | `network` | Sträng | Namnet på nätverket/kanalen. |
| [!UICONTROL Show Type] | `showType` | Sträng | Innehållstypen, till exempel trailer eller hela avsnitt. |
| [!UICONTROL Ad Load Type] | `adLoad` | Sträng | Den typ av annons som läses in enligt varje kunds interna representation. |
| [!UICONTROL MVPD Identifier] | `mvpd` | Sträng | The [!UICONTROL MVPD Identifier] som tillhandahölls via autentisering via Adobe. |
| [!UICONTROL Media Authorized] | `authorized` | Sträng | Bekräftar om användaren har autentiserats via Adobe. |
| [!UICONTROL Day Part] | `dayPart` | Sträng | En egenskap som definierar tiden på dagen då innehållet sändes eller spelades upp. Detta kan ha vilket värde som helst som kunderna behöver |
| [!UICONTROL Feed Type] | `feed` | Sträng | Typen av feed, som antingen kan representera faktiska matningsrelaterade data som EAST HD eller SD, eller matningens källa som en URL. |
| [!UICONTROL Stream Format] | `streamFormat` | Sträng | Strömmens format (HD, SD). |
| [!UICONTROL Resume] | `hasResume` | Boolean | Markerar varje uppspelning som återupptogs efter mer än 30 minuters buffring, paus eller uppehåll. |
| [!UICONTROL Stream Type] | `streamType` | Sträng | Medieströmmens typ. |
| [!UICONTROL Artist] | `artist` | Sträng | Namnet på den albumartist eller grupp som utför musikinspelningen eller videon. |
| [!UICONTROL Album] | `album` | Sträng | Namnet på det album som musikinspelningen eller videon tillhör. |
| [!UICONTROL Record Label] | `label` | Sträng | Namnet på postetiketten. |
| [!UICONTROL Author] | `author` | Sträng | Namnet på mediets författare. |
| [!UICONTROL Radio Station] | `station` | Sträng | Namnet på radiostationen som ljudet spelas upp på. |
| [!UICONTROL Publisher] | `publisher` | Sträng | Namnet på ljudinnehållsutgivaren. |
| [!UICONTROL Video Segment] | `segment` | Sträng | Intervallet som beskriver den del av innehållet som har visats i minuter. |
| [!UICONTROL Media Downloaded Flag] | `isDownloaded` | Boolean | Strömmen spelades upp lokalt på enheten efter att den hämtats. |
| [!UICONTROL Federated Data] | `isFederated` | Boolean | [!UICONTROL Federated Data] anges till true när träffen är federerad (d.v.s. tas emot av kunden som en del av en federerad datadelning, i stället för som en egen implementering). |
| [!UICONTROL Media Starts] | `isViewed` | Boolean | Mediets load-händelse. Detta inträffar när användaren väljer uppspelningsknappen. Detta gäller även om det finns annonser före rullning, buffring, fel och så vidare. |
| [!UICONTROL Content Starts] | `isPlayed` | Boolean | [!UICONTROL Content Starts] blir true när den första bildrutan med media förbrukas. Om användaren hoppar under en annons, buffrar och så vidare, blir det ingen [!UICONTROL Content Starts] -händelse. |
| [!UICONTROL Content Completes] | `isCompleted` | Boolean | [!UICONTROL Content Completes] visar om en medieresurs med tidsangivelser har bevakats tills den har slutförts. Den här händelsen behöver inte nödvändigtvis innebära att användaren tittade på hela videon. Visningsprogrammet kunde ha hoppat över i förväg. |
| [!UICONTROL Content Time Spent] | `timePlayed` | Heltal | [!UICONTROL Content Time Spent] summerar händelsens varaktighet (i sekunder) för alla händelser av typen PLAY i huvudinnehållet. |
| [!UICONTROL Media Time Spent] | `totalTimePlayed` | Heltal | Beskriver den totala tiden som en användare tillbringar med en viss mediefil i tid, vilket inkluderar den tid som tillbringats med att titta på annonser. |
| [!UICONTROL Unique Time Played] | `uniqueTimePlayed` | Heltal | Beskriver summan av de unika intervaller som en användare ser på en medieresurs med tidsangivelse, d.v.s. längden på de visningsintervall som visas flera gånger räknas bara en gång. |
| [!UICONTROL Average Minute Audience] | `averageMinuteAudience` | Nummer | Beskriver den genomsnittliga innehållstiden för ett visst medieobjekt, det vill säga den totala innehållstiden dividerad med längden på alla uppspelningssessioner. |
| [!UICONTROL Ad Count] | `adCount` | Heltal | Antalet annonser som har startats under uppspelningen. |
| [!UICONTROL Chapter Count] | `chapterCount` | Heltal | Antalet kapitel som startades under uppspelningen. |
| [!UICONTROL 10% Progress Marker] | `hasProgress10` | Boolean | Anger att spelhuvudet passerade 10 %-markören för media baserat på strömmens längd. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| [!UICONTROL 25% Progress Marker] | `hasProgress25` | Boolean | Anger att spelhuvudet passerade mediemarkeringen på 25 % baserat på strömmens längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| [!UICONTROL 50% Progress Marker] | `hasProgress50` | Boolean | Anger att spelhuvudet passerade 50 %-markören för media baserat på strömmens längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| [!UICONTROL 75% Progress Marker] | `hasProgress75` | Boolean | Anger att spelhuvudet passerade 75 %-markören för media baserat på strömmens längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| [!UICONTROL 95% Progress Marker] | `hasProgress95` | Boolean | Anger att spelhuvudet passerade 95 %-markören för media baserat på strömmens längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över. |
| [!UICONTROL Estimated Streams] | `estimatedStreams` | Nummer | Det uppskattade antalet video- eller ljudströmmar för varje enskild del av innehållet. |
| [!UICONTROL Pause Impacted Streams] | `hasPauseImpactedStreams` | Boolean | Anger om en eller flera pauser inträffade under uppspelningen av ett enda medieobjekt. |
| [!UICONTROL Pause Events] | `pauseCount` | Heltal | [!UICONTROL Pause Events] räknar antalet pausperioder som inträffade under uppspelning. |
| [!UICONTROL Total Pause Duration] | `pauseTime` | Heltal | [!UICONTROL Total Pause Duration] beskriver hur länge användaren pausade uppspelningen i sekunder. |
| [!UICONTROL Media Segment Views] | `hasSegmentView` | Boolean | [!UICONTROL Media Segment Views] anger när minst en bildruta, inte nödvändigtvis den första, har visats. |
| [!UICONTROL Media Session Server Timeout] | `secondsSinceLastCall` | Nummer | The [!UICONTROL Media Session Server Timeout] anger hur lång tid (i sekunder) som har gått mellan användarens senast kända interaktion och tidpunkten då sessionen stängdes. |
| [!UICONTROL Content Delivery Network] | `cdn` | Sträng | The [!UICONTROL Content Delivery Network] av det innehåll som spelas upp. |
| [!UICONTROL Pev3] | `pev3` | Sträng | [!UICONTROL Pev3] är den typ av medieström som används för rapportering. |
| [!UICONTROL Pccr] | `pccr` | Boolean | [!UICONTROL Pccr] anger att en omdirigering har gjorts. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
