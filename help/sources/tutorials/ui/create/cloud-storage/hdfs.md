---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Apache HDFS-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Skapa en [!DNL Apache] HDFS-källanslutning i användargränssnittet

>[!NOTE]
>HDFS- [!DNL Apache] kontakten är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i [!DNL Adobe Experience Platform] ger möjlighet att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en [!DNL Apache Hadoop Distributed File System] (nedan kallad HDFS) källanslutning med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

- [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig HDFS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera HDFS-källkopplingen måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | URL:en definierar de auth-parametrar som krävs för att ansluta till HDFS anonymt. Mer information om hur du hämtar det här värdet finns i följande dokument om [HTTPS-autentisering för HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Anslut ditt HDFS-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt HDFS-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Cloud storage]** kategorin **[!UICONTROL Apache HDFS]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny HDFS-anslutning.

![katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Sidan visas **[!UICONTROL Connect to HDFS]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina HDFS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/hdfs/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det HDFS-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/hdfs/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt HDFS-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).