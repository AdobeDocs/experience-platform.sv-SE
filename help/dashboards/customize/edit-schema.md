---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål;licensanvändning
title: Redigera schema för att skapa anpassade instrumentpanelswidgetar
description: Den här guiden innehåller stegvisa instruktioner för att välja attribut och konfigurera organisationens schema för att skapa anpassade widgetar för Adobe Experience Platform-instrumentpaneler.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 9b89effa6f90fb513fac9d0b826722ab05020036
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Redigera schema för att skapa anpassade widgetar

Om du vill skapa anpassade widgetar för Adobe Experience Platform-instrumentpaneler måste du först identifiera de kundprofilattribut i realtid som widgetarna ska baseras på.

Den här guiden innehåller stegvisa instruktioner för hur du redigerar organisationens schema genom att välja attribut för att skapa anpassade instrumentpanelswidgetar.

När attributen har valts och schemat har konfigurerats kan du fortsätta med stegen för [skapa anpassade widgetar för dina instrumentpaneler](custom-widgets.md).

>[!NOTE]
>
>Användarna måste beviljas behörigheten Hantera standardinstrumentpaneler för att kunna redigera schemat. Anvisningar om hur du beviljar åtkomstbehörigheter för kontrollpaneler finns i [behörighetsguide för instrumentpanel](../permissions.md).

## Widget-bibliotek {#widget-library}

Den här guiden kräver åtkomst till [!UICONTROL Widget library] i Experience Platform. Om du vill veta mer om widgetbiblioteket och hur du kommer åt det i användargränssnittet börjar du med att läsa [widgetbibliotek - översikt](widget-library.md).

## Redigera schema

I widgetbiblioteket **[!UICONTROL Custom]** Med -fliken kan du skapa widgetar och dela dem med andra användare i organisationen för att anpassa utseendet på dina instrumentpaneler.

Innan du kan skapa anpassade widgetar måste du välja attribut för kundprofil i realtid för att se till att data inkluderas som en del av den dagliga ögonblicksbilden.

>[!IMPORTANT]
>
>Organisationen kan välja högst 20 attribut.

Om din organisation inte har valt några profilattribut börjar du med att välja **[!UICONTROL Configure]** mitt på skärmen.

![Fliken Egen i widgetens bibliotekarbetsyta med Konfigurera markerat.](../images/customization/configure-schema.png)

När minst ett anpassat attribut har skapats väljer du **[!UICONTROL Edit schema]** om du vill visa de markerade attributen och lägga till mer.

![Fliken Egen i widgetens biblioteksyta med redigeringsschema markerat.](../images/customization/edit-schema.png)

## Välj ett attribut

Välj ett attribut i **[!UICONTROL Select union schema field]** navigera till attributet i unionsschemat (eller använd sökning) och markera kryssrutan bredvid attributet. Om du markerar kryssrutan läggs även attributet till i **[!UICONTROL Selected Attributes]** till höger i dialogrutan.

>[!NOTE]
>
>För att ett attribut ska vara synligt för markering måste det vara något av följande: Sträng, Datum, Datum-Tid, Boolean, Kort, Lång, Heltal eller Byte. Datatyperna Map och Double stöds inte och är nedtonade så att de inte kan markeras.

När du har valt de attribut du vill lägga till väljer du **[!UICONTROL Save]** för att spara dina attribut och återgå till fliken för anpassade widgetar.

>[!WARNING]
>Nyligen markerade attribut blir tillgängliga efter nästa dagliga ögonblicksbild när data uppdateras.

![Dialogrutan där du kan välja schemaattribut med attribut och Spara markerat.](../images/customization/select-attribute.png)

## Nästa steg

När du har läst den här guiden kan du navigera till widgetbiblioteket och välja attribut för kundprofil i realtid för att konfigurera ditt schema. När profilattributen är markerade kan du börja [skapa anpassade widgetar för dina instrumentpaneler](custom-widgets.md).
