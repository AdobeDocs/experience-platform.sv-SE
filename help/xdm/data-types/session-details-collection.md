---
title: Samlingsdatatyp för sessionsinformation
description: Läs mer om datatypen XDM (Session Details Collection Experience Data Model).
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# [!UICONTROL Session Details] Samlingsdatatyp

[!UICONTROL Session Details]-samlingen är en XDM-datatyp (Standard Experience Data Model) som spårar data som relaterar till mediespelningssessioner. Fält för mediainsamling används för att samla in data som skickas till andra Adobe-tjänster för vidare bearbetning. Det här schemat omfattar ett brett urval av egenskaper som kan användas för att ge insikter i användarbeteenden och mönster för innehållsförbrukning. Använd datatypen [!UICONTROL Session Details] Collection för att fånga upp användarinteraktion genom att logga uppspelningshändelser, annonsinteraktioner, förloppsmarkörer, pauser och andra mätvärden.

+++Välj om du vill visa ett diagram över datatypen för insamling av sessionsinformation.
![Ett diagram över datatypen för sessionsinformationsinsamlingen.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | Sträng | Nej | Den typ av annons som läses in enligt varje kunds interna representation. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#album) | `album` | Sträng | Nej | Namnet på det album som musikinspelningen eller videon tillhör. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#artist) | `artist` | Sträng | Nej | Namnet på den albumartist eller grupp som utför musikinspelningen eller videon. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#asset-id) | `assetID` | Sträng | Nej | [!UICONTROL Asset ID] är den unika identifieraren för innehållet i medieresursen, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#author) | `author` | Sträng | Nej | Namnet på mediets författare. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-type) | `contentType` | Sträng | Ja | [!UICONTROL Broadcast Content Type] för strömleveransen. Tillgängliga värden per [!UICONTROL Stream Type] är:<br>Ljud: &quot;låt&quot;, &quot;poddsändning&quot;, &quot;ljudbok&quot; och &quot;radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linjär&quot;, &quot;UGC&quot; och &quot;DVoD&quot;.<br>Kunder kan ange anpassade värden för den här parametern. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#network) | `network` | Sträng | Nej | Namnet på nätverket/kanalen. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-channel) | `channel` | Sträng | Ja | [!UICONTROL Content Channel] är distributionskanalen som innehållet spelades upp från. |
| [!UICONTROL Content Delivery Network] | `cdn` | Sträng | Nej | [!UICONTROL Content Delivery Network] av det uppspelade innehållet. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-id) | `name` | string | Ja | [!UICONTROL Content ID] är en unik identifierare av innehållet. Den kan användas för att länka tillbaka till andra branschid eller CMS ID. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-name-(variable)) | `friendlyName` | Sträng | Nej | [!UICONTROL Content Name] är ett användarvänligt (läsbart) namn på innehållet. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-player-name) | `playerName` | Sträng | Ja | Namnet på innehållsspelaren. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#originator) | `originator` | Sträng | Nej | Namnet på innehållsskaparen. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#day-part) | `dayPart` | Sträng | Nej | En egenskap som definierar tiden på dagen då innehållet sändes eller spelades upp. Detta kan ha vilket värde som helst som kunderna behöver |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#episode) | `episode` | Sträng | Nej | Antal avsnitt. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#media-feed-type) | `feed` | Sträng | Nej | Typen av feed, som antingen kan representera faktiska matningsrelaterade data som EAST HD eller SD, eller matningens källa som en URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#first-air-date) | `firstAirDate` | Sträng | Nej | Det datum då innehållet först skrevs på tv. Alla datumformat kan accepteras, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#first-digital-date) | `firstDigitalDate` | Sträng | Nej | Det datum då innehållet först skrevs på en digital kanal eller plattform. Alla datumformat kan användas, men Adobe rekommenderar: ÅÅÅ-MM-DD. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#genre) | `genre` | Sträng | Nej | Typ eller gruppering av innehåll enligt innehållsproducentens definition. Värdena ska vara kommaavgränsade vid variabel implementering. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#authorized) | `authorized` | Sträng | Nej | Bekräftar om användaren har autentiserats via Adobe. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-length-(variable)) | `length` | Heltal | Ja | [!UICONTROL Media Content Length] innehåller klippets längd/körtid - Detta är den maximala längden (eller längden) för innehållet som används (i sekunder). |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#mvpd) | `mvpd` | Sträng | Nej | Multichannel Video Programming Distributor (MVPD)-identifierare som tillhandahölls via autentisering via Adobe. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#publisher) | `publisher` | Sträng | Nej | Namnet på ljudinnehållsutgivaren. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#station) | `station` | Sträng | Nej | Namnet på radiostationen som ljudet spelas upp på. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-rating) | `rating` | Sträng | Nej | Betyg enligt definitionen i TV:s föräldrariktlinjer. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#label) | `label` | Sträng | Nej | Namnet på postetiketten. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#content-resumes) | `hasResume` | Boolean | Nej | Markerar varje uppspelning som återupptogs efter mer än 30 minuters buffring, paus eller uppehåll. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#season) | `season` | Sträng | Nej | The [!UICONTROL Season Number] that the show tillhör. Säsongsserie krävs bara om programmet ingår i en serie. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#show) | `show` | Sträng | Nej | Program-/serienamnet. Programnamnet krävs bara om programmet ingår i en serie. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#show-type) | `showType` | Sträng | Nej | Innehållstypen. Till exempel en trailer eller ett helt avsnitt. Innehållstypen uttrycks som ett heltal mellan 0 och 3. Exempel: &quot;0&quot; = Helt avsnitt; &quot;1&quot; = Förhandsgranska/trailer; &quot;2&quot; = Klipp; &quot;3&quot; = Annat. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#stream-format) | `streamFormat` | Sträng | Nej | Strömmens format (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#stream-type) | `streamType` | Sträng | Nej | Medieströmmens typ. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=sv-SE#sdk-version) | `appVersion` | Sträng | Nej | SDK-versionen som används av spelaren. Detta kan ha vilket värde som helst som passar din spelare. |

{style="table-layout:auto"}
