---
keywords: Amazon S3;S3-mål;s3;amazon s3
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagringsplats för att regelbundet exportera CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# [!DNL Amazon S3] anslutning {#s3-connection}

## Destinationsändringslogg {#changelog}

>[!IMPORTANT]
>
>Med betaversionen av exportdataset och de förbättrade funktionerna för filexport kan du nu se två [!DNL Amazon S3] i målkatalogen.
>* Om du redan exporterar filer till **[!UICONTROL Amazon S3]** mål: Skapa nya dataflöden för nya **[!UICONTROL Amazon S3 beta]** mål.
>* Om du ännu inte har skapat några dataflöden till **[!UICONTROL Amazon S3]** mål, använd den nya **[!UICONTROL Amazon S3 beta]** exportera filer till **[!UICONTROL Amazon S3]**.


![Bild av de två Amazon S3-målkorten sida vid sida.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Förbättringar i nya [!DNL Amazon S3] omfattar följande destinationskort:

* [Stöd för dataexport](/help/destinations/ui/export-datasets.md).
* Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möjlighet att anpassa formateringen i exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Översikt {#overview}

Skapa en utgående liveanslutning till din [!DNL Amazon S3] för att med jämna mellanrum exportera datafiler från Adobe Experience Platform till dina egna S3-butiker.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64-encoded] sträng. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!DNL Amazon S3]åtkomstnyckel** och **[!DNL Amazon S3]hemlig nyckel**: I [!DNL Amazon S3], generera ett `access key - secret access key` två för att ge plattformsåtkomst till din [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64-encoded] sträng. Visa ett exempel på en korrekt formaterad, base64-kodad nyckel i dokumentationslänken nedan. Mittdelen förkortas av utrymmesskäl.

![Bild som visar ett exempel på en korrekt formaterad och base64-krypterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Bucketnamn"
>abstract="Måste vara mellan 3 och 63 tecken långt. Måste börja och sluta med en bokstav eller siffra. Får endast innehålla gemena bokstäver, siffror eller bindestreck ( - ). Får inte formateras som en IP-adress (till exempel 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Mappsökväg"
>abstract="Får endast innehålla tecknen A-Z, a-z, 0-9 och kan innehålla följande specialtecken: `/!-_.'()"^[]+$%.*"`. Om du vill skapa en mapp per segmentfil infogar du makrot `/%SEGMENT_NAME%` eller `/%SEGMENT_ID%` eller `/%SEGMENT_NAME%/%SEGMENT_ID%` i textfältet. Makron kan bara infogas i slutet av mappsökvägen. Visa makroexempel i dokumentationen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Använd makron för att skapa en mapp på lagringsplatsen"

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Bucket name]**: ange namnet på [!DNL Amazon S3] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad segmentfil. Läs [Använd makron för att skapa en mapp på lagringsplatsen](overview.md#use-macros) för instruktioner.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

### Obligatoriskt [!DNL Amazon S3] behörigheter {#required-s3-permission}

Ansluta och exportera data till [!DNL Amazon S3] lagringsplats, skapa en IAM-användare (Identity and Access Management) för [!DNL Platform] in [!DNL Amazon S3] och tilldela behörigheter för följande åtgärder:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i [självstudiekurs om hur du exporterar datauppsättningar](/help/destinations/ui/export-datasets.md).

## Exporterade data {#exported-data}

För [!DNL Amazon S3] destinationer, [!DNL Platform] skapar en datafil på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.
