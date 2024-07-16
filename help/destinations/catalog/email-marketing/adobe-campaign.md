---
keywords: e-post;E-post;e-post;e-postmål;adobe-kampanj;kampanj
title: Adobe Campaign
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# Adobe Campaign

## Översikt {#overview}

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Mer information finns i [Kom igång med Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Om du vill skicka målgruppsdata till Adobe Campaign måste du först [ansluta målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-campaign) från din lagringsplats till Adobe Campaign.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänsten](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall i tillåtelselista.

Se [IP-adressen tillåtelselista för SFTP-mål](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser i Adobe i tillåtelselista.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

Adobe Campaign stöder följande anslutningstyper:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* För **[!UICONTROL Amazon S3]**-anslutningar måste du ange [!UICONTROL Access Key ID] och [!UICONTROL Secret Access Key].
* För **[!UICONTROL SFTP with Password]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL Password].
* För **[!UICONTROL SFTP with SSH Key]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL SSH Key].
* För **[!UICONTROL Azure Blob]** anslutningar måste du ange en anslutningssträng.
* Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under avsnittet **[!UICONTROL Key]**. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.
* **[!UICONTROL Name]**: Välj ett relevant namn för målet.
* **[!UICONTROL Description]**: Ange en beskrivning för målet.
* **[!UICONTROL Bucket Name]**: *För S3-anslutningar*. Ange platsen för din S3-bucket där [!DNL Platform] ska placera dina exportdata som CSV-filer.
* **[!UICONTROL Folder Path]**: Ange sökvägen på lagringsplatsen där [!DNL Platform] ska placera dina exportdata som CSV-filer.
* **[!UICONTROL Container]**: *För blobanslutningar*. Behållaren som innehåller blobben som mappsökvägen finns i.
* **[!UICONTROL File Format]**: Välj **CSV** om du vill exportera CSV-filer till lagringsplatsen.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}


Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Målattribut {#destination-attributes}

När du aktiverar målgrupper till det här målet rekommenderar Adobe att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Bästa praxis när du aktiverar målgrupper till e-postmarknadsföringsmål](overview.md#best-practices).

## Exporterade data {#exported-data}

För [!DNL Adobe Campaign] mål skapar [!DNL Platform] en `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i avsnittet [Verifiera målgruppsaktivering](../../ui/activate-batch-profile-destinations.md#verify) i självstudiekursen om målgruppsaktivering.

## Konfigurera dataimport till Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tänk på lagringsgränserna för [!DNL SFTP], lagringsgränserna för databaser och begränsningar för den aktiva profilen enligt ditt Adobe Campaign-kontrakt när du utför den här integreringen.
>* Du måste schemalägga, importera och mappa dina exporterade segment i Adobe Campaign med [!DNL Campaign] arbetsflöden. Se [Konfigurera en återkommande import](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) i Adobe Campaign Classic-dokumentationen och [Om datahanteringsaktiviteter](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) i Adobe Campaign Standard-dokumentationen.
>* Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].

När du har anslutit [!DNL Platform] till ditt [!DNL Amazon S3]- eller [!DNL Azure Blob]-lagringsutrymme måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i följande Adobe Campaign-dokumentationssidor:
* [Kom igång med import och export av data](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) och [Inläsning av data (fil)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) i Adobe Campaign Classic-dokumentationen.
* [Kom igång med processer och datahantering](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) och [Läs in fil](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) i Adobe Campaign Standard-dokumentationen.
