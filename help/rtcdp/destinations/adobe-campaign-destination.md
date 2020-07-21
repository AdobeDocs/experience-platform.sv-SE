---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
seo-description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Adobe Campaign

## Översikt

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Mer information finns i [Om Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Om du vill skicka segmentdata till Adobe Campaign måste du först [ansluta målet](#connect-destination) i Adobe Customer Data Platform i realtid och sedan [konfigurera en dataimport](#import-data-into-campaign) från din lagringsplats till Adobe Campaign.

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du Adobe Campaign och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Adobes kampanj](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. I arbetsflödet för anslutningsmål väljer du **[!UICONTROL Connection type]** lagringsplats. För Adobe Campaign kan du välja mellan **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj sedan **[!UICONTROL Connect]**.

   ![Konfigurera kampanjguiden](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   För **[!UICONTROL Amazon S3]** anslutningar måste du ange ditt ID för åtkomstnyckel och hemlig åtkomstnyckel.
För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.
För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i Campaign-information](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Fyll i **[!UICONTROL Basic Information]** den relevanta informationen för destinationen enligt nedan:
   * **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
   * **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
   * **[!UICONTROL Bucket Name]**: *För S3-anslutningar*. Ange platsen för S3-bucket där CDP i realtid ska placera dina exportdata som CSV- eller tabbavgränsade filer.
   * **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.

   ![Grundläggande information om kampanj](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klicka **[!UICONTROL Create]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till målet Adobe Campaign rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.


## Konfigurera dataimport i Adobe Campaign {#import-data-into-campaign}

När du har anslutit CDP i realtid till din [!DNL Amazon S3] eller SFTP-lagringen måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i [Importera data](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) i hjälpdokumentationen för Adobe Campaign.