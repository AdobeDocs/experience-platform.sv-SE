---
keywords: ansluta mål;mål ansluta;ansluta mål
title: Skapa en ny målanslutning
type: Tutorial
description: I den här självstudiekursen visas stegen för att ansluta till ett mål i Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Skapa en ny målanslutning

## Översikt {#overview}

Innan du kan skicka målgruppsdata till ett mål måste du skapa en anslutning till målplattformen. I den här artikeln beskrivs hur du konfigurerar ett nytt mål med Adobe Experience Platform användargränssnitt.

## Skapa en ny målanslutning {#setup}

1. Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Katalogsida](../assets/ui/connect-destinations/catalog.png)

1. Beroende på om du har en befintlig anslutning till målet kan du se antingen en **[!UICONTROL Set up]**- eller en **[!UICONTROL Activate segments]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate segments]** och **[!UICONTROL Set up]** finns i avsnittet [Katalog](../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

   Välj antingen **[!UICONTROL Set up]** eller **[!UICONTROL Activate segments]**, beroende på vilken knapp som är tillgänglig för dig.

   ![Katalogsida](../assets/ui/connect-destinations/set-up.png)

   ![Aktivera segment](../assets/ui/connect-destinations/activate-segments.png)

1. Om du valde **[!UICONTROL Set up]** går du vidare till nästa steg.

   Om du valde **[!UICONTROL Activate segments]** kan du nu se en lista över befintliga målanslutningar.

   Välj **[!UICONTROL Configure new destination]**.

   ![Konfigurera nytt mål](../assets/ui/connect-destinations/configure-new-destination.png)

1. Ange anslutningsinformation för målplattformen och välj sedan **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >Bilden nedan används endast som illustration. Målanslutningsinformationen varierar mellan olika mål. Detaljerad information om anslutningsinformationen för ditt mål finns i avsnittet **Anslutningsparametrar** i varje [målkatalog](../catalog/overview.md) sida (t.ex. [Google Customer Match](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Anslut till mål](../assets/ui/connect-destinations/connect-destination.png)

1. Välj **[!UICONTROL Next]**.

   ![Anslut till mål](../assets/ui/connect-destinations/next.png)

1. Välj de marknadsföringsåtgärder som gäller för de data som du vill exportera till målet. Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i översikten över [dataanvändningsprinciper](../../data-governance/policies/overview.md).

   ![Välj marknadsföringsåtgärder](../assets/ui/connect-destinations/governance.png)

1. Välj **[!UICONTROL Save & Exit]** om du vill spara målkonfigurationen eller välj **[!UICONTROL Next]** om du vill fortsätta till målgruppsdata [aktiveringsflödet](activation-overview.md).