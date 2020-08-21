---
keywords: email;Email;e-mail;email destinations;oracle eloqua;oracle
title: Oracle Eloqua-mål
seo-title: Oracle Eloqua-mål
description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
seo-description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oracle och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
translation-type: tm+mt
source-git-commit: 31b74067903cf7a2ecc4b8f81c11585b672a75ad
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Översikt

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av [!DNL Oracle] som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.

Om du vill skicka segmentdata till [!DNL Oracle Eloqua]måste du först [ansluta målet](#connect-destination) i kunddataplattformen i Adobe och sedan [konfigurera en dataimport](#import-data-into-eloqua) från lagringsplatsen till [!DNL Oracle Eloqua].

## Anslut till mål {#connect-destination}

1. I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** markerar du [!DNL Oracle Eloqua]och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Du kan t. [!DNL Oracle Eloqua]ex. välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

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

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till [!DNL Oracle Eloqua] målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Exporterade data {#exported-data}

För [!DNL Oracle Eloqua] mål skapar Adobe Real-time CDP en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Eloqua_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Konfigurera dataimport i [!DNL Oracle Eloqua] {#import-data-into-eloqua}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från lagringsplatsen till [!DNL Oracle Eloqua]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) i [!DNL Oracle Eloqua Help Center].