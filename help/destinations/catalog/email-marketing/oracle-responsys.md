---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Oracle Responsys-mål
seo-title: Oracle Responsys-mål
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oracle erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
seo-description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oracle erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Översikt

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) är ett verktyg för e-postmarknadsföring i storföretag för flerkanalskampanjer som erbjuds av [!DNL Oracle] att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till [!DNL Oracle Responsys]måste du först [ansluta till målet](#connect-destination) i kunddataplattformen i realtid och sedan [konfigurera en dataimport](#import-data-into-responsys) från lagringsplatsen till [!DNL Oracle Responsys].

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [för](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Koppla mål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** markerar du [!DNL Oracle Responsys]och sedan **[!UICONTROL Connect destination]**.

![Anslut till svar](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Du kan t. [!DNL Oracle Responsys]ex. välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.

För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

![Fyll i svarsinformation](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

I **[!UICONTROL Setup]** steget fyller du i relevant information för destinationen enligt nedan:
- **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
- **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
- **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.

![Grundläggande information om svar](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klicka **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](../../ui/activate-destinations.md) till målet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) .

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till [!DNL Oracle Responsys] målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Exporterade data {#exported-data}

För [!DNL Oracle Responsys] mål skapar CDP i realtid en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport i [!DNL Oracle Responsys] {#import-data-into-responsys}

När du har anslutit CDP i realtid till din [!DNL Amazon S3] eller SFTP-lagringen måste du konfigurera dataimporten från din lagringsplats till [!DNL Oracle Responsys]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].