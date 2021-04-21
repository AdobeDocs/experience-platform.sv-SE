---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål;licensanvändning
title: Använda widgetbiblioteket för att lägga till och skapa instrumentpanelswidgetar
description: 'Den här guiden innehåller stegvisa instruktioner för att lägga till standardwidgetar och skapa anpassade widgetar för att visualisera instrumentpanelsdata i Adobe Experience Platform. '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# (Beta) Widget library {#widget-library}

>[!IMPORTANT]
>
>Instrumentpanelsfunktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

I Adobe Experience Platform användargränssnitt kan du visa och interagera med organisationens data via flera kontrollpaneler. Du kan även uppdatera vissa av dessa instrumentpaneler genom att lägga till nya widgetar i instrumentpanelsvyn. Förutom standardwidgetarna från Adobe kan du skapa anpassade widgetar och dela dem i hela organisationen.

Den här handboken innehåller stegvisa instruktioner för hur du lägger till standardwidgetar och skapar anpassade widgetar för att anpassa den information som visas på kontrollpanelerna [!UICONTROL Profiles] och [!UICONTROL Segments] i plattformsgränssnittet.

Mer information om hur du ändrar plats och storlek för widgetar i kontrollpanelerna [!UICONTROL Profiles], [!UICONTROL Destinations] och [!UICONTROL Segments] finns i handboken [modify dashboards](modify.md).

