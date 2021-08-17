---
keywords: ansluta mål;mål ansluta;ansluta mål
title: Skapa en ny målanslutning
type: Tutorial
description: I den här självstudiekursen visas stegen för att ansluta till ett mål i Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Skapa en ny målanslutning

## Översikt {#overview}

Innan du kan skicka målgruppsdata till ett mål måste du skapa en anslutning till målplattformen. I den här artikeln beskrivs hur du konfigurerar ett nytt mål med Adobe Experience Platform användargränssnitt.

## Skapa en ny målanslutning {#setup}

### Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Katalogsida](../assets/ui/connect-destinations/catalog.png)

1. Beroende på om du har en befintlig anslutning till målet kan du se antingen en **[!UICONTROL Configure]**- eller en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan. Välj antingen **[!UICONTROL Configure]** eller **[!UICONTROL Activate]**, beroende på vilken knapp som är tillgänglig för dig.

   ![Katalogsida](../assets/ui/connect-destinations/set-up.png)

   ![Aktivera segment](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### Kontosteg {#account}

Välj **[!UICONTROL New Account]** om du vill konfigurera en ny anslutning till målet. Om du tidigare har konfigurerat en anslutning till målet väljer du **[!UICONTROL Existing Account]** och markerar den befintliga anslutningen.

De inloggningsuppgifter du måste ange i kontosteget varierar beroende på mål och autentiseringstyp.

* För molnlagringsmål måste du ange autentiseringsuppgifter för att Experience Platform ska kunna ansluta till din lagringsplats.

   ![Välj kontotyp för molnlagringsmål](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* För Facebook och flera andra mål för sociala nätverk och annonser väljer du **[!UICONTROL New account]** och sedan **[!UICONTROL Connect to destination]**. Detta tar dig till inloggningssidan för målet, så att du kan ansluta Experience Platform till målet.

   ![Välj kontotyp för sociala mål](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>I avsnittet **[!UICONTROL Connection parameters]** på varje målkatalogsida finns detaljerad information om de parametrar som krävs i det här steget (t.ex. [Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters) kräver en anslutningssträng).

### Autentiseringssteg {#authentication}

Ange anslutningsinformation för målplattformen och välj sedan **[!UICONTROL Create destination]**.

1. Välj de marknadsföringsåtgärder som gäller för de data som du vill exportera till målet. Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i översikten över [dataanvändningsprinciper](../../data-governance/policies/overview.md).

   >[!IMPORTANT]
   >
   >Bilden nedan används endast som illustration. Målanslutningsinformationen varierar mellan olika mål. Detaljerad information om anslutningsinformationen för ditt mål finns i avsnittet **[!UICONTROL Connection parameters]** i varje [målkatalog](../catalog/overview.md) sida (t.ex. [Google Customer Match](../catalog/advertising/google-customer-match.md#parameters)).

   ![Anslut till mål](../assets/ui/connect-destinations/connect-destination.png)

1. Välj **[!UICONTROL Save & Exit]** om du vill spara målkonfigurationen eller välj **[!UICONTROL Next]** om du vill fortsätta till målgruppsdata [aktiveringsflödet](activation-overview.md).