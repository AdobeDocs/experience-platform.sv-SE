---
title: Oracle Responsys-mål
seo-title: Oracle Responsys-mål
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av Oracle för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
seo-description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av Oracle för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Översikt

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) är ett verktyg för e-postmarknadsföring i storföretag för flerkanalskampanjer som erbjuds av [!DNL Oracle] att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till [!DNL Oracle Responsys]måste du först [ansluta till målet](#connect-destination) i Adobe Real-time Customer Data Platform och sedan [konfigurera en dataimport](#import-data-into-responsys) från lagringsplatsen till [!DNL Oracle Responsys].

## Koppla mål {#connect-destination}

1. I **[!UICONTROL Connections > Destinations]** markerar du [!DNL Oracle Responsys]och väljer sedan **[!UICONTROL Connect destination]**.

   ![Anslut till svar](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Du kan t. [!DNL Oracle Responsys]ex. välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

   För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.
För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

   ![Fyll i svarsinformation](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. I **[!UICONTROL Setup]** steget fyller du i relevant information för destinationen enligt nedan:
   * **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
   * **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
   * **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
   * **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat du vill exportera till lagringsplatsen.

   ![Grundläggande information om svar](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Klicka **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](/help/rtcdp/destinations/activate-destinations.md) till målet.

## Målattribut {#destination-attributes}

När du [aktiverar segment](/help/rtcdp/destinations/activate-destinations.md) till [!DNL Oracle Responsys] målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Konfigurera dataimport i [!DNL Oracle Responsys] {#import-data-into-responsys}

När du har anslutit CDP i realtid till din Amazon S3- eller SFTP-lagring måste du konfigurera dataimporten från lagringsplatsen till [!DNL Oracle Responsys]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].