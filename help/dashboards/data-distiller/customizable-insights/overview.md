---
title: Anpassningsbara insikter för utökad apprapportering
description: Lär dig hur du använder SQL-frågor för att generera insikter för dina anpassade instrumentpaneler.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Anpassningsbara insikter för utökad apprapportering

Använd anpassade SQL-frågor för att effektivt extrahera insikter från olika strukturerade datauppsättningar. Teknikerna kan använda frågeproffsläge för att utföra komplexa analyser med SQL och sedan dela analysen med icke-tekniska användare via diagram på din anpassade kontrollpanel eller exportera dem i CSV-filer. Den här metoden för att skapa insikter är väl anpassad för tabeller med tydliga relationer och ger en större grad av anpassning inom era insikter och filter som kan passa nischexempel.

>[!IMPORTANT]
>
>Frågeproffsläget är bara tillgängligt för användare som har köpt [Data Distiller SKU](../../../query-service/data-distiller/overview.md).

Om du vill generera insikter från SQL måste du först skapa en instrumentpanel.

## Skapa en anpassad kontrollpanel {#create-custom-dashboard}

Om du vill skapa en anpassad kontrollpanel väljer du **[!UICONTROL Dashboards]** från den vänstra navigeringspanelen för att öppna arbetsytan Kontrollpaneler. Nästa, välj **[!UICONTROL Create dashboard]**.

![Kontrollpanelens lager med Skapa kontrollpanel markerat.](../../images/customizable-insights/create-dashboard.png)

The **[!UICONTROL Create dashboard]** visas. Det finns två alternativ att välja mellan när du vill skapa en instrumentpanel. Om du vill skapa insikter kan du antingen använda en befintlig datamodell med [[!UICONTROL Guided design mode]](../../user-defined-dashboards.md) eller din egen SQL med [!UICONTROL Query pro mode].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Att använda en befintlig datamodell har fördelarna med att tillhandahålla ett strukturerat, effektivt och skalbart ramverk som är skräddarsytt efter just era affärsbehov. Så här lär du dig hur [skapa insikter från en befintlig datamodell](../../user-defined-dashboards.md#create-widget)finns i den anpassade handboken för kontrollpanelen.

Insikter som genererats från SQL-frågor ger mycket större flexibilitet och anpassning. Teknikerna kan använda frågeproffsläge för att utföra komplexa analyser på SQL och sedan dela analysen med icke-tekniska användare via denna kontrollpanel. Välj **[!UICONTROL Query pro mode]** följt av **[!UICONTROL Save]**.

>[!NOTE]
>
>När du har gjort ett val kan du inte ändra det här valet på den instrumentpanelen. I stället måste du skapa en ny instrumentpanel med en annan metod för att skapa instrumentpaneler.

![The [!UICONTROL Create dashboard] där Query Pro och Save är markerade.](../../images/customizable-insights/query-pro-mode.png)

## Skapa ett diagram {#create-a-chart}

Se [guide för frågeproffsläge](./query-pro-mode.md) om du vill ha stegvisa instruktioner om hur du skapar ett diagram med SQL.
