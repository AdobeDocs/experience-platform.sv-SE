---
keywords: email;Email;e-mail;email destinations;salesforce;salesforce destination
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
seo-description: Salesforce Marketing Cloud är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## Översikt

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

Om du vill skicka segmentdata till [!DNL Salesforce Marketing Cloud]måste du först [ansluta målet](#connect-destination) i CDP i realtid och sedan [konfigurera en dataimport](#import-data-into-salesforce) från lagringsplatsen till [!DNL Salesforce Marketing Cloud].

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [för](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Koppla mål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** markerar du [!DNL Salesforce Marketing Cloud]och sedan **[!UICONTROL Connect destination]**.

![Anslut till Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du **[!UICONTROL Authentication]** och väljer en av dina befintliga anslutningar i **[!UICONTROL Existing Account]** steget. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Du kan t. [!DNL Salesforce Marketing Cloud]ex. välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.

För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

![Fyll i Salesforce-information](../../assets/catalog/email-marketing/salesforce/account-info.png)

I **[!UICONTROL Setup]** steget fyller du i relevant information för destinationen enligt nedan:
- **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
- **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
- **[!UICONTROL File Format]**: **[!UICONTROL CSV]** eller **[!UICONTROL TAB_DELIMITED]**. Välj vilket filformat som ska exporteras till lagringsplatsen.

![Grundläggande information för Salesforce](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Klicka **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](../../ui/activate-destinations.md) till målet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) .

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till [!DNL Salesforce Marketing Cloud] målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Exporterade data {#exported-data}

För [!DNL Salesforce Marketing Cloud] mål skapar CDP i realtid en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport i [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

När du har anslutit CDP i realtid till din [!DNL Amazon S3] eller SFTP-lagringen måste du konfigurera dataimporten från din lagringsplats till [!DNL Salesforce Marketing Cloud]. Mer information om hur du gör detta finns i [Importera prenumeranter till Marketing Cloud från en fil](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) i [!DNL Salesforce Help Center].