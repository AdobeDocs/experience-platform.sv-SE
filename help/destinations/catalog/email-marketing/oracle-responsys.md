---
keywords: e-post;E-post;e-postadresser;oraclets svarsmål
title: Oraclena svarssystemanslutning
description: Responsys är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som Oraclet erbjuder för att personalisera interaktioner över e-post, mobiler, displayannonsering och sociala medier.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# [!DNL Oracle Responsys] anslutning

## Översikt {#overview}

[Svar](https://www.oracle.com/cx/marketing/campaign-management/) är ett e-postmarknadsföringsverktyg för företag för flerkanalskampanjer som erbjuds av [!DNL Oracle] för att personalisera interaktioner över e-post, mobiler, webbannonsering och sociala medier.

Skicka segmentdata till [!DNL Oracle Responsys]måste du först [ansluta till målet](#connect-destination) i Adobe Experience Platform, och [konfigurera en dataimport](#import-data-into-responsys) från din lagringsplats till [!DNL Oracle Responsys].

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adress tillåtelselista för molnlagringsmål](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

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
* **[!UICONTROL File Format]**: Välj **CSV** för att exportera CSV-filer till lagringsplatsen.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Målattribut {#destination-attributes}

När du aktiverar segment till det här målet rekommenderar Adobe att du väljer en unik identifierare från din [union](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [bästa praxis när ni aktiverar målgrupper för e-postmarknadsföring](overview.md#best-practices).

## Exporterade data {#exported-data}

För [!DNL Oracle Responsys] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [verifiera aktivering av segment](../../ui/activate-batch-profile-destinations.md#verify) i segmentaktiveringssjälvstudiekursen.

## Konfigurera dataimport i [!DNL Oracle Responsys] {#import-data-into-responsys}

Efter anslutning [!DNL Platform] till [!DNL SFTP] måste du konfigurera dataimporten från lagringsplatsen till [!DNL Oracle Responsys]. Om du vill lära dig hur du gör detta kan du läsa [Importera kontakter eller konton](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) i [!DNL Oracle Responsys Help Center].
