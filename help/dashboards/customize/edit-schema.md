---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål;licensanvändning
title: Redigera schema för att skapa anpassade instrumentpanelswidgetar
description: 'Den här guiden innehåller stegvisa instruktioner för att välja attribut och konfigurera organisationens schema för att skapa anpassade widgetar för Adobe Experience Platform-instrumentpaneler. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 16a8764fd27e6b1ae32bc37b3abcd521aaf88887
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Redigera schema för att skapa anpassade widgetar

Om du vill skapa anpassade widgetar för Adobe Experience Platform-instrumentpaneler måste du först identifiera de kundprofilattribut i realtid som widgetarna ska baseras på.

Den här guiden innehåller stegvisa instruktioner för hur du redigerar organisationens schema genom att välja attribut för att skapa anpassade instrumentpanelswidgetar.

När attributen har valts och schemat har konfigurerats kan du fortsätta med stegen för att [skapa anpassade widgetar för dina instrumentpaneler](custom-widgets.md).

>[!NOTE]
>
>Användarna måste beviljas behörigheten Hantera standardinstrumentpaneler för att kunna redigera schemat. Anvisningar om hur du beviljar åtkomstbehörigheter för kontrollpaneler finns i [behörighetsguiden för kontrollpanelen](../permissions.md).

## Widget-bibliotek {#widget-library}

Den här guiden kräver åtkomst till [!UICONTROL Widget library] i Experience Platform. Om du vill veta mer om widgetbiblioteket och hur du kommer åt det i användargränssnittet kan du börja med att läsa översikten [widgetbiblioteket](widget-library.md).

## Redigera schema

I widgetbiblioteket kan du på fliken **[!UICONTROL Custom]** skapa widgetar och dela dem med andra användare i organisationen för att anpassa utseendet på dina instrumentpaneler.

Innan du kan skapa anpassade widgetar måste du välja attribut för kundprofil i realtid för att se till att data inkluderas som en del av den dagliga ögonblicksbilden.

>[!IMPORTANT]
>
>Organisationen kan välja högst 20 attribut.

Om din organisation inte har valt några profilattribut börjar du med att välja **[!UICONTROL Edit schema]** i det övre högra hörnet i widgetbiblioteket.

När minst ett anpassat attribut har skapats väljer du **[!UICONTROL Edit schema]** för att visa de valda attributen och lägga till fler.

![](../images/customization/edit-schema.png)

## Välj ett attribut

Om du vill välja ett attribut i dialogrutan **[!UICONTROL Select union schema field]** navigerar du till attributet i unionsschemat (eller använder sökning) och markerar kryssrutan bredvid attributet. Om du markerar kryssrutan läggs även attributet till i listan **[!UICONTROL Selected Attributes]** till höger i dialogrutan.

>[!NOTE]
>
>För att ett attribut ska vara synligt för markering måste det vara något av följande: Sträng, Datum, Datum-Tid, Boolean, Kort, Lång, Heltal eller Byte. Datatyperna Map och Double stöds inte och är nedtonade så att de inte kan markeras.

När du har valt de attribut du vill lägga till väljer du **[!UICONTROL Save]** för att spara dina attribut och återgå till fliken för anpassade widgetar.

>[!WARNING]
>Nyligen markerade attribut blir tillgängliga efter nästa dagliga ögonblicksbild när data uppdateras.

![](../images/customization/select-attribute.png)

## Nästa steg

När du har läst den här guiden kan du navigera till widgetbiblioteket och välja attribut för kundprofil i realtid för att konfigurera ditt schema. När du har valt profilattribut kan du börja [skapa anpassade widgetar för dina instrumentpaneler](custom-widgets.md).