---
keywords: e-post;E-post;e-post;e-postmål;oracle eloqua;oracle
title: Oracle Eloqua-anslutning
description: Oracle Eloqua är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av Oraclet och som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] anslutning

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) är en SaaS-plattform (Software as a service) för automatiserad marknadsföring som erbjuds av  [!DNL Oracle] som hjälper B2B-marknadsförare och organisationer att hantera marknadsföringskampanjer och generera säljleads.

Om du vill skicka segmentdata till [!DNL Oracle Eloqua] måste du först [ansluta målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-eloqua) från lagringsplatsen till [!DNL Oracle Eloqua].

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

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

Se [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till mål.

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till det här målet rekommenderar Adobe att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes).

## Exporterade data {#exported-data}

För [!DNL Oracle Eloqua]-mål skapar Plattform en tabbavgränsad `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport till [!DNL Oracle Eloqua] {#import-data-into-eloqua}

När du har anslutit [!DNL Platform] till ditt [!DNL SFTP]-lagringsutrymme måste du konfigurera dataimporten från din lagringsplats till [!DNL Oracle Eloqua]. Mer information om hur du gör detta finns i [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) i [!DNL Oracle Eloqua Help Center].
