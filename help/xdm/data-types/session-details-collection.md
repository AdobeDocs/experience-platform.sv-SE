---
title: Samlingsdatatyp för sessionsinformation
description: Läs mer om datatypen XDM (Session Details Collection Experience Data Model).
source-git-commit: fb000d45d828c01fdb08d7555512f07ab52e1f7b
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# [!UICONTROL Session Details] Samlingsdatatyp

[!UICONTROL Session Details] Samlingen är en XDM-datatyp (Experience Data Model) som håller reda på data som hör till mediespelningssessioner. Fält för mediainsamling används för att samla in data som skickas till andra Adobe-tjänster för vidare bearbetning. Det här schemat omfattar ett brett urval av egenskaper som kan användas för att ge insikter i användarbeteenden och mönster för innehållsförbrukning. Använd [!UICONTROL Session Details] Samla in datatyp för att fånga användarengagemanget genom att logga uppspelningshändelser, annonsinteraktioner, förloppsmarkörer, pauser och andra mätvärden.

+++Välj om du vill visa ett diagram över datatypen för insamling av sessionsinformation.
![Ett diagram över datatypen Session Details Collection.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | Sträng | Nej | Den typ av annons som läses in enligt varje kunds interna representation. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Sträng | Nej | Namnet på det album som musikinspelningen eller videon tillhör. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Sträng | Nej | Namnet på den albumartist eller grupp som utför musikinspelningen eller videon. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Sträng | Nej | The [!UICONTROL Asset ID] är den unika identifieraren för medieresursens innehåll, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Sträng | Nej | Namnet på mediets författare. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Sträng | Ja | The [!UICONTROL Broadcast Content Type] av strömleveransen. Tillgängliga värden per [!UICONTROL Stream Type] inkludera:<br>Ljud: &quot;låt&quot;, &quot;poddsändning&quot;, &quot;ljudbok&quot; och &quot;radio&quot;.<br>Video: VoD, Live, Linear, UGC och DVoD.<br>Kunder kan ange anpassade värden för den här parametern. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Sträng | Nej | Namnet på nätverket/kanalen. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Sträng | Ja | The [!UICONTROL Content Channel] är distributionskanalen som innehållet spelades upp från. |
| [[!UICONTROL Content Completes]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Boolean | Nej | [!UICONTROL Content Completes] visar om en medieresurs med tidsangivelser har bevakats tills den har slutförts. Den här händelsen behöver inte nödvändigtvis innebära att användaren tittade på hela videon. Visningsprogrammet kunde ha hoppat över i förväg. |
| [!UICONTROL Content Delivery Network] | `cdn` | Sträng | Nej | The [!UICONTROL Content Delivery Network] av det innehåll som spelas upp. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | string | Ja | The [!UICONTROL Content ID] är en unik identifierare av innehållet. Den kan användas för att länka tillbaka till andra branschs- eller CMS-ID:n. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Sträng | Nej | The [!UICONTROL Content Name] är det&quot;vänliga&quot; (läsbara) namnet på innehållet. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Sträng | Ja | Namnet på innehållsspelaren. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Sträng | Nej | Namnet på innehållsskaparen. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Sträng | Nej | En egenskap som definierar tiden på dagen då innehållet sändes eller spelades upp. Detta kan ha vilket värde som helst som kunderna behöver |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Sträng | Nej | Antal avsnitt. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Sträng | Nej | Typen av feed, som antingen kan representera faktiska matningsrelaterade data som EAST HD eller SD, eller matningens källa som en URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Sträng | Nej | Det datum då innehållet först skrevs på tv. Alla datumformat kan accepteras, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Sträng | Nej | Det datum då innehållet först skrevs på en digital kanal eller plattform. Alla datumformat kan användas, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Sträng | Nej | Typ eller gruppering av innehåll enligt innehållsproducentens definition. Värdena ska vara kommaavgränsade vid variabel implementering. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Sträng | Nej | Bekräftar om användaren har autentiserats via Adobe. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Heltal | Ja | The [!UICONTROL Media Content Length] innehåller klippets längd/körningsmiljö - Detta är den maximala längden (eller längden) på det innehåll som används (i sekunder). |
| [[!UICONTROL Media Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Boolean | Nej | Mediets load-händelse. Detta inträffar när användaren väljer uppspelningsknappen. Detta gäller även om det finns annonser före rullning, buffring, fel och så vidare. |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Sträng | Nej | Multichannel Video Programming Distributor (MVPD)-identifierare som tillhandahölls via autentisering via Adobe. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Sträng | Nej | Namnet på ljudinnehållsutgivaren. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Sträng | Nej | Namnet på radiostationen som ljudet spelas upp på. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Sträng | Nej | Betyg enligt definitionen i TV:s föräldrariktlinjer. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Sträng | Nej | Namnet på postetiketten. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Boolean | Nej | Markerar varje uppspelning som återupptogs efter mer än 30 minuters buffring, paus eller uppehåll. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Sträng | Nej | The [!UICONTROL Season Number] som föreställningen tillhör. Säsongsserie krävs bara om programmet ingår i en serie. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Sträng | Nej | Program-/serienamnet. Programnamnet krävs bara om programmet ingår i en serie. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Sträng | Nej | Innehållstypen. Till exempel en trailer eller ett helt avsnitt. Innehållstypen uttrycks som ett heltal mellan 0 och 3. Exempel: &quot;0&quot; = Helt avsnitt; &quot;1&quot; = Förhandsgranska/trailer; &quot;2&quot; = Klipp; &quot;3&quot; = Annat. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Sträng | Nej | Strömmens format (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Sträng | Nej | Medieströmmens typ. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Sträng | Nej | SDK-versionen som används av spelaren. Detta kan ha vilket värde som helst som passar din spelare. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
