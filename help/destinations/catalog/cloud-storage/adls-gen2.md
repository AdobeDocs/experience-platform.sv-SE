---
title: Azure Data Lake Storage Gen2-anslutning
description: Lär dig hur du ansluter till Azure Data Lake Storage Gen2 för att aktivera målgrupper och exportera datamängder.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# [!DNL Azure Data Lake Storage Gen2]-anslutning

## Översikt {#overview}

Läs den här sidan om du vill veta mer om hur du skapar en utgående liveanslutning till din [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])-datavy för att regelbundet exportera datafiler från Experience Platform.

## Anslut till ditt [!DNL ADLS Gen2]-lagringsutrymme via API eller användargränssnittet {#connect-api-or-ui}

* Om du vill ansluta till lagringsplatsen [!DNL ADLS Gen2] med Experience Platform användargränssnitt läser du avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Om du vill ansluta till din [!DNL ADLS Gen2]-lagringsplats programmatiskt läser du [Aktivera målgrupper till filbaserade mål med hjälp av API-självstudiekursen för Flow-tjänsten](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment, tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här [exporterar du datauppsättningar med Experience Platform användargränssnitt](/help/destinations/ui/export-datasets.md).
* Så här [exporterar du datauppsättningar programmatiskt med API:t för Flow Service ](/help/destinations/api/export-datasets.md).

## Filformat för exporterade data {#file-format}

När du exporterar *målgruppsdata* skapar Experience Platform en `.csv` -, `parquet` - eller `.json` -fil på den angivna lagringsplatsen. Mer information om filerna finns i avsnittet [Filformat som stöds för export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) i självstudiekursen om målgruppsaktivering.

När du exporterar *datauppsättningar* skapar Experience Platform en `.parquet`- eller `.json`-fil på den lagringsplats som du angav. Mer information om filerna finns i avsnittet [Verifiera lyckad datauppsättningsexport](../../ui/export-datasets.md#verify) i självstudiekursen om exportdatamängder.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](/help/destinations/ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!UICONTROL URL]**: Slutpunkten för [!DNL Azure Data Lake Storage Gen2]. Slutpunktsmönstret är: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]**: Klientinformationen som innehåller ditt program.
* **[!UICONTROL Service principal ID]**: Programmets klient-ID.
* **[!UICONTROL Service principal key]**: Programmets nyckel.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer alternativet [!UICONTROL CSV] kan du även [konfigurera filformateringsalternativen](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat. Manifestet har fått ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [Dataflödet kör](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Den exporterade filens storlek i byte.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemaläggning {#scheduling}

I steget **[!UICONTROL Scheduling]** kan du [ställa in exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för ditt [!DNL Azure Data Lake Storage Gen2]-mål och du kan även [konfigurera namnet på dina exporterade filer](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I steget **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om aktivering av gruppmål.

## Validera slutförd dataexport {#exported-data}

Kontrollera [!DNL Azure Data Lake Storage Gen2]-lagringen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats.
