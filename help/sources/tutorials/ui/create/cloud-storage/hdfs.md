---
keywords: Experience Platform;hem;populära ämnen;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Skapa en Apache HDFS Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Apache Hadoop Distributed File System med hjälp av Adobe Experience Platform användargränssnitt.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Skapa en [!DNL Apache] HDFS-källanslutning i användargränssnittet

>[!NOTE]
>
>HDFS-anslutningen [!DNL Apache] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

Source-anslutningar i [!DNL Adobe Experience Platform] ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en [!DNL Apache Hadoop Distributed File System]-källanslutning (kallas nedan HDFS) med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Experience Platform]:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig HDFS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera HDFS-källkopplingen måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | URL:en definierar de auth-parametrar som krävs för att ansluta till HDFS anonymt. Mer information om hur du hämtar det här värdet finns i följande dokument om [HTTPS-autentisering för HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Anslut ditt HDFS-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt HDFS-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Apache HDFS]** under kategorin **[!UICONTROL Cloud storage]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny HDFS-anslutning.

![katalog](../../../../images/tutorials/create/hdfs/catalog.png)

Sidan **[!UICONTROL Connect to HDFS]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina HDFS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/hdfs/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det HDFS-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/hdfs/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt HDFS-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till  [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md).
