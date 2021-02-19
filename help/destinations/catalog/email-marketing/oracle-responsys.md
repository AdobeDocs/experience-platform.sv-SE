---
keywords: e-post;E-post;e-postadresser;oracle svarar på målet
title: Oracle Responsys-anslutning
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oracle erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# [!DNL Oracle Responsys] anslutning

[Responsys ](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) är ett verktyg för e-postmarknadsföring i storföretag för flerkanalskampanjer som erbjuds av  [!DNL Oracle] att personalisera interaktioner i e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till [!DNL Oracle Responsys] måste du först [ansluta till målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-responsys) från lagringsplatsen till [!DNL Oracle Responsys].

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Anslutningsmål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL Oracle Responsys] och sedan **[!UICONTROL Connect destination]**.

![Anslut till svar](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

I steget **[!UICONTROL Authentication]** väljer du **[!UICONTROL Existing Account]** och en av dina befintliga anslutningar om du tidigare har konfigurerat en anslutning till molnlagringsmålet. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning. Fyll i autentiseringsuppgifterna för ditt konto och välj **[!UICONTROL Connect to destination]**. För [!DNL Oracle Responsys] kan du välja mellan **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på din anslutningstyp, och välj **[!UICONTROL Connect to destination]**.

För **[!UICONTROL SFTP with Password]**-anslutningar måste du ange domän, port, användarnamn och lösenord.

För **[!UICONTROL SFTP with SSH Key]**-anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

![Fyll i svarsinformation](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

I steget **[!UICONTROL Setup]** ska du fylla i relevant information för destinationen enligt nedan:
- **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
- **[!UICONTROL Bucket name]**: Din Amazon S3-bucket, där Platform sparar dataexporten. Indata måste vara mellan 3 och 63 tecken långa. Måste börja och sluta med en bokstav eller siffra. Får endast innehålla gemena bokstäver, siffror eller bindestreck ( - ). Får inte formateras som en IP-adress (till exempel 192.100.1.1).
- **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där Plattform ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
- **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.
- **[!UICONTROL Marketing actions]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns på sidan [Datastyrning i Adobe Experience Platform](../../../data-governance/policies/overview.md). Mer information om de enskilda Adobe-definierade marknadsföringsåtgärderna finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

![Grundläggande information om svar](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klicka på **[!UICONTROL Create destination]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](../../ui/activate-destinations.md) till målet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md).

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till målet [!DNL Oracle Responsys] rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes) i Destinationer för e-postmarknadsföring.

## Exporterade data {#exported-data}

För [!DNL Oracle Responsys]-mål skapar Platform en tabbavgränsad `.txt`- eller `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport till [!DNL Oracle Responsys] {#import-data-into-responsys}

När du har anslutit plattformen till ditt [!DNL Amazon S3]- eller SFTP-lagringsutrymme måste du konfigurera dataimporten från din lagringsplats till [!DNL Oracle Responsys]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].