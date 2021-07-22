---
keywords: Experience Platform;användargränssnitt;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål;licensanvändning;widgets;mått;
title: Skapa anpassade widgetar för instrumentpaneler
description: 'Den här guiden innehåller stegvisa instruktioner för hur du skapar anpassade widgetar som kan användas i Adobe Experience Platform-kontrollpaneler. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# Skapa anpassade widgetar för instrumentpaneler

I Adobe Experience Platform kan du visa och interagera med organisationens data via flera kontrollpaneler. Du kan även uppdatera vissa instrumentpaneler genom att lägga till nya widgetar i instrumentpanelsvyn. Förutom standardwidgetarna från Adobe kan du även skapa anpassade widgetar och dela dem i hela organisationen.

Den här guiden innehåller stegvisa instruktioner för att skapa och lägga till anpassade widgetar i kontrollpanelerna [!UICONTROL Profiles], [!UICONTROL Segments] och [!UICONTROL Destinations] i plattformsgränssnittet.

Mer information om standardwidgetar finns i guiden för [hur du lägger till standardwidgetar till dina instrumentpaneler](standard-widgets.md).

>[!NOTE]
>
>Widgetarna som visas på kontrollpanelen [!UICONTROL License usage] kan inte anpassas. Om du vill veta mer om den här unika kontrollpanelen läser du dokumentationen till kontrollpanelen för licensanvändning](../guides/license-usage.md).[

## Widget-bibliotek {#widget-library}

Den här guiden kräver åtkomst till [!UICONTROL Widget library] i Experience Platform. Om du vill veta mer om widgetbiblioteket och hur du kommer åt det i användargränssnittet kan du börja med att läsa översikten [widgetbiblioteket](widget-library.md).

## Komma igång med anpassade widgetar

I widgetbiblioteket kan du på fliken **[!UICONTROL Custom]** skapa widgetar och dela dem med andra användare i organisationen för att anpassa utseendet på dina instrumentpaneler.

>[!IMPORTANT]
>
>Din organisation kan skapa maximalt 20 anpassade widgetar i widgetbiblioteket.

Välj fliken **[!UICONTROL Custom]** för att börja skapa anpassade widgetar eller för att visa anpassade widgetar som din organisation redan har skapat.

![](../images/customization/custom-widgets.png)

## Skapa en anpassad widget

Om du vill skapa en anpassad widget väljer du **[!UICONTROL Create]** från mitten av widgetbiblioteket, eller om anpassade widgetar redan har skapats, väljer du **[!UICONTROL Create widget]** i det övre högra hörnet av widgetbiblioteket.

![](../images/customization/create-widget.png)

I dialogrutan **[!UICONTROL Create widget]** kan du ange en titel och en beskrivning för den nya widgeten och välja det attribut som du vill att widgeten ska visa.

>[!NOTE]
>
>Listan med tillgängliga attribut beror på vilket schema som har konfigurerats för din organisation. Om du vill veta mer om attributval och schemakonfiguration läser du guiden [redigera schemat för att skapa anpassade widgetar](edit-schema.md).

Om du vill välja ett attribut markerar du alternativknappen bredvid attributet som du vill lägga till.

>[!NOTE]
>
>Endast ett attribut kan markeras per widget och endast en widget kan skapas per attribut. Om en widget redan har skapats för ett attribut visas attributet nedtonat.

![](../images/customization/create-widget-dialog.png)

## Förhandsgranska anpassad widget

En förhandsvisning av den nya widgeten visas i dialogrutan med ett vågrätt stolpdiagram med modelldata.

>[!NOTE]
>
>Det enda mätvärde som för närvarande stöds för alla attribut är profilantal och den enda visualisering som för närvarande stöds för anpassade widgetar är ett diagram med vågräta staplar.
>
>Data som visas i exempelwidgeten är endast avsedda som illustrationer. Förhandsgranskningen visar inte faktiska data från din organisation.

![](../images/customization/create-widget-select-attribute.png)

Om du vill spara din nya widget och gå tillbaka till fliken [!UICONTROL Custom] väljer du **[!UICONTROL Create]**. Din nya widget är nu tillgänglig för att läggas till på en instrumentpanel genom att välja widgeten i biblioteket och välja **[!UICONTROL Add widget]**.

## Arkivera en anpassad widget

När en widget har lagts till i biblioteket kan den arkiveras med knappen **[!UICONTROL Archive]**. Du kan också redigera widgeten för att uppdatera titel- eller beskrivningsfälten.

## Nästa steg

När du har läst det här dokumentet kan du komma åt widgetbiblioteket och använda det för att skapa och lägga till anpassade widgetar för organisationen. Om du vill ändra storlek och plats för widgetar som visas på kontrollpanelen läser du [Ändra instrumentpanelsguiden](modify.md).
