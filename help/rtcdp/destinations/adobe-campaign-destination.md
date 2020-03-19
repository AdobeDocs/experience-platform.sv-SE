---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
seo-description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## Översikt

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Mer information finns i [Om Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Om du vill skicka segmentdata till Adobe Campaign måste du först [ansluta destinationen](#connect-destination) i Adobes kunddataplattform i realtid och sedan [konfigurera en dataimport](#import-data-into-campaign) från din lagringsplats till Adobe Campaign.

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Anslutningar > Destinationer]** väljer du Adobe Campaign och sedan **[!UICONTROL Connect-mål]**.

   ![Anslut till Adobes kampanj](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Välj **[!UICONTROL anslutningstyp]** för lagringsplatsen i Anslutningsmålguiden. För Adobe Campaign kan du välja mellan **Amazon S3**, **SFTP med lösenord** och **SFTP med SSH-nyckel**. Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj sedan **[!UICONTROL Anslut]**.

   ![Konfigurera kampanjguiden](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   För **S3** -anslutningar måste du ange ditt nyckel-ID och hemlig åtkomstnyckel.
För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord.
För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i Campaign-information](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. I **Grundläggande information**, fyll i relevant information för destinationen enligt nedan:
   * **Namn**: Välj ett relevant namn för destinationen.
   * **Beskrivning**: Ange en beskrivning för destinationen.
   * **Buckennamn**: *För S3-anslutningar*. Ange platsen för S3-bucket där CDP i realtid ska placera dina exportdata som CSV- eller tabbavgränsade filer.
   * **Mappsökväg**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **Filformat**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Grundläggande information om kampanj](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klicka på **Skapa** när du har fyllt i fälten i **Grundläggande information**. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Adobe Campaign-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.


## Konfigurera dataimport i Adobe Campaign {#import-data-into-campaign}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i [Importera data](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) i hjälpdokumentationen för Adobe Campaign.