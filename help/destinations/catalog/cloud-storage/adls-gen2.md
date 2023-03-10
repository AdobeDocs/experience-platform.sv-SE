---
title: (Beta) Azure Data Lake Storage Gen2-anslutning
description: Lär dig hur du ansluter till Azure Data Lake Storage Gen2 för att aktivera segment och exportera datauppsättningar.
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 010818b56154067402a7cd66f489dd2080142e53
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# (Beta) [!DNL Azure Data Lake Storage Gen2] anslutning

>[!IMPORTANT]
>
>Den här destinationen finns för närvarande i betaversionen och är endast tillgänglig för ett begränsat antal kunder. Om du vill begära åtkomst till [!DNL Azure Data Lake Storage Gen2] kontakta din Adobe-representant och uppge [!DNL Organization ID].

## Översikt {#overview}

Läs den här sidan om du vill veta mer om hur du skapar en utgående liveanslutning till [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) Data Lake för att regelbundet exportera datafiler från Experience Platform.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du väljer på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](/help/destinations/ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL URL]**: Slutpunkten för [!DNL Azure Data Lake Storage Gen2]. Slutpunktsmönstret är: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]**: Klientinformationen som innehåller ditt program.
* **[!UICONTROL Service principal ID]**: Programmets klient-ID.
* **[!UICONTROL Service principal key]**: Programmets nyckel.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

   ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: väljer du vilket format Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Schemaläggning {#scheduling}

I **[!UICONTROL Scheduling]** kan du [konfigurera exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för [!DNL Azure Data Lake Storage Gen2] mål och du kan också [konfigurera namnet på de exporterade filerna](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om att aktivera gruppdestinationer.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i [självstudiekurs om hur du exporterar datauppsättningar](/help/destinations/ui/export-datasets.md).

## Validera slutförd dataexport {#exported-data}

Kontrollera dina [!DNL Azure Data Lake Storage Gen2] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.
