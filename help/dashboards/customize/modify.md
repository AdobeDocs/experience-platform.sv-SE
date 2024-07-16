---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål;licensanvändning
title: Ändra plattformsinstrumentpaneler i användargränssnittet
description: Den här guiden innehåller stegvisa instruktioner för hur du anpassar hur organisationens Adobe Experience Platform-data visas på kontrollpaneler.
exl-id: 75e4aea7-b521-434d-9cd5-32a00d00550d
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Ändra instrumentpaneler {#modify-dashboards}

I Adobe Experience Platform användargränssnitt kan du visa och interagera med organisationens data via flera kontrollpaneler. Standardwidgetar och standardmått som visas på kontrollpanelerna kan justeras på en enskild användarnivå för att visa önskade data, och widgetar kan skapas och delas mellan användare i samma organisation.

>[!NOTE]
>
>Alla uppdateringar som görs på kontrollpanelerna görs per organisation och per sandlåda.

Den här handboken innehåller stegvisa instruktioner för hur du anpassar hur instrumentpanelsdata visas på kontrollpanelerna [!UICONTROL Profiles], [!UICONTROL Segments] och [!UICONTROL Destinations] i plattformsgränssnittet.

## Komma igång

Från en kontrollpanel (till exempel kontrollpanelen [!UICONTROL Profiles]) kan du välja **[!UICONTROL Modify dashboard]** för att ändra storlek på och ordna om befintliga widgetar.

![Kontrollpanelen för profiler med kontrollpanelen Ändra markerad.](../images/customization/modify-dashboard.png)

## Ordna om widgetar

När du har valt att ändra kontrollpanelen kan du ändra ordningen på widgetarna genom att markera widgetens rubrik och dra och släppa widgetarna i önskad ordning. I det här exemplet flyttas widgeten **[!UICONTROL Profiles count trend]** till den översta raden och widgeten **[!UICONTROL Profile count]** visas nu på den andra raden.

![Kontrollpanelen Profiler med två omsorterade widgetar markerade.](../images/customization/move-widget.png)

## Ändra storlek på widgetar

Du kan också ändra storlek på en widget genom att markera vinkelsymbolen i det nedre högra hörnet av widgeten (`⌟`) och dra widgeten till önskad storlek. I det här exemplet ändras storleken på widgeten **[!UICONTROL Profiles by identity]** så att den fyller hela den översta raden och de andra widgetarna flyttas automatiskt till den andra raden. Observera hur den vågräta axeln justeras för att ge mer detaljerade steg när widgeten blir större.

>[!NOTE]
>
>När widgetarna anpassas i storlek flyttas de omgivande widgetarna dynamiskt. Detta kan medföra att vissa widgetar flyttas till ytterligare rader, vilket kräver att du rullar för att se alla widgetar.

![Kontrollpanelen Profiler med en widget med ändrad storlek markerad.](../images/customization/resize-widget.png)

## Spara uppdateringar av instrumentpanelen

När du har flyttat och ändrat storlek på widgetar väljer du **[!UICONTROL Save & exit]** för att spara ändringarna och återgå till huvudinstrumentpanelsvyn. Om du inte vill behålla ändringarna väljer du **[!UICONTROL Cancel]** för att återställa instrumentpanelen och återgå till huvudinstrumentpanelsvyn.

![Kontrollpanelen för profiler med både Avbryt och Spara och Avsluta markerat.](../images/customization/save-changes.png)

## Widget-bibliotek

Förutom att ändra storlek på och ordna om widgetar kan du välja **[!UICONTROL Modify dashboard]** i [!UICONTROL Profiles]-, [!UICONTROL Segments]- och [!UICONTROL Destinations]-kontrollpanelerna för att komma åt **[!UICONTROL Widget library]**, där du kan hitta fler widgetar att visa eller skapa anpassade widgetar för din organisation.

Stegvisa instruktioner om hur du kommer åt och arbetar med [!UICONTROL Widget library] finns i [widgetens bibliotekshandbok](widget-library.md).

![Widgetbibliotekets arbetsyta med Standard och Egen markerad.](../images/customization/widget-library.png)

## Nästa steg

När du har läst det här dokumentet har du lärt dig hur du använder funktionen för att ändra ordning på och ändra storlek på widgetar för att anpassa instrumentpanelsvyn. Om du vill lära dig hur du skapar och lägger till widgetar på dina instrumentpaneler kan du läsa [widgetens bibliotekshandbok](widget-library.md).
