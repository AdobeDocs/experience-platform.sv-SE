---
keywords: e-post;E-post;e-post;e-postmål;adobe-kampanj;kampanj
title: Adobe Campaign-anslutning
description: Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---

# Adobe Campaign-anslutning

## Översikt {#overview}

Adobe Campaign är en uppsättning lösningar som hjälper er att personalisera och leverera kampanjer i alla kanaler, både online och offline. Mer information finns i [Kom igång med Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Om du vill skicka segmentdata till Adobe Campaign måste du först [ansluta målet](#connect-destination) i Adobe Experience Platform och sedan [konfigurera en dataimport](#import-data-into-campaign) från lagringsplatsen till Adobe Campaign.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt i  **[!UICONTROL Select attributes]** steget i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

## IP-adress tillåtelselista {#allow-list}

När du konfigurerar e-postmarknadsföringsmål med SFTP-lagring rekommenderar Adobe att du lägger till vissa IP-intervall till tillåtelselista.

Se [IP-adressen tillåtelselista för molnlagringsdestinationer](../cloud-storage/ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i tillåtelselista.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

Adobe Campaign stöder följande anslutningstyper:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* För **[!UICONTROL Amazon S3]**-anslutningar måste du ange [!UICONTROL Access Key ID] och [!UICONTROL Secret Access Key].
* För **[!UICONTROL SFTP with Password]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL Password].
* För **[!UICONTROL SFTP with SSH Key]**-anslutningar måste du ange [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] och [!UICONTROL SSH Key].
* För **[!UICONTROL Azure Blob]**-anslutningar måste du ange en anslutningssträng.
* Du kan även bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering med PGP/GPG till dina exporterade filer under **[!UICONTROL Key]**-avsnittet. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.
* **[!UICONTROL Name]**: Välj ett relevant namn för destinationen.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen.
* **[!UICONTROL Bucket Name]**:  *För S3-anslutningar*. Ange platsen för S3-bucket där [!DNL Platform] ska placera dina exportdata som CSV-filer eller tabbavgränsade filer.
* **[!UICONTROL Folder Path]**: Ange sökvägen till lagringsplatsen där dina exportdata  [!DNL Platform] ska lagras som CSV-filer eller tabbavgränsade filer.
* **[!UICONTROL Container]**:  *För Blob-anslutningar*. Behållaren som innehåller blobben som mappsökvägen finns i.
* **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Välj vilket filformat som ska exporteras till lagringsplatsen.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till mål.

## Målattribut {#destination-attributes}

När du [aktiverar segment](../../ui/activate-destinations.md) till det här målet rekommenderar Adobe att du väljer en unik identifierare från ditt [unionsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet. Mer information finns i [Välja vilka schemafält som ska användas som målattribut i de exporterade filerna](./overview.md#destination-attributes).

## Exporterade data {#exported-data}

För [!DNL Adobe Campaign]-mål skapar [!DNL Platform] en tabbavgränsad `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## Konfigurera dataimport till Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tänk på lagringsgränserna för [!DNL SFTP], lagringsgränserna för databaser och de aktiva profilgränserna enligt ditt Adobe Campaign-kontrakt när du utför den här integreringen.
>* Du måste schemalägga, importera och mappa dina exporterade segment i Adobe Campaign med hjälp av [!DNL Campaign]-arbetsflöden. Se [Konfigurera en återkommande import](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) i Adobe Campaign Classic-dokumentationen och [Om datahanteringsaktiviteter](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) i Adobe Campaign Standard-dokumentationen.
>* Den metod som rekommenderas för att skicka data till Adobe Campaign är via [!DNL Amazon S3] eller [!DNL Azure Blob].


När du har anslutit [!DNL Platform] till ditt [!DNL Amazon S3]- eller [!DNL Azure Blob]-lagringsutrymme måste du konfigurera dataimporten från din lagringsplats till Adobe Campaign. Mer information om hur du gör detta finns i följande Adobe Campaign-dokumentationssidor:
* [Kom igång med import och ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) export av data och  [datainläsning (fil)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) i Adobe Campaign Classic-dokumentationen.
* [Kom igång med processer och ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) datahantering och  [Läs in ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) fil i Adobe Campaign Standard-dokumentationen.
