---
title: Skicka mediahändelse
description: Skicka mediedata till Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Skicka mediahändelse

Åtgärden **[!UICONTROL Send media event]** skickar mediahändelsen till en datastream, som sedan kan användas av program och tjänster som Adobe Experience Platform eller Adobe Analytics. Den här åtgärden är användbar när du spårar direktuppspelat medieinnehåll på din egenskap.

![Experience Platform-gränssnittsbild som visar skärmen för att skicka mediahändelser.](../assets/send-media-event.png)

Vilka alternativ som är tillgängliga beror på vilken **[!UICONTROL Media event type]** du väljer. Alla mediahändelsetyper kräver **[!UICONTROL Player ID]**, som är namnet på innehållsspelaren.

Vissa händelsetyper kan konfigurera andra fält. Om en mediahändelsetyp inte finns med här är det enda tillgängliga fältet [!UICONTROL Player ID]. Följande mediahändelsetyper innehåller andra fält:

## [!UICONTROL Ad break start]

Gör att du kan konfigurera information om reklamstativ.

* **[!UICONTROL Ad break name]**: Annonsbrytningens egna namn.
* **[!UICONTROL Ad break offset (seconds)]**: Annonsens förskjutning i innehållet, i sekunder.
* **[!UICONTROL Ad break index]**: Indexvärdet för annonsen bryts inuti innehållet, med början vid 1.

## [!UICONTROL Ad start]

Gör att du kan konfigurera annonsinformation.

* **[!UICONTROL Ad name]**: Annonsens egna namn.
* **[!UICONTROL Ad ID]**: ID för annonsen. Alla alfanumeriska värden stöds.
* **[!UICONTROL Ad length (seconds)]**: Längden på videoannonsen, i sekunder.
* **[!UICONTROL Advertiser]**: Det företag eller det varumärke vars produkt visas i annonsen.
* **[!UICONTROL Campaign ID]**: ID:t för annonskampanjen.
* **[!UICONTROL Creative ID]**: Annonspersonalens ID.
* **[!UICONTROL Creative URL]**: Webbadressen till annonspersonalen.
* **[!UICONTROL Placement ID]**: Annonsens placerings-ID.
* **[!UICONTROL Site ID]**: ID:t för annonsplatsen.
* **[!UICONTROL Pod position]**: Indexvärdet för annonsen inuti den överordnade annonsbrytningen, med början vid 0.

Den här händelsetypen stöder även möjligheten att tillhandahålla anpassade metadata som en del av mediahändelsenyttolasten.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: Ett [Experience](/help/xdm/data-types/qoe-data-details-collection.md)-objekt som anger bithastighet, uteslutna bildrutor, bildrutor per sekund och tid att starta.

## [!UICONTROL Chapter start]

Gör att du kan konfigurera kapitelinformation.

* **[!UICONTROL Chapter name]**: Namnet på kapitlet eller segmentet.
* **[!UICONTROL Chapter length]**: Kapitelns längd i sekunder.
* **[!UICONTROL Chapter index]**: Placeringen av kapitlet i innehållet.
* **[!UICONTROL Chapter offset]**: Kapitlets förskjutning från innehållets början, i sekunder.

Den här händelsetypen stöder även möjligheten att tillhandahålla anpassade metadata som en del av mediahändelsenyttolasten.

## [!UICONTROL Error]

Gör att du kan konfigurera felinformation.

* **[!UICONTROL Error name]**: Felnamnet.
* **[!UICONTROL Source]**: Felets källa.

## [!UICONTROL Session start]

Gör att du kan konfigurera information om mediesessioner.

