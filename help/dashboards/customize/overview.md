---
keywords: Experience Platform;användargränssnitt;gränssnitt;instrumentpaneler;instrumentpanel;profiler;segment;mål
title: Anpassning av instrumentpanel - översikt
description: Läs mer om hur du kan anpassa de data som visas på dina Adobe Experience Platform-kontrollpaneler.
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Översikt över anpassning av instrumentpanel

De profiler, segment och målpaneler som finns i Adobe Experience Platform kan anpassas på flera olika sätt. Den här guiden ger en översikt över tillgängliga anpassningar, med länkar till steg-för-steg-instruktioner som guidar dig igenom hur du anpassar vilka widgetar som visas på dina instrumentpaneler samt deras storlek, form och plats.

>[!NOTE]
>
>Widgetarna som visas på kontrollpanelen [!UICONTROL License usage] kan inte anpassas. Om du vill veta mer om den här unika kontrollpanelen läser du dokumentationen till kontrollpanelen för licensanvändning](../guides/license-usage.md).[

## Ändra instrumentpanel

Om du väljer **[!UICONTROL Modify dashboard]** bland profilerna, segmenten eller målkontrollpanelerna kan du justera storlek, ordning och plats för de widgetar som är synliga på din instrumentpanel. Mer information om hur du ändrar utseendet på widgetar i dina instrumentpaneler finns i [handboken om att ändra instrumentpaneler](modify.md).

## Widgetbiblioteket

I widgetbiblioteket i Experience Platform kan du visa alla [standardwidgetar](#standard-widgets) och [anpassade](#custom-widgets) widgetar som är tillgängliga för din organisation. Från dina kontrollpaneler (till exempel profilkontrollpanelen) kan du välja **[!UICONTROL Modify dashboard]** för att visa knappen **[!UICONTROL Widget library]**.

![](../images/customization/modify-dashboard.png)

Välj **[!UICONTROL Widget library]** för att öppna widgetbiblioteket och visa alla tillgängliga standardmått eller börja skapa anpassade widgetar.

![](../images/customization/widget-library-button.png)

### Standardwidgetar {#standard-widgets}

Standardwidgetar refererar till de widgetar som Adobe tillhandahåller för användning i dina instrumentpaneler. Dessa widgetar är skrivskyddade och kan inte redigeras av din organisation.

I widgetbiblioteket innehåller fliken **[!UICONTROL Standard]** alla tillgängliga standardwidgetar från Adobe. Du kan uppdatera dina instrumentpaneler med hjälp av dessa standardvärden. Mer information om hur du lägger till standardwidgetar på din instrumentpanel finns i guiden för [att använda standardwidgetar i instrumentpaneler](standard-widgets.md).

### Anpassade widgetar {#custom-widgets}

Anpassade widgetar avser widgetar som har skapats och delats av medlemmar i organisationen. Dessa widgetar skapas via fliken **[!UICONTROL Custom]** i widgetbiblioteket och kräver att din organisation anger tillgängliga mått med hjälp av ett [schema](#edit-schema)

Fullständiga steg för att skapa egna widgetar finns i guiden [anpassade widgetar för instrumentpaneler](custom-widgets.md).

![](../images/customization/widget-library.png)

#### Redigera schema {#edit-schema}

Om du vill skapa en [anpassad widget](#custom-widgets) för dina instrumentpaneler måste du först identifiera det attribut för kundprofil i realtid som widgeten ska baseras på.

Stegvisa instruktioner för hur du redigerar organisationens schema för att skapa anpassade instrumentpanelswidgetar finns i guiden för [redigering av ditt instrumentpanelsschema](edit-schema.md).

## Nästa steg

När du har läst det här dokumentet är du redo att börja anpassa dina instrumentpaneler i Experience Platform genom att ändra storlek, form och ordning på befintliga widgetar, lägga till standardwidgetar från Adobe eller skapa och dela anpassade widgetar med organisationen.