>[!NOTE]
>
>Widgetarna som visas på kontrollpanelen [!UICONTROL License usage] kan inte anpassas. Om du vill veta mer om den här unika kontrollpanelen läser du dokumentationen till kontrollpanelen för licensanvändning](guides/license-usage.md).[

## Öppna widgetbiblioteket

Från en kontrollpanel (till exempel profilpanelen) kan du välja **[!UICONTROL Modify dashboard]** följt av **[!UICONTROL Widget library]** för att få åtkomst till widgetbiblioteket.

>[!NOTE]
>
>Knappen [!UICONTROL Widget library] visas bara när [!UICONTROL Modify dashboard] har valts.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

[!UICONTROL Widget library] innehåller två flikar, [!UICONTROL Standard] och [!UICONTROL Custom].

* Fliken **[!UICONTROL Standard]** innehåller widgetar som skapats av Adobe och gör att du kan uppdatera din instrumentpanel med dessa standardvärden. Mer information om hur du lägger till standardwidgetar på din instrumentpanel finns i avsnittet [standardwidgetar](#standard-widgets) i den här handboken.
* På fliken **[!UICONTROL Custom]** kan du skapa och dela widgetar inom din organisation. Fullständiga steg för att skapa egna widgetar finns i avsnittet [anpassade widgetar](#custom-widgets) i den här handboken.

![](images/customization/widget-library.png)

## Standardwidgetar {#standard-widgets}

Fliken **[!UICONTROL Standard]** innehåller widgetar som skapats av Adobe, uppdelade i kategorier. Om du väljer en kategori visas de tillgängliga widgetarna för den instrumentpanelen. Varje widget visas som ett kort med rubrik, beskrivning och en exempelvisualisering av måttet.

>[!NOTE]
>
>Det går bara att lägga till widgetar i instrumentpanelen som matchar den valda kategorin. Till exempel kan bara widgetar från kategorin [!UICONTROL Profiles] läggas till på kontrollpanelen [!UICONTROL Profiles].

![](images/customization/standard-widgets.png)

Om du vill välja en standardwidget som ska läggas till på instrumentpanelen markerar du widgeten och markerar kryssrutan för widgeten. När minst en widget är markerad belyses knappen **[!UICONTROL Add widget]**.

>[!NOTE]
>
>Räknaren i det övre högra hörnet av widgetbiblioteket visar det totala antalet valda widgetar.

Välj **[!UICONTROL Add widget]** om du vill lägga till valda widgetar på instrumentpanelen.

![](images/customization/add-widget.png)

## Anpassade widgetar {#custom-widgets}

>[!IMPORTANT]
>
>Din organisation kan skapa maximalt 20 anpassade widgetar i widgetbiblioteket.

Om du vill anpassa kontrollpanelernas utseende ytterligare i Experience Platform kan du skapa widgetar och dela dem med andra användare i organisationen. I widgetbiblioteket väljer du fliken **[!UICONTROL Custom]** för att börja skapa anpassade widgetar. På fliken [!UICONTROL Custom] visas alla widgetar som har skapats av din organisation. I det här exemplet har inga anpassade widgetar skapats ännu.

![](images/customization/custom-widgets.png)

### Välj attribut

För att kunna skapa anpassade widgetar måste man identifiera kundprofilattribut i realtid för att säkerställa att data inkluderas som en del av den dagliga ögonblicksbilden. Om din organisation inte har valt några profilattribut visas knappen [!UICONTROL Configure schema] i det övre högra hörnet i widgetbiblioteket.

När minst ett anpassat attribut har valts visas knappen [!UICONTROL Edit schema] i det övre högra hörnet i widgetbiblioteket. Välj **[!UICONTROL Edit schema]** för att öppna dialogrutan **[!UICONTROL Select union schema field]** för att visa de valda attributen och lägga till fler attribut.

>[!IMPORTANT]
>
>En organisation kan välja högst 20 attribut.

![](images/customization/edit-schema.png)

Om du vill välja ett attribut navigerar du till attributet i unionsschemat (eller använder sökning) och markerar kryssrutan bredvid attributet. Om du markerar kryssrutan läggs även attributet till i listan **[!UICONTROL Selected Attributes]** till höger i dialogrutan.

>[!NOTE]
>
>För att ett attribut ska vara synligt för markering måste det vara något av följande: Sträng, Datum, Datum-Tid, Boolean, Kort, Lång, Heltal eller Byte. Datatyperna Map och Double stöds inte och är nedtonade så att de inte kan markeras.

När du har valt de attribut du vill lägga till väljer du **[!UICONTROL Save]** för att spara dina attribut och återgå till fliken för anpassade widgetar.

Nyligen markerade attribut är tillgängliga efter den dagliga ögonblicksbilden när data uppdateras.

![](images/customization/select-attribute.png)

### Skapa en anpassad widget

Om du vill skapa en anpassad widget väljer du **[!UICONTROL Create]** från mitten av widgetbiblioteket, eller om anpassade widgetar redan har skapats, väljer du **[!UICONTROL Create widget]** i det övre högra hörnet av widgetbiblioteket.

![](images/customization/create-widget.png)

I dialogrutan **[!UICONTROL Create widget]** kan du ange en rubrik och beskrivning för den nya widgeten och välja det attribut som du vill att widgeten ska visa. Om du vill välja ett attribut markerar du alternativknappen bredvid attributet som du vill lägga till.

>[!NOTE]
>
>Endast ett attribut kan markeras per widget. Om en widget redan har skapats för ett attribut visas attributet nedtonat.

![](images/customization/create-widget-dialog.png)

En förhandsvisning av den nya widgeten visas i dialogrutan med ett vågrätt stolpdiagram med modelldata.

>[!NOTE]
>
>Det enda mätvärde som för närvarande stöds för alla attribut är profilantal och den enda visualisering som för närvarande stöds för anpassade widgetar är ett diagram med vågräta staplar.
>
>Data som visas i exempelwidgeten är endast avsedda som illustrationer. Förhandsgranskningen visar inte faktiska data från din organisation.

![](images/customization/create-widget-select-attribute.png)

Om du vill spara din nya widget och gå tillbaka till fliken [!UICONTROL Custom] väljer du **[!UICONTROL Create]**. Din nya widget är nu tillgänglig för att läggas till på en instrumentpanel genom att välja widgeten i biblioteket och välja **[!UICONTROL Add widget]**.

### Arkivera en anpassad widget

När en widget har lagts till i biblioteket kan den arkiveras med knappen **[!UICONTROL Archive]**. Du kan också redigera widgeten för att uppdatera titel- eller beskrivningsfälten.

## Nästa steg

När du har läst det här dokumentet kan du nu komma åt [!UICONTROL Widget library] och använda det för att lägga till widgetar på en instrumentpanel eller skapa anpassade widgetar för din organisation. Om du vill ändra storlek och plats för widgetar på kontrollpanelen läser du [Ändra instrumentpanelsguiden](modify.md).
