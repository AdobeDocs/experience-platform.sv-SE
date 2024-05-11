---
title: Skapa ett globalt filter
description: Lär dig filtrera dina datainsikter med ett anpassat globalt filter.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Skapa ett globalt filter {#create-global-filter}

Om du vill skapa ett globalt filter väljer du först **[!UICONTROL Add filter]** från kontrollpanelsvyn och sedan **[!UICONTROL Global filter]** i listrutan.

>[!IMPORTANT]
>
>Se till att du mappar dina globala filter till alla dina diagram. Detta är inte en automatisk process. Om du vill använda ett globalt filter måste du inkludera en [frågeparameter](../../../../query-service/ui/parameterized-queries.md) i diagrammets SQL, [aktivera globalt filter](#enable-global-filter) i widgetdispositionen, och [välj ett körtidsvärde](#select-global-filter) för parametern i den globala filterdialogrutan. Se frågeproffshandboken för att lära dig hur du redigerar din SQL om du behöver lägga till en frågeparameter.

![En anpassad kontrollpanel med Lägg till filter och dess listruta markerad.](../../../images/customizable-insights/add-filter.png)

Du kan snabbt ändra de insikter som din SQL ger med anpassade globala filter.

The [!UICONTROL Create a global filter] öppnas. När du skapar ett globalt filter följer du samma process som när du skapar en insikt med SQL. Välj först en databas (datamodell med insikter) att fråga efter, ange sedan din anpassade SQL i Frågeredigeraren och slutligen välj körningsikonen (![En körningsikon.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Du måste inkludera ett ID och ett värde när du skapar ett globalt filter. Med exempelvärdena kan du köra SQL-satsen och skapa diagrammet. Observera att de exempelvärden du anger när du komponerar programsatsen ersätts med de faktiska värden du väljer för datumet eller det globala filtret vid körning.

När frågan har körts visas resultatet på fliken Resultat. Välj **[!UICONTROL Next]**.

![The [!UICONTROL Create a global filter dialog] med datamängdens listruta, ikonen kör och Nästa markerat.](../../../images/customizable-insights/global-filter.png)

Det sista steget i arbetsflödet för att skapa globala filter kräver att du lägger till en etikett för filtret. Lägg till en etikett i **[!UICONTROL Filter label]** textfält och välj en filtertyp i listrutan.

>[!NOTE]
>
>Endast [!UICONTROL Combo box] Filtertypsalternativ stöds för närvarande.

Äntligen väljer du **[!UICONTROL Select]** för att återgå till din instrumentpanel.

![The [!UICONTROL Create a global filter dialog] med markering och textinmatning för filteretikett markerat.](../../../images/customizable-insights/global-filter-label.png)

## Aktivera det globala filtret för varje insikter {#enable-global-filter}

>[!TIP]
>
>Aktivera de globala filtren i alla diagram du skapar. Detta garanterar att de värden du väljer som ett globalt filter återspeglas i alla dina diagram.

När du har skapat det globala filtret för instrumentpanelen blir växlingsknappen för det globala filtret tillgänglig som en del av widgetens disposition.

![Widgetdispositionen med växlingsknappen Global Filter markerad.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Se till att den globala filterparametern inkluderas i SQL för varje insikt.

## Markera ett globalt filter {#select-global-filter}

Öppna [!UICONTROL Filters] som visar alla dina anpassade filter väljer du filterikonen (![En filterikon.](../../../images/customizable-insights/filter.png)) till vänster om din instrumentpanel. Om du vill använda effekterna på instrumentpanelsinsikter väljer du ett alternativ i listrutan för det globala filtret och väljer sedan **[!UICONTROL Apply]**.

![En anpassad kontrollpanel med filterdialogrutan markerad.](../../../images/customizable-insights/custom-filters.png)
