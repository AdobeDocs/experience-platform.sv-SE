---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål
title: Anpassning av instrumentpanel - översikt
description: Läs mer om hur du kan anpassa de data som visas på dina Adobe Experience Platform-kontrollpaneler.
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 27252d547afd30acc7b334d5054f1350dc0031b7
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Översikt över anpassning av instrumentpanel

De profiler, segment och målpaneler som finns i Adobe Experience Platform kan anpassas på flera olika sätt. Den här guiden ger en översikt över tillgängliga anpassningar, med länkar till steg-för-steg-instruktioner som guidar dig igenom hur du anpassar vilka widgetar som visas på dina instrumentpaneler samt deras storlek, form och plats.

>[!NOTE]
>
>Widgetarna visas i [!UICONTROL License usage] Kontrollpanelen kan inte anpassas. Om du vill veta mer om den här unika kontrollpanelen kan du läsa [dokumentation om kontrollpanelen för licensanvändning](../guides/license-usage.md).

## Ändra instrumentpanel

Markera **[!UICONTROL Modify dashboard]** på kontrollpanelerna för profiler, segment och mål kan du justera storlek, ordning och plats för de widgetar som är synliga på din kontrollpanel. Mer information om hur du ändrar utseendet på widgetar i dina instrumentpaneler finns i [ändra kontrollpaneler](modify.md).

## Widgetbiblioteket

Widgetbiblioteket i Experience Platform är där du kan visa alla [standard](#standard-widgets) och [anpassad](#custom-widgets) widgetar som är tillgängliga för din organisation. På dina kontrollpaneler (till exempel profilkontrollpanelen) kan du välja **[!UICONTROL Modify dashboard]** för att visa **[!UICONTROL Widget library]** -knappen.

![Kontrollpanelen Profiler med kontrollpanelen Ändra markerad.](../images/customization/modify-dashboard.png)

Välj **[!UICONTROL Widget library]** för att öppna widgetbiblioteket och visa alla tillgängliga standardmått eller börja skapa anpassade widgetar.

![Kontrollpanelen Profiler med widgetbiblioteket markerat.](../images/customization/widget-library-button.png)

### Standardwidgetar {#standard-widgets}

Standardwidgetar refererar till de widgetar som Adobe tillhandahåller för användning i dina instrumentpaneler. Dessa widgetar är skrivskyddade och kan inte redigeras av din organisation.

I widgetbiblioteket **[!UICONTROL Standard]** -fliken innehåller alla tillgängliga standardwidgetar från Adobe. Du kan uppdatera dina instrumentpaneler med hjälp av dessa standardvärden. Om du vill veta mer om hur du lägger till standardwidgetar på din instrumentpanel kan du läsa guiden för [använda standardwidgetar i kontrollpaneler](standard-widgets.md).

### Anpassade widgetar {#custom-widgets}

Anpassade widgetar avser widgetar som har skapats och delats av medlemmar i organisationen. Dessa widgetar skapas med **[!UICONTROL Custom]** -fliken i widgetbiblioteket och kräva att organisationen anger tillgängliga värden med hjälp av en [schema](#edit-schema)

Fullständiga steg för att skapa egna widgetar finns i [anpassade widgetar för kontrollpaneler](custom-widgets.md).

![Widgetbibliotekets arbetsyta med Standard och Egen markerat.](../images/customization/widget-library.png)

#### Redigera schema {#edit-schema}

För att skapa en [anpassad widget](#custom-widgets) för dina instrumentpaneler måste du först identifiera det attribut för kundprofil i realtid som widgeten ska baseras på.

Stegvisa instruktioner för hur du redigerar organisationens schema för att skapa anpassade widgetar för kontrollpaneler finns i guiden. [redigera ditt instrumentpanelsschema](edit-schema.md).

## Nästa steg

När du har läst det här dokumentet är du redo att börja anpassa dina instrumentpaneler i Experience Platform genom att ändra storlek, form och ordning på befintliga widgetar, lägga till standardwidgetar från Adobe eller skapa och dela anpassade widgetar med organisationen.
