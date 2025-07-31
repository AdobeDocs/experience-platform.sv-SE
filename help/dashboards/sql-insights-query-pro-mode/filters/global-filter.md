---
title: Skapa ett globalt filter
description: Lär dig filtrera dina datainsikter med ett anpassat globalt filter.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: 60b0c73766c89b98685810b4f58cfe1a40316dc9
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Skapa ett globalt filter {#create-global-filter}

Om du vill skapa ett globalt filter väljer du först **[!UICONTROL Add filter]** i instrumentpanelsvyn och sedan **[!UICONTROL Global filter]** i listrutan.

>[!IMPORTANT]
>
>Se till att du mappar dina globala filter till alla dina diagram. Detta är inte en automatisk process. Om du vill använda ett globalt filter måste du inkludera en [frågeparameter](../../../query-service/ui/parameterized-queries.md) i diagrammets SQL, [aktivera det globala filtret](#enable-global-filter) i widgetens disposition och [välja ett körtidsvärde](#select-global-filter) för parametern i den globala filterdialogrutan. Se frågeproffshandboken för att lära dig hur du redigerar din SQL om du behöver lägga till en frågeparameter.

![En anpassad kontrollpanel med filtret Lägg till och den nedrullningsbara menyn markerad.](../../images/sql-insights-query-pro-mode/add-filter.png)

Du kan snabbt ändra de insikter som din SQL ger med anpassade globala filter.

Dialogrutan [!UICONTROL Create a global filter] öppnas. När du skapar ett globalt filter följer du samma process som när du skapar en insikt med SQL. Välj först en databas (datamodell med insikter) att fråga efter, ange sedan din anpassade SQL i Frågeredigeraren och slutligen kör-ikonen (![En körningsikon.](/help/images/icons/play.png)).

>[!IMPORTANT]
>
>Du måste inkludera ett ID och ett värde när du skapar ett globalt filter. Med exempelvärdena kan du köra SQL-satsen och skapa diagrammet. Observera att de exempelvärden du anger när du komponerar programsatsen ersätts med de faktiska värden du väljer för datumet eller det globala filtret vid körning.

När frågan har körts visas resultatet på fliken Resultat. Välj **[!UICONTROL Next]**.

>[!NOTE]
>
>Frågeresultaten är som standard begränsade till 100 rader. Om du vill returnera fler rader lägger du till en LIMIT-sats i SQL-frågan med önskat radantal. Om du vill hämta alla rader och ta bort standardgränsen använder du LIMIT 0 i frågan.

![[!UICONTROL Create a global filter dialog] med listrutan Datauppsättning, körningsikonen och nästa markerade.](../../images/sql-insights-query-pro-mode/global-filter.png)

Det sista steget i arbetsflödet för att skapa globala filter kräver att du lägger till en etikett för filtret. Lägg till en etikett i textfältet **[!UICONTROL Filter label]** och välj en filtertyp i listrutan.

>[!NOTE]
>
>Endast filtertypsalternativet [!UICONTROL Combo box] stöds för närvarande.

Välj slutligen **[!UICONTROL Select]** om du vill återgå till instrumentpanelsvyn.

![Textindata för [!UICONTROL Create a global filter dialog] med markering och filteretiketten är markerade.](../../images/sql-insights-query-pro-mode/global-filter-label.png)

## Aktivera det globala filtret för varje insikter {#enable-global-filter}

>[!TIP]
>
>Aktivera de globala filtren i alla diagram du skapar. Detta garanterar att de värden du väljer som ett globalt filter återspeglas i alla dina diagram.

När du har skapat det globala filtret för instrumentpanelen blir växlingsknappen för det globala filtret tillgänglig som en del av widgetens disposition.

![Widgetdispositionen med växlingsknappen för globalt filter markerad.](../../images/sql-insights-query-pro-mode/global-filter-consent.png)

>[!IMPORTANT]
>
>Se till att den globala filterparametern inkluderas i SQL för varje insikt.

## Markera ett globalt filter {#select-global-filter}

Om du vill öppna dialogrutan [!UICONTROL Filters] med alla dina anpassade filter väljer du filterikonen (![En filterikon.](/help/images/icons/filter.png)) till vänster om instrumentpanelen. Om du sedan vill använda effekterna på dina instrumentpanelsinsikter väljer du ett alternativ i listrutan för det globala filtret och väljer **[!UICONTROL Apply]**.

![En anpassad kontrollpanel med filterdialogrutan markerad.](../../images/sql-insights-query-pro-mode/custom-filters.png)

## Rensa globalt filter {#clear-global-filter}

Om du vill ta bort alla egna globala filter väljer du **[!UICONTROL Clear all]** i dialogrutan [!UICONTROL Filters].

![Dialogrutan Filter med Rensa alla markerat.](../../images/sql-insights-query-pro-mode/clear-all.png)
