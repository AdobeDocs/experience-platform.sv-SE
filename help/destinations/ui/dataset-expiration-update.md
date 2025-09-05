---
title: Utöka datauppsättningsexportscheman för dataflöden som skapats före november 2024
description: Lär dig hur du förlänger exportschemat för dataexportdataflöden som skapats före november 2024 och som slutar fungera den 1 september 2025.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 0da592dd2846ed0f1eeb31102842c8895cac6952
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Utöka datauppsättningsexportscheman för dataflöden som skapats före november 2024

>[!IMPORTANT]
>
>**Åtgärd krävs**: Om din organisation har [dataflöden för dataexport](export-datasets.md) som skapats före november 2024 kommer dessa dataflöden att sluta fungera den 1 september 2025. I den här guiden beskrivs hur du förlänger exportschemat efter detta datum för de dataflöden som du vill behålla.

## Översikt {#overview}

I [september 2024-utgåvan av Experience Platform](/help/release-notes/2024/september-2024.md#destinations) introducerade Adobe ett standardslutdatum på **1 maj 2025** för alla datauppsättningsexportdataflöden som skapades före september 2024-utgåvan.

**Detta datum har sedan dess uppdaterats till 1 september 2025** för alla datauppsättningsexportdataflöden som skapades **före november 2024**.

Datauppsättningsexportdataflöden som skapats före november 2024 avbryter dataexporten den **1 september 2025** om du inte förlänger deras förfallodatum manuellt.

Om du behöver dataflödena för att kunna fortsätta exportera data efter den **1 september 2025** måste du utöka deras scheman för varje mål som du exporterar datauppsättningar till genom att följa stegen i den här handboken.

## Berörda destinationer {#affected-destinations}

Din organisation kan ha aktiva datauppsättningsexportdataflöden som skickar data till de mål som anges nedan. Följ stegen i de följande avsnitten och se på genomsökningsvideon för att lära dig hur du identifierar vilka datauppsättningar som ska upphöra att gälla.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Videosjälvstudiekurs {#video}

I videon nedan visas steg för steg hur du identifierar datauppsättningsexporter med kommande slutdatum och utökar exportschemat för de dataflöden du vill behålla.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Steg 1: Identifiera berörda dataflöden {#identify-dataflows}

Innan du förlänger exportschemat för datauppsättningsexportdataflödena måste du först identifiera vilka dataflöden som påverkas av det kommande förfallodatumet. Följ stegen nedan för att hitta dataflöden som kräver åtgärder.

1. Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i Experience Platform-gränssnittet.
2. Välj **[!UICONTROL Activate]** på ett mål som har aktiva datauppsättningsexportdataflöden.

   >[!TIP]
   >
   >Använd filtret **[!UICONTROL Data Types]** till vänster om katalogen för att filtrera tillgängliga mål efter **[!UICONTROL Datasets]**.

3. Välj datatypen **[!UICONTROL Datasets]** om du bara vill visa dataflödena med datauppsättningsexporter.
   ![Skärmbild som visar hur du filtrerar dataflöden efter datatyp.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Markera kolumnrubriken **[!UICONTROL Created]** och välj **[!UICONTROL Sort Ascending]** om du vill visa äldre dataflöden.
   ![Skärmbild som visar hur dataflöden sorteras stigande.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identifiera vilka av dataflödena som skapades före november 2024 som du vill behålla.

## Steg 2: Få åtkomst till arbetsflödet för exportdataset {#access-workflow}

För varje dataflöde som du vill behålla måste du ha tillgång till arbetsflödet för exportdatamängder för att kunna ändra schemat.

1. Markera dataflödets namn i kolumnen **[!UICONTROL Name]**. Du kommer nu till sidan **[!UICONTROL Dataflow runs]**.
2. På den här sidan väljer du alternativet **[!UICONTROL Export datasets]**.
   ![Skärmbild som visar alternativet för exportdatauppsättningar på körningssidan för dataflöde.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Välj **[!UICONTROL Select datasets]** på sidan **[!UICONTROL Next]**. Du behöver inte lägga till några nya datauppsättningar i dataflödet.
4. Detta tar dig till sidan **[!UICONTROL Scheduling]** där du också kan se ett meddelande som informerar dig om att datauppsättningens exportförfallodatum har passerats.
   ![Datauppsättningsexportdataflöden med förfallomeddelande](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Steg 3: Utöka exportschemat {#extend-export-schedule}

Nu kan du ändra exportschemat så att det fortsätter efter 1 september 2025.

1. Välj **[!UICONTROL Edit schedule]**.
   ![Skärmbild av schemaläggningssteget med knappen Redigera schema.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Välj ett nytt exportschema och välj sedan **[!UICONTROL Save]**.
   ![Skärmbild av schemaläggningssteget med schemaläggningsalternativ.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Mer information om hur du konfigurerar datauppets exportscheman finns i [dokumentationen för datauppsättningsexport](export-datasets.md#scheduling).

## Vad händer om jag missar den 1 september 2025? {#missed-deadline}

Om datauppsättningsexportflödena löpte ut den 1 september 2025 och du fortfarande vill utöka dem följer du stegen i avsnitten ovan för att utöka deras schema.

Om du utökar exportschemat inom 30 dagar (eller mindre om [time-to-live-uppsättningen för den exporterade datamängden](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md) är mindre än 30 dagar) kan du fortfarande få en återfyllnad av data som inte exporterades mellan den 1 september och det datum du återaktiverade exporten. När du anger en ny sluttid blir *inte* en fullständig filexport först. I stället fortsätter exporten stegvis från den plats där den slutade den 1 september.