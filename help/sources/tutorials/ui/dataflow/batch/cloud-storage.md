---
keywords: Experience Platform;home;popular topics;dataflow;Dataflow
solution: Experience Platform
title: Configure a Dataflow for a Cloud Storage Batch Connector in the UI
topic-legacy: overview
type: Tutorial
description: Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. This tutorial provides steps to configure a new dataflow using your cloud storage account.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 10f04044e970158131677e0c630edf761d4577bd
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 0%

---

# Konfigurera ett dataflöde för en batchanslutning till molnlagring i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en [!DNL Platform] datauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med ditt molnlagringskonto.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schema Editor tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Provides a unified, real-time consumer profile based on aggregated data from multiple sources.

Den här självstudiekursen kräver dessutom att du har ett etablerat molnlagringskonto. En lista med självstudiekurser för att skapa olika molnlagringskonton i användargränssnittet finns i [översikt över källanslutningar](../../../../home.md).

### Filformat som stöds

[!DNL Experience Platform] supports the following file formats to be ingested from external storages:

* Avgränsaravgränsade värden (DSV): Alla värden med ett tecken kan användas som avgränsare för DSV-formaterade datafiler.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatted data files must be XDM-compliant.
* [!DNL Apache Parquet]: Parquet-formaterade datafiler måste vara XDM-kompatibla.
* Komprimerade filer: JSON och avgränsade filer kan komprimeras som: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`och `tar`.

## Select data

After creating your cloud storage account, the **[!UICONTROL Select data]** step appears, providing an interface for you to explore your cloud storage file hierarchy.

* Den vänstra delen av gränssnittet är en katalogwebbläsare som visar lagringsfiler och kataloger i molnet.
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en kompatibel fil.

![gränssnitt](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

Om du väljer en mapp i listan kan du gå igenom mapphierarkin till djupare mappar. Du kan markera en mapp om du vill importera alla filer i mappen rekursivt. När du importerar en hel mapp måste du se till att alla filer i mappen delar samma schema.

När du har markerat en kompatibel fil eller mapp väljer du motsvarande dataformat på menyn [!UICONTROL Select data format] nedrullningsbar meny.

I följande tabell visas rätt dataformat för de filtyper som stöds:

| Filtyp | Dataformat |
| --- | --- |
| CSV | [!UICONTROL Delimited] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

Välj **[!UICONTROL JSON]** och vänta några sekunder på att förhandsvisningsgränssnittet ska fyllas i.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>Till skillnad från filtyperna separerad och JSON är Parquet-formaterade filer inte tillgängliga för förhandsgranskning.

I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Som standard visas den första filen i den markerade mappen i förhandsvisningsgränssnittet.

Om du vill förhandsgranska en annan fil markerar du förhandsvisningsikonen bredvid namnet på filen som du vill inspektera.

![standardförhandsvisning](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

När du har inspekterat innehållet och strukturen för filerna i mappen väljer du **[!UICONTROL Next]** om du vill importera alla filer i mappen rekursivt.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Om du föredrar att välja en viss fil markerar du den fil som du vill importera och väljer sedan **[!UICONTROL Next]**.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Set a custom delimiter for delimited files

You can set a custom delimiter when ingesting delimited files. Select the **[!UICONTROL Delimiter]** option and then select a delimiter from the dropdown menu. The menu displays the most frequently used options for delimiters, including a comma (`,`), a tab (`\t`), and a pipe (`|`). Om du föredrar att använda en egen avgränsare väljer du **[!UICONTROL Custom]** och ange en avgränsare med ett tecken i popup-indatafältet.

När du har valt dataformat och angett avgränsare väljer du **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Infoga komprimerade filer

Du kan importera komprimerade JSON-filer eller avgränsade filer genom att ange deras komprimeringstyp.

I [!UICONTROL Select data] markerar du en komprimerad fil för inhämtning och väljer sedan lämplig filtyp och om den är XDM-kompatibel eller inte. Nästa, välj **[!UICONTROL Compression type]** och välj sedan lämplig komprimerad filtyp för källdata.

Med en komprimerad filtyp identifierad väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## Mappa datafält till ett XDM-schema

The **[!UICONTROL Mapping]** visas med ett interaktivt gränssnitt för att mappa källdata till [!DNL Platform] datauppsättning. Källfiler som är formaterade i Parquet måste vara XDM-kompatibla och kräver inte att du konfigurerar mappningen manuellt, medan CSV-filer kräver att du uttryckligen konfigurerar mappningen, men tillåter att du väljer vilka källdatafält som ska mappas. Om JSON-filer markeras som XDM-klagomål krävs ingen manuell konfiguration. Om den inte är markerad som XDM-kompatibel måste du explicit konfigurera mappningen.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** väljer du datamängdikonen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

The **[!UICONTROL Select dataset]** visas. Find the dataset you you wish to use, select it, then click **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Använd en ny datauppsättning**

To ingest data into a new dataset, select **[!UICONTROL New dataset]** and enter a name and description for the dataset in the fields provided. Om du vill lägga till ett schema kan du ange ett befintligt schemanamn i **[!UICONTROL Select schema]** -dialogrutan. Du kan också välja **[!UICONTROL Schema advanced search]** för att söka efter ett lämpligt schema.

Under det här steget kan du aktivera datauppsättningen för [!DNL Real-time Customer Profile] och skapa en helhetsbild av ett företags attribut och beteenden. Data från alla aktiverade datauppsättningar inkluderas i [!DNL Profile] och ändringarna tillämpas när du sparar dataflödet.

Växla **[!UICONTROL Profile dataset]** för att aktivera måldatauppsättningen för [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

The **[!UICONTROL Select schema]** visas. Välj det schema som du vill tillämpa på den nya datauppsättningen och välj sedan **[!UICONTROL Done]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om mappningsfunktioner och beräkningsfält finns i [Handbok för dataprefixfunktioner](../../../../../data-prep/functions.md) eller [guide för beräknade fält](../../../../../data-prep/calculated-fields.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

För JSON-filer kan du, förutom att direkt mappa fält till andra fält, direkt mappa objekt till andra objekt och arrayer till andra arrayer. Du kan också förhandsgranska och mappa komplexa datatyper som arrayer i JSON-filer med hjälp av en koppling för molnlagringskälla.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Observera att du inte kan mappa mellan olika typer. Du kan till exempel inte mappa ett objekt till en array eller ett fält till ett objekt.

>[!TIP]
>
>Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. You can manually adjust mapping rules to suit your use cases.

Select **[!UICONTROL Preview data]** to see mapping results of up to 100 rows of sample data from the selected dataset.

Under förhandsgranskningen prioriteras identitetskolumnen som det första fältet, eftersom det är den nyckelinformation som krävs vid validering av mappningsresultat.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

När källdata har mappats väljer du **[!UICONTROL Close]**.

## Schedule ingestion runs

The **[!UICONTROL Scheduling]** step appears, allowing you to configure an ingestion schedule to automatically ingest the selected source data using the configured mappings. I följande tabell visas de olika konfigurerbara fälten för schemaläggning:

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Valbara frekvenser inkluderar `Once`, `Minute`, `Hour`, `Day`och `Week`. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. |
| Starttid | En UTC-tidsstämpel som anger när det allra första intaget är inställt. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. If **[!UICONTROL Backfill]** är aktiverat kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. If **[!UICONTROL Backfill]** är inaktiverat, kommer endast de filer som läses in mellan den första importkörningen och starttiden att importeras. Filer som lästs in före starttiden importeras inte. |

Dataflöden är utformade för att automatiskt importera data enligt schema. Börja med att välja intagsfrekvens. Ange sedan intervallet för att ange perioden mellan två flödeskörningar. Intervallets värde måste vara ett heltal som inte är noll och måste vara större än eller lika med 15.

Om du vill ange starttid för intaget justerar du datumet och tiden som visas i rutan för starttid. Du kan också välja kalenderikonen för att redigera starttidsvärdet. Starttiden måste vara större än eller lika med den aktuella tiden i UTC.

Ange värden för schemat och välj **[!UICONTROL Next]**.

>[!NOTE]
>
>För batchimport väljer varje efterföljande dataflöde filer som ska importeras från källan baserat på deras **senast ändrad** tidsstämpel. Detta innebär att gruppdataflöden hämtar valda filer från källan som antingen är nya eller har ändrats sedan den senaste dataflödeskörningen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Konfigurera ett dataflöde för engångsbruk

Om du vill ställa in engångsinmatning väljer du den nedrullningsbara frekvenspilen och väljer **[!UICONTROL Once]**. Du kan fortsätta att redigera ett dataflöde för att få en engångsfrekvens så länge som starttiden är kvar i framtiden. När starttiden har passerat kan engångsfrekvensvärdet inte längre redigeras. **[!UICONTROL Interval]** och **[!UICONTROL Backfill]** är inte synliga när du ställer in ett dataflöde för engångsinmatning.

>[!IMPORTANT]
>
>Vi rekommenderar att du schemalägger dataflödet för engångsbruk när du använder [FTP-anslutning](../../../../connectors/cloud-storage/ftp.md).

När du har angett lämpliga värden för schemat väljer du **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Ange information om dataflöde

The **[!UICONTROL Dataflow detail]** visas så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Under den här processen kan du även aktivera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**. Aktivering **[!UICONTROL Partial ingestion]** ger möjlighet att importera data som innehåller fel, upp till ett visst tröskelvärde som du kan ange. Aktivering **[!UICONTROL Error diagnostics]** ger information om felaktiga data som batchas separat. Mer information finns i [partiell batchingång - översikt](../../../../../ingestion/batch-ingestion/partial.md).

Ange värden för dataflödet och välj **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Granska ditt dataflöde

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
* **[!UICONTROL Scheduling]**: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** så att dataflödet kan skapas.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen om [övervaka konton och dataflöden i användargränssnittet](../../monitor.md).

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med **[!UICONTROL Delete]** finns i **[!UICONTROL Dataflows]** arbetsyta. Mer information om hur du tar bort dataflöden finns i självstudiekursen om [ta bort dataflöden i användargränssnittet](../../delete.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta in data från en extern molnlagring och fått insikter om att övervaka datauppsättningar. Om du vill veta mer om hur du skapar dataflöden kan du komplettera din inlärning genom att titta på videon nedan. Dessutom kan inkommande data nu användas av underordnade [!DNL Platform] tjänster som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

* [[!DNL Real-time Customer Profile] översikt](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> The [!DNL Platform] Gränssnittet som visas i följande video är inaktuellt. Läs dokumentationen ovan för de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

When a dataflow is created, it immediately becomes active and ingests data according to the schedule it was given. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Within the **[!UICONTROL Sources]** workspace, click the **[!UICONTROL Browse]** tab. Klicka sedan på namnet på kontot som är associerat med det aktiva dataflödet som du vill inaktivera.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

The **[!UICONTROL Source activity]** visas. Välj det aktiva dataflödet i listan för att öppna dess **[!UICONTROL Properties]** kolumn till höger på skärmen som innehåller en **[!UICONTROL Enabled]** växlingsknapp. Click the toggle to disable the dataflow. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Aktivera inkommande data för [!DNL Profile] population

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-time Customer Profile] data. Mer information om hur du fyller i [!DNL Real-time Customer Profile] data, se självstudiekursen om [Profilpopulation](../../profile.md).
