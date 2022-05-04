---
keywords: Experience Platform;profil;segment;segment;segmentering;användargränssnitt;gränssnitt;anpassning;segmentpanel;instrumentpanel
title: Kontrollpanel för segment
description: 'Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om segment som din organisation har skapat. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: b4cd7bc0d8c038346aacdda7c4c9def12864065c
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Kontrollpanel för segment {#segment-dashboard}

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om dina segment, som de tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med segmentkontrollpanelen i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En översikt över alla funktioner i Adobe Experience Platform Segmentation Service i användargränssnittet finns på [Användargränssnittsguide för segmenteringstjänst](../../segmentation/ui/overview.md).

## Instrumentpanelsdata för segment

På segmentkontrollpanelen visas en ögonblicksbild av de attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och segmentkontrollpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska segmentkontrollpanelen

Navigera till [!UICONTROL Segments] kontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Segments]** i den vänstra listen väljer du **[!UICONTROL Overview]** för att visa kontrollpanelen.

>[!NOTE]
>
>Om din organisation inte har använt Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanfogningsprinciper har skapats kan [!UICONTROL Segments] Kontrollpanelen visas inte. I stället [!UICONTROL Overview] På -fliken visas länkar och dokumentation som hjälper dig att komma igång med segmentering.

![](../images/segments/dashboard-overview.png)

### Ändra [!UICONTROL Segments] kontrollpanel

Du kan ändra utseendet på [!UICONTROL Segments] kontrollpanel genom att välja **[!UICONTROL Modify dashboard]**. Detta gör att du kan flytta, lägga till och ta bort widgetar från kontrollpanelen samt få tillgång till **[!UICONTROL Widget library]** för att utforska tillgängliga widgetar och skapa anpassade widgetar för din organisation.

Se [ändra kontrollpaneler](../customize/modify.md) och [Översikt över widgetbiblioteket](../customize/widget-library.md) dokumentation som lär dig mer.

## Markera ett segment

Kontrollpanelen markerar automatiskt ett segment som ska visas, men du kan ändra segmentet med hjälp av listrutemenyn eller segmentväljaren.

Om du vill välja ett annat segment markerar du listrutan bredvid segmentnamnet eller använder segmentväljaren för att öppna segmentmarkeringsdialogrutan.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgetar och mätvärden

Kontrollpanelen för segment består av widgetar, som är skrivskyddade mått som ger viktig information om det valda segmentet.

Datum och tid för den senaste uppdateringen av en widget visar när den senaste ögonblicksbilden av data togs. Datum och tid för ögonblicksbilden anges i UTC. den inte finns i den enskilda användarens eller IMS-organisationens tidszon.

![](../images/segments/widget-timestamp.png)

## Standardwidgetar

Adobe tillhandahåller flera standardwidgetar som du kan använda för att visualisera olika mätvärden för dina segment. Du kan också skapa anpassade widgetar som ska delas med din organisation med hjälp av [!UICONTROL Widget library]. Om du vill veta mer om hur du skapar anpassade widgetar börjar du med att läsa [Översikt över widgetbiblioteket](../customize/widget-library.md).

Om du vill veta mer om de tillgängliga standardwidgetarna väljer du namnet på en widget i följande lista:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Audience activation order]](#audience-activation-order)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Audience size change trend]](#audience-size-change-trend)
* [[!UICONTROL Audience size trend by identity]](#audience-size-trend-by-identity)

### [!UICONTROL Audience size] {#audience-size}

The **[!UICONTROL Audience size]** visar det totala antalet sammanfogade profiler i det markerade segmentet när ögonblicksbilden togs. Det här numret är resultatet av att du har tillämpat segmentsammanfogningsprincipen på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person i segmentet.

Mer information om fragment och sammanfogade profiler får du om du börjar med att läsa [Översikt över kundprofiler i realtid](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

The **[!UICONTROL Identity overlap]** widgeten visar ett Venndiagram, eller ett uppsättningsdiagram, som visar överlappningen mellan profiler i segmentet som innehåller flera identiteter.

När du har använt listrutemenyerna i widgeten för att markera de identiteter som du vill jämföra, visas cirklar med den relativa storleken för varje identitet. Antalet profiler som innehåller båda namnutrymmena representeras av storleken på överlappningen mellan cirklarna.

Om en kund interagerar med ert varumärke i mer än en kanal kopplas flera identiteter till den enskilda kunden, och därför är det troligt att organisationen har flera profiler som innehåller fragment från mer än en identitet.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

The **[!UICONTROL Profiles by identity]** widgeten visar uppdelningen av identiteter för alla sammanfogade profiler i det valda segmentet. Det totala antalet profiler efter identitet kan vara högre än det totala antalet profiler i segmentet eftersom en profil kan ha flera associerade identiteter. Med andra ord kan de värden som visas för varje identitet tillsammans bli större än den totala målgruppsstorleken i segmentet, eftersom om en kund interagerar med varumärket i mer än en kanal kan flera identiteter kopplas till den enskilda kunden.

Välj **[!UICONTROL Captions]** för att öppna dialogrutan med automatiska bildtexter.

![Dialogrutan Profiler efter identitetsteckningar.](../images/segments/profiles-by-identity.png)

En maskininlärningsmodell genererar automatiskt datainsikter genom att analysera den övergripande fördelningen och de viktigaste dimensionerna av data.

Läs mer om identiteter på [Dokumentation för Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Audience activation order] {#audience-activation-order}

The [!UICONTROL Audience activation order] widgeten innehåller en tabell med tre kolumner som visar [!UICONTROL destination name], [!UICONTROL platform]och aktiveringen [!UICONTROL date] av publiken. Listan ordnas från hög till låg enligt senaste och kan innehålla upp till 10 rader.

![The Audience activation order widget.](../images/segments/audience-activation-order.png)

### [!UICONTROL Audience size trend] {#audience-size-trend}

The [!UICONTROL Audience size trend] widgeten innehåller en illustration av linjediagram för det totala antalet profiler som uppfyller villkoren i **alla** segmentdefinition under en viss tidsperiod. Trenden för målgruppens storlek kan visas under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten. Publiken visas på y-axeln och tiden på x-axeln.

![Widgeten för målgruppsstorlekstrend.](../images/segments/audience-size-trend.png)

### [!UICONTROL Audience size change trend] {#audience-size-change-trend}

Den här widgeten innehåller ett linjediagram som illustrerar skillnaden i det totala antalet profiler som är kvalificerade för ett visst segment mellan de senaste ögonblicksbilderna. Det segment som valts för analys väljs i listrutan Översikt. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten. Publiken visas på y-axeln och tiden på x-axeln.

![Widgeten Ändra målgruppsstorlek.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Audience size trend by identity] {#audience-size-trend-by-identity}

Den här widgeten visar trenden för målgruppens storlek för ett visst segment baserat på identitetstypen som valts i widgetens listruta. Det segment som används för analys väljs i listrutan Översikt. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. Tidsperioden väljs i en listruta i widgeten.

![Storlekstrend för målgrupper efter identitetswidget.](../images/segments/audience-size-trend-by-identity.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta segmentkontrollpanelen och välja ett segment att visa. Du bör också förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med segment i användargränssnittet för Experience Platform finns i [Användargränssnittsguide för segmenteringstjänst](../../segmentation/ui/overview.md).
