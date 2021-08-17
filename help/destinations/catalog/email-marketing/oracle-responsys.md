---
keywords: e-post;E-post;e-postadresser;oraclets svarsmål
title: Oraclena svarssystemanslutning
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oraclet erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!DNL Oracle Responsys] anslutning

## Översikt {#overview}

[Responsys ](https://www.oracle.com/cx/marketing/campaign-management/) är ett verktyg för e-postmarknadsföring i storföretag för flerkanalskampanjer som erbjuds av  [!DNL Oracle] att personalisera interaktioner i e-post, mobiler, displayannonsering och sociala medier.

Om du vill skicka segmentdata till [!DNL Oracle Responsys] måste du först [ansluta till målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-responsys) från lagringsplatsen till [!DNL Oracle Responsys].

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-batch-profile-destinations.md#select-attributes)målgruppsaktivering.

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adressen tillåtelselista för molnlagringsdestinationer](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

Detta mål stöder följande anslutningstyper:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* För **[!UICONTROL SFTP with Password]**-anslutningar måste du ange:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* För **[!UICONTROL SFTP with SSH Key]**-anslutningar måste du ange:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]
* Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under **[!UICONTROL Key]**-avsnittet. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.
* **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
* **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där Plattform ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
* **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att batchprofilens exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Målattribut {#destination-attributes}

När du aktiverar segment till det här målet rekommenderar Adobe att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [metodtips när du aktiverar målgrupper för e-postmarknadsföringsmål](overview.md#best-practices).

## Exporterade data {#exported-data}

För [!DNL Oracle Responsys]-mål skapar Plattform en tabbavgränsad `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [verifiera segmentaktivering](../../ui/activate-batch-profile-destinations.md#verify) i segmentaktiveringsjälvstudiekursen.

## Konfigurera dataimport till [!DNL Oracle Responsys] {#import-data-into-responsys}

När du har anslutit [!DNL Platform] till ditt [!DNL SFTP]-lagringsutrymme måste du konfigurera dataimporten från din lagringsplats till [!DNL Oracle Responsys]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].
