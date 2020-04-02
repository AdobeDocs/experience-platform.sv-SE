---
title: Oracle Eloqua-mål
seo-title: Oracle Eloqua-mål
description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
seo-description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Oracle Eloqua

## Översikt

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle som syftar till att hjälpa B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.

Om du vill skicka segmentdata till Oracle Eloqua måste du först [ansluta målet](#connect-destination) i Adobes kunddataplattform för realtid och sedan [konfigurera en dataimport](#import-data-into-eloqua) från din lagringsplats till Oracle Eloqua.

## Anslut till mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** väljer du Oracle Eloqua och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. För Oracle Eloqua kan du välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

   För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.
För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Konfigurera Eloqua-guiden](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. I **[!UICONTROL Setup]** steget fyller du i relevant information för destinationen enligt nedan:
   * **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
   * **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
   * **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Eloqua grundläggande information](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Klicka **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet har skapats och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Oracle Eloqua-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport till Oracle Eloqua {#import-data-into-eloqua}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Oracle Eloqua. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) i hjälpcentret för Oracle Eloqua.