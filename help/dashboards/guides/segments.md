---
keywords: Experience Platform;profil;segment;segment;segmentering;användargränssnitt;gränssnitt;anpassning;segmentpanel;instrumentpanel
title: Stödlinje för instrumentpanel för segment
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om segment som din organisation har skapat.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 7f226a37996ab5e1fef432c6007d7d488f84ded6
workflow-type: tm+mt
source-wordcount: '1699'
ht-degree: 0%

---

# [!UICONTROL Segments] kontrollpanel {#segment-dashboard}

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om dina segment, som de tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med segmentkontrollpanelen i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En översikt över alla funktioner i Adobe Experience Platform Segmentation Service i användargränssnittet finns på [Användargränssnittsguide för segmenteringstjänst](../../segmentation/ui/overview.md).

## [!UICONTROL Segments] instrumentpanelsdata

På segmentkontrollpanelen visas en ögonblicksbild av de attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och segmentkontrollpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska [!UICONTROL Segments] kontrollpanel {#explore}

Navigera till [!UICONTROL Segments] kontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Segments]** i den vänstra listen väljer du **[!UICONTROL Overview]** för att visa kontrollpanelen.

>[!NOTE]
>
>Om din organisation inte har använt Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanfogningsprinciper har skapats kan [!UICONTROL Segments] Kontrollpanelen visas inte. I stället [!UICONTROL Overview] På -fliken visas länkar och dokumentation som hjälper dig att komma igång med segmentering.

![Fliken Översikt över kontrollpanelen Segment.](../images/segments/dashboard-overview.png)

### Ändra [!UICONTROL Segments] kontrollpanel {#modify}

Du kan ändra utseendet på [!UICONTROL Segments] kontrollpanel genom att välja **[!UICONTROL Modify dashboard]**. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt få tillgång till **[!UICONTROL Widget library]** för att utforska tillgängliga widgetar och skapa anpassade widgetar för din organisation.

Se [ändra kontrollpaneler](../customize/modify.md) och [Översikt över widgetbiblioteket](../customize/widget-library.md) dokumentation som lär dig mer.

### Lägg till widgetar {#add-widget}

Välj **[!UICONTROL Add widget]** för att navigera till widgetbiblioteket och se en lista över tillgängliga widgetar att lägga till på din instrumentpanel.

![Översikt över kontrollpanelen Segment med widgeten Lägg till markerad.](../images/segments/segments-overview-add-widget.png)

