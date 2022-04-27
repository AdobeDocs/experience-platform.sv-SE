---
keywords: ansluta mål;mål ansluta;ansluta mål
title: Skapa en ny målanslutning
type: Tutorial
description: I den här självstudiekursen visas stegen för att ansluta till ett mål i Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 729c0724c7af88bb69c9d68a45d58c3575c90828
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Skapa en ny målanslutning

>[!IMPORTANT]
> 
>Om du vill ansluta till ett mål behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

## Översikt {#overview}

Innan du kan skicka målgruppsdata till ett mål måste du skapa en anslutning till målplattformen. I den här artikeln beskrivs hur du konfigurerar ett nytt mål med Adobe Experience Platform användargränssnitt.

## Skapa en ny målanslutning {#setup}

1. Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Katalogsida](../assets/ui/connect-destinations/catalog.png)

1. Beroende på om du har en befintlig anslutning till ditt mål kan du se en **[!UICONTROL Set up]** eller en **[!UICONTROL Activate segments]** på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate segments]** och **[!UICONTROL Set up]**, se [Katalog](../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

   Välj antingen **[!UICONTROL Set up]** eller **[!UICONTROL Activate segments]**, beroende på vilken knapp som är tillgänglig för dig.

   ![Katalogsida](../assets/ui/connect-destinations/set-up.png)

   ![Aktivera segment](../assets/ui/connect-destinations/activate-segments.png)

1. Om du valde **[!UICONTROL Set up]** går du vidare till nästa steg.

   Om du valde **[!UICONTROL Activate segments]** kan du nu se en lista över befintliga målanslutningar.

   Välj **[!UICONTROL Configure new destination]**.

   ![Konfigurera nytt mål](../assets/ui/connect-destinations/configure-new-destination.png)

1. Ange anslutningsinformation för målplattformen och välj **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >Bilden nedan används endast som illustration. Målanslutningsinformationen varierar mellan olika mål. Mer information om anslutningsinformation för ditt mål finns i **Anslutningsparametrar** i varje [målkatalog](../catalog/overview.md) sida (till exempel [Google kundmatchning](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Anslut till mål](../assets/ui/connect-destinations/connect-destination.png)

1. (Valfritt) Välj de aviseringar om måldataflöde som du vill prenumerera på. Du kan prenumerera på varningar när du skapar ett dataflöde för att få varningsmeddelanden om status, om det lyckades eller om det inte gick att köra ditt flöde. Se [Prenumerera på aviseringar om destinationer i sitt sammanhang](alerts.md) om du vill ha detaljerad information om varningar om måldataflöde.

   ![Användargränssnittsbild som visar prenumerationsalternativen för destinationsaviseringar i sitt sammanhang](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Välj **[!UICONTROL Next]**.

   ![Anslut till mål](../assets/ui/connect-destinations/next.png)

1. Välj de marknadsföringsåtgärder som gäller för de data som du vill exportera till målet. Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [dataanvändningsprinciper - översikt](../../data-governance/policies/overview.md) sida.

   ![Välj marknadsföringsåtgärder](../assets/ui/connect-destinations/governance.png)

1. Välj **[!UICONTROL Save & Exit]** för att spara målkonfigurationen, eller välj **[!UICONTROL Next]** för att gå vidare till målgruppsdata [aktiveringsflöde](activation-overview.md).