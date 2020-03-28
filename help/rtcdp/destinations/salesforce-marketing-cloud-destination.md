---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget och som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
seo-description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget och som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Salesforce Marketing Cloud

## Översikt

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

Om du vill skicka segmentdata till Salesforce Marketing Cloud måste du först [ansluta målet](#connect-destination) i Adobe CDP i realtid och sedan [konfigurera en dataimport](#import-data-into-salesforce) från din lagringsplats till Salesforce Marketing Cloud.

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du Salesforce Marketing Cloud och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. För Salesforce Marketing Cloud kan du välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

   För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.
För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i Salesforce-information](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. I **[!UICONTROL Setup]** steget fyller du i relevant information för destinationen enligt nedan:
   * **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
   * **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
   * **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **[!UICONTROL File Format]**: **[!UICONTROL CSV]** eller **[!UICONTROL TAB_DELIMITED]**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Grundläggande information för Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Klicka **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Salesforce Marketing Cloud-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport i Salesforce Marketing Cloud {#import-data-into-salesforce}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Salesforce Marketing Cloud. Mer information om hur du gör detta finns i [Importera prenumeranter till Marketing Cloud från en fil](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) i Salesforce Help Center.