I widgetbiblioteket kan du bläddra genom urvalet av standardwidgetar och anpassade segmentwidgetar. Mer information om hur du lägger till widgetar finns i dokumentationen för widgetbiblioteket. [lägga till en widget](../customize/widget-library.md#add-widgets).

## Markera ett segment

Kontrollpanelen markerar automatiskt ett segment som ska visas, men du kan ändra segmentet med hjälp av listrutemenyn eller segmentväljaren.

Om du vill välja ett annat segment markerar du listrutan bredvid segmentnamnet eller använder segmentväljaren för att öppna segmentmarkeringsdialogrutan.

>[!IMPORTANT]
>
>Endast segment med ett profilantal över noll visas i listan med valbara segment.

![Översikt över kontrollpanelen Segment med den globala segmentlistrutan markerad.](../images/segments/change-segment.png)

![Dialogrutan Välj segment som visar alla tillgängliga segment.](../images/segments/select-segment-dialog.png)

## Widgetar och mätvärden

Kontrollpanelen för segment består av widgetar, som är skrivskyddade mått som ger viktig information om det valda segmentet.

Datum och tid för den senaste ögonblicksbilden visas högst upp på [!UICONTROL Overview] bredvid segmentlistrutan. Alla widgetdata är korrekta från och med det datumet och den tidpunkten. Tidsstämpeln för ögonblicksbilden anges i UTC. det ligger inte i den enskilda användarens eller organisationens tidszon.

![Fliken Segmentöversikt med en widgettidsstämpel markerad.](../images/segments/widget-timestamp.png)

## Standardwidgetar {#standard-widgets}

Adobe tillhandahåller flera standardwidgetar som du kan använda för att visualisera olika mätvärden för dina segment. Du kan också skapa anpassade widgetar som ska delas med din organisation med hjälp av [!UICONTROL Widget library]. Om du vill veta mer om hur du skapar anpassade widgetar börjar du med att läsa [Översikt över widgetbiblioteket](../customize/widget-library.md).

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Audience activation order]](#audience-activation-order)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Audience size change trend]](#audience-size-change-trend)
* [[!UICONTROL Audience size trend by identity]](#audience-size-trend-by-identity)
* [[!UICONTROL Audience overlap]](#audience-overlap)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Scheduled activations]](#scheduled-activations)

### [!UICONTROL Audience size] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Målgruppsstorlek"
>abstract="Den här widgeten visar det totala antalet sammanfogade profiler i det valda segmentet. Det här numret beror på den sammanfogningsprincip som används för dina data och är korrekt vid tidpunkten för den senaste ögonblicksbilden."

The **[!UICONTROL Audience size]** visar det totala antalet sammanfogade profiler i det markerade segmentet när ögonblicksbilden togs. Det här numret är resultatet av att du har tillämpat segmentsammanfogningsprincipen på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person i segmentet.

Mer information om fragment och sammanfogade profiler får du om du börjar med att läsa [Översikt över kundprofiler i realtid](../../profile/home.md).

![Översikt över kontrollpanelen Segment med widgeten Målgruppsstorlek markerad.](../images/segments/audience-size.png)

### [!UICONTROL Audience size trend] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Trend för målgruppsstorlek"
>abstract="Den här widgeten innehåller information om det totala antalet profiler som uppfyller villkoren i **alla** segmentdefinition, som den tagits under den dagliga ögonblicksbilden, för de senaste 30 dagarna, 90 dagarna eller 12 månaderna."

The **[!UICONTROL Audience size trend]** widgeten innehåller en illustration av linjediagram för det totala antalet profiler som uppfyller villkoren i **alla** segmentdefinition under en viss tidsperiod. Trenden för målgruppens storlek kan visas under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten. Publiken visas på y-axeln och tiden på x-axeln.

Den här widgeten innehåller även den automatiska [!UICONTROL Captions] där en maskininlärningsmodell analyserar diagram- och segmentdata och automatiskt genererar bildtexter som beskriver viktiga trender och viktiga händelser. Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![I segmentöversikten visas widgeten för målgruppsstorlekstrend.](../images/segments/audience-size-trend-captions.png)

Dialogrutan med automatiska bildtexter öppnas och innehåller information om dina data.

![Dialogrutan med automatiska bildtexter för widgeten Storlekstrend för publik.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Mer information om segmentutvärdering och hur profiler kvalificerar sig och avslutar segment finns i [Dokumentation för segmenteringstjänst](../../segmentation/home.md).

### [!UICONTROL Audience size change trend] {#audience-size-change-trend}

Den här widgeten innehåller ett linjediagram som illustrerar skillnaden i det totala antalet profiler som är kvalificerade för ett visst segment mellan de senaste ögonblicksbilderna. Det segment som valts för analys väljs i listrutan Översikt. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten. Publiken visas på y-axeln och tiden på x-axeln.

![Widgeten Ändra målgruppsstorlek.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Audience size trend by identity] {#audience-size-trend-by-identity}

Den här widgeten visar trenden för målgruppens storlek för ett visst segment baserat på identitetstypen som valts i widgetens listruta. Det segment som används för analys väljs i listrutan Översikt. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten.

![Storlekstrend för målgrupper efter identitetswidget.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Audience activation order] {#audience-activation-order}

The [!UICONTROL Audience activation order] widgeten innehåller en tabell med tre kolumner som visar [!UICONTROL destination name], [!UICONTROL platform]och aktiveringen [!UICONTROL date] av publiken. Listan ordnas från hög till låg enligt senaste och kan innehålla upp till 10 rader.

![The Audience activation order widget.](../images/segments/audience-activation-order.png)

### [!UICONTROL Audience overlap] {#audience-overlap}

Den här widgeten representerar antalet profiler från två segment som uppfyller kriterierna för båda segmentdefinitionerna. Segmenten som används för jämförelsen markeras på menyerna i widgeten. Det totala antalet profiler i den relevanta segmentdefinitionen kan du se genom att hålla markören över en cirkel eller skärningspunkten i Venndiagrammet.

Med den här widgeten kan du optimera din segmenteringsstrategi genom att visualisera likheterna i resultaten av segmentdefinitionerna.

![Widgeten för överlappning av publik.](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitetsöverlappning"
>abstract="Den här widgeten visar överlappningen av profiler i ditt segment som innehåller båda valda identiteter. Cirklarna visar den relativa storleken för varje identitet. Antalet profiler som innehåller båda namnutrymmena representeras av överlappningen mellan cirklarna."

The **[!UICONTROL Identity overlap]** widgeten visar ett Venndiagram, eller ett uppsättningsdiagram, som visar överlappningen mellan profiler i segmentet som innehåller flera identiteter.

Använd listrutemenyerna i widgeten för att välja de identiteter som du vill jämföra. Cirklarna visar den relativa storleken för varje vald identitet, där antalet profiler som innehåller båda namnutrymmena representeras av storleken på överlappningen mellan cirklarna.

Om en kund interagerar med ert varumärke i mer än en kanal kopplas flera identiteter till den enskilda kunden, och därför är det troligt att organisationen har flera profiler som innehåller fragment från mer än en identitet.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Översikt över kontrollpanelen Segment med widgeten Identity overlap markerad.](../images/segments/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profiler efter identitet"
>abstract="Den här widgeten visar hur identiteterna fördelar sig för alla sammanslagna profiler i det valda segmentet."

The **[!UICONTROL Profiles by identity]** widgeten visar uppdelningen av identiteter i alla sammanfogade profiler i det valda segmentet. Det totala antalet profiler efter identitet kan vara högre än det totala antalet profiler i segmentet eftersom en profil kan ha flera associerade identiteter. Med andra ord kan de värden som visas för varje identitet tillsammans bli större än den totala målgruppsstorleken i segmentet, eftersom om en kund interagerar med varumärket i mer än en kanal kan flera identiteter kopplas till den enskilda kunden.

Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![Dialogrutan Profiler efter identitetsteckningar.](../images/segments/profiles-by-identity.png)

En maskininlärningsmodell genererar automatiskt datainsikter genom att analysera den övergripande fördelningen och de viktigaste dimensionerna av data.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Schemalagda aktiveringar {#scheduled-activations}

The [!UICONTROL Scheduled activations] widgeten innehåller en tabellvy över de senast aktiverade målplatserna. Tabellen innehåller målplattformen, namnet på aktiveringsflödet till den här destinationen samt start- och slutdatumet för aktiveringen för det valda segmentet. Om det inte finns något slutdatum för aktiveringen visas det som [!UICONTROL Ongoing]. Det segment som ska analyseras väljs i listrutan högst upp på sidan.

Med widgeten kan du snabbt identifiera var och när målgruppen aktiveras och göra duplicerade eller onödiga aktiveringar mer transparenta. Den samlade informationen visar också var aktiveringar har utelämnats.

![Widgeten för schemalagda aktiveringar.](../images/segments/scheduled-activations.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta segmentkontrollpanelen och välja ett segment att visa. Du bör också förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med segment i användargränssnittet för Experience Platform finns i [Användargränssnittsguide för segmenteringstjänst](../../segmentation/ui/overview.md).
