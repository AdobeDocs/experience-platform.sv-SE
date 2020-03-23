---
title: Oracle Eloqua-mål
seo-title: Oracle Eloqua-mål
description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
seo-description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Översikt

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle som syftar till att hjälpa B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.

Om du vill skicka segmentdata till Oracle Eloqua måste du först [ansluta målet](#connect-destination) i Adobes kunddataplattform för realtid och sedan [konfigurera en dataimport](#import-data-into-eloqua) från din lagringsplats till Oracle Eloqua.

## Anslut till mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du Oracle Eloqua och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. Välj lagringsplats **[!UICONTROL Connection type]** i guiden Anslut till mål. För Oracle Eloqua kan du välja mellan **SFTP med lösenord** och **SFTP med SSH-nyckel**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect]**.

   ![Konfigurera Eloqua-guiden](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord.
För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i Eloqua-information](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. I **Grundläggande information**, fyll i relevant information för destinationen enligt nedan:
   * **Namn**: Välj ett relevant namn för destinationen.
   * **Beskrivning**: Ange en beskrivning för destinationen.
   * **Mappsökväg**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **Filformat**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Eloqua grundläggande information](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Klicka på **Skapa** när du har fyllt i fälten i **Grundläggande information**. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Oracle Eloqua-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport till Oracle Eloqua {#import-data-into-eloqua}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Oracle Eloqua. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) i hjälpcentret för Oracle Eloqua.