* **[!UICONTROL Handle media session automatically]**: En kryssruta som gör att Web SDK kan skicka nödvändiga pingar automatiskt. Du kan avmarkera den här kryssrutan om du vill skicka ping-filer manuellt.
* **[!UICONTROL Playhead]**: Spelhuvudet i sekunder.
* **[!UICONTROL Content type]**: Innehållstypen. Alla strängvärden stöds. Adobe har även följande förinställningar:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: Den maximala längden för innehållet som konsumeras, i sekunder. Värdet `86400` är standardvärde för direktmedia med okänd längd.
* **[!UICONTROL Content ID]**: Innehållets innehålls-ID.
* **[!UICONTROL Ad load type]**: Den typ av annons som lästs in. Följande två värden stöds:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: Det album låten tillhör.
* **[!UICONTROL Artist]**: Låtens artist.
* **[!UICONTROL Asset ID]**: Den unika identifieraren för medieresursens innehåll. Dessa ID:n härleds vanligtvis från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system.
* **[!UICONTROL Author]**: Namnet på författaren till ljudboken.
* **[!UICONTROL Authorized]**: En flagga som avgör om användaren är inloggad med Adobe-autentisering.
* **[!UICONTROL Day part]**: Tidpunkten på dagen när innehållet sändes eller spelades upp. Alla strängvärden stöds.
* **[!UICONTROL Episode]**: Avsnittsnumret.
* **[!UICONTROL Feed type]**: Typen av feed.
* **[!UICONTROL First air date]**: Det datum då innehållet först skrevs på tv. Alla strängvärden stöds, men Adobe rekommenderar att du använder formatet `YYYY-MM-DD`.
* **[!UICONTROL First digital date]**: Det datum då innehållet först skrevs på en digital kanal eller plattform. Alla strängvärden stöds, men Adobe rekommenderar att du använder formatet `YYYY-MM-DD`.
* **[!UICONTROL Content name]**: Innehållets egna namn.
* **[!UICONTROL Genre]**: Den typ eller gruppering av innehåll som definierats av innehållsproducenten. Det här fältet stöder flera värden, avgränsade med kommatecken.
* **[!UICONTROL Label]**: Namnet på postetiketten.
* **[!UICONTROL Rating]**: Den klassificering som definieras av TV Parental Guidelines.
* **[!UICONTROL MVPD]**: MVPD som tillhandahålls av Adobe-autentisering.
* **[!UICONTROL Network]**: Nätverks- eller kanalnamnet.
* **[!UICONTROL Originator]**: Innehållets skapare.
* **[!UICONTROL Publisher]**: Utgivaren av ljudinnehåll.
* **[!UICONTROL Season]**: Om programmet är en del av en serie visas serienumret.
* **[!UICONTROL Show]**: Om programmet ingår i en serie, serienamnet.
* **[!UICONTROL Show type]**: Visningstypen. Alla strängvärden stöds. Adobe har även följande förinställningar:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: Strömtypen.
* **[!UICONTROL Stream format]**: Strömmens format, till exempel HD eller SD.
* **[!UICONTROL Station]**: Radiokationens namn eller ID.

Den här händelsetypen stöder även möjligheten att tillhandahålla anpassade metadata som en del av mediahändelsenyttolasten. Den tillåter även åsidosättningar av dataströmskonfigurationer, vilket ger dig kontroll över vilka program och tjänster som tar emot dessa data. När du anger en åsidosättning av en datastream-konfiguration i både ett enskilt kommando och i inställningarna för taggtilläggskonfigurationen, prioriteras det enskilda kommandot. Mer information finns i [Åsidosättningar av dataströmskonfiguration](../configure/configuration-overrides.md).

## [!UICONTROL States update]

Gör att du kan konfigurera information om tillståndsuppdatering. Du kan starta eller avsluta följande lägen:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

Följande fält är tillgängliga:

* **[!UICONTROL States started]**: En nedrullningsbar meny där du kan ange att ett läge har startats. Om du väljer knappen **[!UICONTROL Add another state that started]** kan du starta flera lägen i samma åtgärd.
* **[!UICONTROL States ended]**: En nedrullningsbar meny där du kan ange att ett läge har avslutats. Om du väljer knappen **[!UICONTROL Add another state that ended]** kan du avsluta flera lägen i samma åtgärd.
