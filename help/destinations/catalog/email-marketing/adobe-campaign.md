---
keywords: e-post;E-post;e-post;e-postmål;adobe-kampanj;kampanj
title: Adobe Campaign-anslutning
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 47e0dfb59edca58e205cb478e9ee624659753ab9
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Adobe Campaign-anslutning

## Översikt {#overview}

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Se [Kom igång med Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) för mer information.

Om du vill skicka segmentdata till Adobe Campaign måste du först [ansluta till målet](#connect-destination) i Adobe Experience Platform, och [konfigurera en dataimport](#import-data-into-campaign) från lagringsplatsen till Adobe Campaign.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adress tillåtelselista för SFTP-mål](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

Adobe Campaign stöder följande anslutningstyper:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* För **[!UICONTROL Amazon S3]** anslutningar måste du ange [!UICONTROL Access Key ID] och [!UICONTROL Secret Access Key].
* För **[!UICONTROL SFTP with Password]** anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username]och [!UICONTROL Password].
* För **[!UICONTROL SFTP with SSH Key]** anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username]och [!UICONTROL SSH Key].
* För **[!UICONTROL Azure Blob]** måste du ange en anslutningssträng.
* Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under **[!UICONTROL Key]** -avsnitt. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.
* **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
* **[!UICONTROL Bucket Name]**: *För S3-anslutningar*. Ange platsen för din S3-bucket där [!DNL Platform] sparar exportdata som CSV-filer.
* **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där [!DNL Platform] sparar exportdata som CSV-filer.
* **[!UICONTROL Container]**: *För blobanslutningar*. Behållaren som innehåller blobben som mappsökvägen finns i.
* **[!UICONTROL File Format]**: Välj **CSV** för att exportera CSV-filer till lagringsplatsen.

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

För [!DNL Adobe Campaign] destinationer, [!DNL Platform] skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [verifiera aktivering av segment](../../ui/activate-batch-profile-destinations.md#verify) i segmentaktiveringssjälvstudiekursen.

## Konfigurera dataimport till Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Kom ihåg [!DNL SFTP] lagringsbegränsningar, lagringsgränser för databaser och begränsningar för aktiv profil enligt ditt Adobe Campaign-kontrakt när denna integrering utförs.
>* Du måste schemalägga, importera och mappa exporterade segment i Adobe Campaign med [!DNL Campaign] arbetsflöden. Se [Konfigurera en återkommande import](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) i Adobe Campaign Classic dokumentation och [Om datahanteringsaktiviteter](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) i Adobe Campaign Standard-dokumentationen.
>* Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].


Efter anslutning [!DNL Platform] till [!DNL Amazon S3] eller [!DNL Azure Blob] måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i följande Adobe Campaign-dokumentationssidor:
* [Kom igång med import och export av data](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) och [Inläsning av data (fil)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) i Adobe Campaign Classic-dokumentationen.
* [Kom igång med processer och datahantering](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) och [Läs in fil](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) i Adobe Campaign Standard-dokumentationen.
