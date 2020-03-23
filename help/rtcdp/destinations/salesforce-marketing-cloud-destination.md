---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget och som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
seo-description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget och som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Översikt

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

Om du vill skicka segmentdata till Salesforce Marketing Cloud måste du först [ansluta målet](#connect-destination) i Adobe CDP i realtid och sedan [konfigurera en dataimport](#import-data-into-salesforce) från din lagringsplats till Salesforce Marketing Cloud.

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du Salesforce Marketing Cloud och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Välj lagringsplats **[!UICONTROL Connection type]** i guiden Anslut till mål. För Salesforce Marketing Cloud kan du välja mellan **SFTP med lösenord** och **SFTP med SSH-nyckel**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect]**.

   ![Konfigurera Salesforce-guiden](/help/rtcdp/destinations/assets/salesforce-step1.png)

   För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord.
För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i Salesforce-information](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. I **Grundläggande information**, fyll i relevant information för destinationen enligt nedan:
   * **Namn**: Välj ett relevant namn för destinationen.
   * **Beskrivning**: Ange en beskrivning för destinationen.
   * **Mappsökväg**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **Filformat**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Grundläggande information för Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Klicka på **Skapa** när du har fyllt i fälten i **Grundläggande information**. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Salesforce Marketing Cloud-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport i Salesforce Marketing Cloud {#import-data-into-salesforce}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Salesforce Marketing Cloud. Mer information om hur du gör detta finns i [Importera prenumeranter till Marketing Cloud från en fil](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) i Salesforce Help Center.