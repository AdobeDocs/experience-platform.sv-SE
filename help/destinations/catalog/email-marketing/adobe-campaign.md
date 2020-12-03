---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
seo-description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---


# Adobe Campaign

## Översikt

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Mer information finns [i Om Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Om du vill skicka segmentdata till Adobe Campaign måste du först [ansluta målet](#connect-destination) i kunddataplattformen i realtid och sedan [konfigurera en dataimport](#import-data-into-campaign) från lagringsplatsen till Adobe Campaign.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [för](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Koppla mål {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du Adobe Campaign och sedan **[!UICONTROL Connect destination]**.

![Anslut till Adobes kampanj](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

I arbetsflödet för anslutningsmål väljer du **[!UICONTROL Connection type]** lagringsplats. För Adobe Campaign kan du välja mellan **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** och **[!UICONTROL SFTP with SSH Key]**. Fyll i informationen nedan, beroende på vilken typ av anslutning du har, och välj sedan **[!UICONTROL Connect]**.

![Konfigurera kampanjguiden](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- För **[!UICONTROL Amazon S3]** anslutningar måste du ange ditt ID för åtkomstnyckel och hemlig åtkomstnyckel.
- För **[!UICONTROL SFTP with Password]** anslutningar måste du ange domän, port, användarnamn och lösenord.
- För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange domän, port, användarnamn och SSH-nyckel.

Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till de exporterade filerna under **[!UICONTROL Key]** avsnittet. Observera att den här offentliga nyckeln **måste** skrivas som en Base64-kodad sträng.

![Fyll i Campaign-information](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Fyll i **[!UICONTROL Basic Information]** den relevanta informationen för destinationen enligt nedan:
- **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
- **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
- **[!UICONTROL Bucket Name]**: *För S3-anslutningar*. Ange platsen för S3-bucket där CDP i realtid ska placera dina exportdata som CSV- eller tabbavgränsade filer.
- **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där CDP i realtid ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
- **[!UICONTROL File Format]**: **CSV** eller **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.

![Grundläggande information om kampanj](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Klicka **[!UICONTROL Create]** när du har fyllt i fälten ovan. Målet är nu anslutet och du kan [aktivera segment](../../ui/activate-destinations.md) till målet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) .

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till Adobe Campaign-målet rekommenderar vi att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes) i dokumentationen för e-postmarknadsföringsmål.

## Exporterade data {#exported-data}

För [!DNL Adobe Campaign] mål skapar CDP i realtid en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Konfigurera dataimport till Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Tänk på lagringsgränserna för SFTP, lagringsgränserna för databaser och de aktiva profilgränserna enligt ditt Adobe Campaign-avtal när du utför den här integreringen.
>- Du måste schemalägga, importera och mappa exporterade segment i Adobe Campaign med hjälp av [!DNL Campaign] arbetsflöden. Mer information finns i [Konfigurera en återkommande import](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) i Adobe Campaign-dokumentationen.



När du har anslutit CDP i realtid till din [!DNL Amazon S3] eller SFTP-lagringen måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i [Importera data](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) i Adobe Campaign-dokumentationen.