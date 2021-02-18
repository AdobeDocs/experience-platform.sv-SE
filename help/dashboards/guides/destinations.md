---
keywords: Experience Platform;profil;kundprofil i realtid;användargränssnitt;anpassning;profilpanel;instrumentpanel
title: Kontrollpanel för destinationer
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om organisationens aktiva destinationer.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# (Beta) [!UICONTROL Destinations] kontrollpanel

>[!IMPORTANT]
>
>Instrumentpanelsfunktionerna som beskrivs i det här dokumentet är för närvarande i betaversion och är inte tillgängliga för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om din organisations aktiva mål, som den fångats in under en daglig ögonblicksbild. I den här handboken beskrivs hur du får åtkomst till och arbetar med kontrollpanelen för mål i användargränssnittet, och den innehåller mer information om mätvärdena som visas på kontrollpanelen.

En översikt över destinationer samt en katalog över alla tillgängliga destinationer i Experience Platform finns på [målöversikten](../../destinations/home.md).

## [!UICONTROL Destinations] instrumentpanelsdata  {#destinations-dashboard-data}

Kontrollpanelen [!UICONTROL Destinations] visar en ögonblicksbild av de mål som din organisation har aktiverat i Experience Profile. Data i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för destinationer uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen för destinationer

Om du vill navigera till målkontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Destinations]** i den vänstra listen och sedan fliken **[!UICONTROL Overview]** för att visa kontrollpanelen.

![](../images/destinations/dashboard-overview.png)

## Tillgängliga widgetar

Experience Platform tillhandahåller flera widgetar som du kan använda för att visualisera olika mått som relaterar till dina mål. Välj namnet på en widget nedan om du vill veta mer:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

Widgeten **[!UICONTROL Most used destinations]** visar organisationens främsta destinationer efter antalet segment som mappas vid den senaste ögonblicksbilden. Denna rankning ger insikt i vilka destinationer som används samtidigt som de som kan vara underutnyttjade också kan visas.

Om du till exempel konfigurerade ett mål i går men inte har mappat några segment till det, kan du se att målet för närvarande är underutnyttjat.

Antalet mappade segment som visas i kolumnen Antal segment är exakt som i den senaste ögonblicksbilden. Om du mappar ett nytt segment till målet uppdateras inte antalet förrän nästa ögonblicksbild tas.

Om du väljer namnet på ett mål i den lista som visas på widgeten kommer du till målinformationen som länkad från fliken **[!UICONTROL Browse]**. Du kan också välja **[!UICONTROL View All]** för att navigera till fliken **[!UICONTROL Browse]** och sedan markera namnet på ett mål för att visa informationen om det.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

Med widgeten **[!UICONTROL Recently created destinations]** kan du visa en lista över organisationens senast konfigurerade mål.

Det datum som visas motsvarar den senaste ögonblicksbilden. Om du skapar ett nytt mål kommer det alltså inte att visas i listan förrän nästa ögonblicksbild har tagits.

Om du väljer namnet på ett mål i den lista som visas på widgeten kommer du till målinformationen som länkad från fliken **[!UICONTROL Browse]**. Du kan också välja **[!UICONTROL View All]** för att navigera till fliken **[!UICONTROL Browse]** och sedan markera namnet på ett mål för att visa informationen om det.

Mer information om hur du konfigurerar särskilda typer av destinationer finns i [måldokumentationen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

Widgeten **[!UICONTROL Recently activated segments]** innehåller en lista över de segment som senast har mappats till ett mål. Den här listan innehåller en ögonblicksbild av vilka segment och mål som används aktivt i systemet och kan hjälpa till att felsöka felaktiga mappningar.

Det uppdaterade datum som visas visar den senaste gången segmentet aktiverades till målet och är exakt som den senaste ögonblicksbilden. Det innebär att om du aktiverar ett segment till målet kommer det uppdaterade datumet inte att ändras förrän nästa fixering har tagits.

Om du väljer namnet på ett segment i listan som visas på widgeten kommer du till segmentinformationen. Du kan också välja **[!UICONTROL View All]** för att navigera till fliken för segmentbläddring och sedan markera namnet på ett segment för att visa informationen om det.

Mer information om hur du arbetar med segment i Experience Platform får du om du börjar med att läsa översikten över segmenteringstjänsten](../../segmentation/home.md).[

![](../images/destinations/recently-activated-segments.png)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta kontrollpanelen för destinationer och förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med mål i Experience Platform finns i [måldokumentationen](../../destinations/home.md).