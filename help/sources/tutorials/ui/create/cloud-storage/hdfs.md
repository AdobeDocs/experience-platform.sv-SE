---
keywords: Experience Platform;hem;populära ämnen;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Skapa en källanslutning för Apache HDFS i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Apache Hadoop Distributed File System med hjälp av Adobe Experience Platform användargränssnitt.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Skapa en [!DNL Apache] HDFS-källanslutning i användargränssnittet

>[!NOTE]
>
>The [!DNL Apache] HDFS-kontakten är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Källkopplingar i [!DNL Adobe Experience Platform] göra det möjligt att importera externt källdata på schemalagd basis. Den här självstudiekursen innehåller steg för hur du autentiserar en [!DNL Apache Hadoop Distributed File System] (nedan kallat &quot;HDFS&quot;)-källkontakt med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig HDFS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen på [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera HDFS-källkopplingen måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | URL:en definierar de auth-parametrar som krävs för att ansluta till HDFS anonymt. Mer information om hur du får fram det här värdet finns i följande dokument på [HTTPS-autentisering för HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Anslut ditt HDFS-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt HDFS-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Cloud storage]** kategori, välj **[!UICONTROL Apache HDFS]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny HDFS-anslutning.

![katalog](../../../../images/tutorials/create/hdfs/catalog.png)

The **[!UICONTROL Connect to HDFS]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina HDFS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/hdfs/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det HDFS-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/hdfs/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt HDFS-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
