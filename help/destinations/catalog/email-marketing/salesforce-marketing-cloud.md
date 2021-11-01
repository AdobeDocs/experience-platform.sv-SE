---
keywords: e-post;E-post;e-post;e-postadresser;salesforce;salesforce-mål
title: Salesforce Marketing Cloud-anslutning
seo-description: Salesforce Marketing Cloud is a digital marketing suite formerly known as ExactTarget that allows you to build and customize journeys for visitors and customers to personalize their experience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] anslutning

## Översikt {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) är en digital marknadsföringssvit som tidigare kallades ExactTarget som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

Skicka segmentdata till [!DNL Salesforce Marketing Cloud]måste du först [ansluta till målet](#connect-destination) i Platform, och sedan [konfigurera en dataimport](#import-data-into-salesforce) från din lagringsplats till [!DNL Salesforce Marketing Cloud].

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut på [målaktiveringsarbetsflöde](../../ui/activate-batch-profile-destinations.md#select-attributes).

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adress tillåtelselista för molnlagringsmål](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

Detta mål stöder följande anslutningstyper:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* För **[!UICONTROL SFTP with Password]** anslutningar måste du ange:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under **[!UICONTROL Key]** -avsnitt. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.
* **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
* **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där Plattform ska placera dina exportdata som CSV-filer.
* **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Målattribut {#destination-attributes}

När du aktiverar segment till det här målet rekommenderar Adobe att du väljer en unik identifierare från din [union](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [bästa praxis när ni aktiverar målgrupper för e-postmarknadsföring](overview.md#best-practices).

## Exporterade data {#exported-data}

För [!DNL Salesforce Marketing Cloud] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [verifiera aktivering av segment](../../ui/activate-batch-profile-destinations.md#verify) i segmentaktiveringssjälvstudiekursen.

## Konfigurera dataimport i [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Efter anslutning [!DNL Platform] till [!DNL SFTP] måste du konfigurera dataimporten från lagringsplatsen till [!DNL Salesforce Marketing Cloud]. Om du vill lära dig hur du gör detta kan du läsa [Importera prenumeranter till Marketing Cloud från en fil](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) i [!DNL Salesforce Help Center].
