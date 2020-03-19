---
title: Oracle Responsys-mål
seo-title: Oracle Responsys-mål
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av Oracle för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
seo-description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av Oracle för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Översikt

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av Oracle för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till Oracle Responsys måste du först [ansluta målet](#connect-destination) i Adobes kunddataplattform för realtid och sedan [konfigurera en dataimport](#import-data-into-responsys) från din lagringsplats till Oracle Responsys.

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Anslutningar > Destinationer]** väljer du Oracle Responsys och sedan **[!UICONTROL Connect-mål]**.

   ![Anslut till svar](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. Välj **[!UICONTROL anslutningstyp]** för lagringsplatsen i Anslutningsmålguiden. För Oracle Responsys kan du välja mellan **SFTP med lösenord** och **SFTP med SSH-nyckel**. Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj **[!UICONTROL Anslut]**.

   ![Ställ in svarsguiden](/help/rtcdp/destinations/assets/responsys-wizard.png)

   För **SFTP med lösenordsanslutningar** måste du ange domän, port, användarnamn och lösenord.
För **SFTP med SSH-nyckelanslutningar** måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i svarsinformation](/help/rtcdp/destinations/assets/responsys-step2.png)

1. I **Grundläggande information**, fyll i relevant information för destinationen enligt nedan:
   * **Namn**: Välj ett relevant namn för destinationen.
   * **Beskrivning**: Ange en beskrivning för destinationen.
   * **Mappsökväg**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **Filformat**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.
   ![Grundläggande information om svar](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Klicka på **Skapa** när du har fyllt i fälten i **Grundläggande information**. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till Oracle Responsys-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport i Oracle Responsys {#import-data-into-responsys}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från din lagringsplats till Oracle Responsys. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i hjälpcentret för Oracle Responsys.