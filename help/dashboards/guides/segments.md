---
keywords: Experience Platform;profil;segment;segment;segmentering;användargränssnitt;gränssnitt;anpassning;segmentpanel;instrumentpanel
title: Kontrollpanel för segment
description: 'Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om segment som din organisation har skapat. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# (Beta) Kontrollpanel för segment {#segment-dashboard}

>[!IMPORTANT]
>
>Instrumentpanelsfunktionerna som beskrivs i det här dokumentet är för närvarande i betaversion och är inte tillgängliga för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om dina segment, som de tagits under en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med segmentkontrollpanelen i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En översikt över alla funktioner i Adobe Experience Platform Segmentation Service i användargränssnittet för plattformen finns i [gränssnittshandboken för segmenteringstjänsten](../../segmentation/ui/overview.md).

## Instrumentpanelsdata för segment

På segmentkontrollpanelen visas en ögonblicksbild av de attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och segmentkontrollpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska segmentkontrollpanelen

Om du vill navigera till segmentkontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Segments]** i den vänstra listen och sedan fliken **[!UICONTROL Overview]** för att visa kontrollpanelen.

![](../images/segments/dashboard-overview.png)

### Markera ett segment

Kontrollpanelen väljer automatiskt ett segment som ska visas, men du kan ändra segmentet som visas med den nedrullningsbara menyn. Om du vill välja ett annat segment markerar du listrutan bredvid segmentnamnet och markerar sedan det segment som du vill visa.

>[!NOTE]
>
>I listrutan visas alla segment som din organisation har skapat hittills. Det kan innebära att du måste rulla för att kunna se hela listan med tillgängliga segment.

![](../images/segments/change-segment.png)

### Widgetar och mätvärden

Kontrollpanelen för segment består av widgetar, som är skrivskyddade mått som ger viktig information om det valda segmentet. Datum och tid för den senaste uppdateringen av widgeten visas när den senaste ögonblicksbilden av data togs.

![](../images/segments/widget-timestamp.png)

## Tillgängliga widgetar

Experience Platform tillhandahåller flera widgetar som du kan använda för att visualisera olika mätvärden för ditt segment. Välj namnet på en widget nedan om du vill veta mer:

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

Widgeten **[!UICONTROL Segment size]** visar det totala antalet sammanslagna profiler i det valda segmentet när ögonblicksbilden togs. Det här numret är resultatet av att du har tillämpat segmentsammanfogningsprincipen på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person i segmentet.

Mer information om fragment och sammanfogade profiler får du om du börjar med att läsa [Kundprofilöversikt i realtid](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

Widgeten **[!UICONTROL Profiles added over time]** ger information om det totala antalet profiler i segmentet som tagits under den dagliga ögonblicksbilden under de senaste 30 dagarna. Den här widgeten visar hur segmentstorleken kan ha ändrats under en 30-dagarsperiod när nya profiler kvalificerar sig för eller avslutar segmentet.

Mer information om segmentutvärdering och hur profiler kvalificerar sig och avslutar segment finns i [dokumentationen för segmenteringstjänsten](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Widgeten **[!UICONTROL Profiles by namespace]** visar uppdelningen av namnutrymmen i alla sammanfogade profiler i det valda segmentet. Det totala antalet profiler per ID-namnområde ([!UICONTROL ID namespace] i widgeten) kan vara högre än det totala antalet profiler i segmentet eftersom en profil kan ha flera namnutrymmen kopplade till sig. Med andra ord kan de värden som visas för varje namnutrymme tillsammans vara större än de totala profilerna i segmentet, eftersom om en kund interagerar med varumärket i mer än en kanal kan flera namnutrymmen kopplas till den enskilda kunden.

Mer information om identitetsnamnutrymmen finns i [dokumentationen för Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta segmentkontrollpanelen och välja ett segment att visa. Du bör också förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med segment i användargränssnittet för Experience Platform finns i [Användargränssnittshandboken för segmenteringstjänster](../../segmentation/ui/overview.md).