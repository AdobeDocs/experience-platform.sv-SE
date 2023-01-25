---
description: Lär dig hur du konfigurerar filformateringsalternativ när du aktiverar data till filbaserade mål
title: (Beta) Konfigurera filformateringsalternativ för filbaserade mål
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 14ce4a11f53ef24b3008b3f775cc926d05ea8f8e
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# (Beta) Konfigurera filformateringsalternativ för filbaserade mål

>[!IMPORTANT]
>
>The **[!UICONTROL File formatting options]** i Adobe Experience Platform finns i betaversionen. Dokumentationen och funktionerna kan komma att ändras.
>Kontakta din Adobe-representant för att få tillgång till den här funktionen.
> 
>Filformateringsalternativen som beskrivs i det här dokumentet är för närvarande bara tillgängliga för CSV-filer.

Du kan välja att konfigurera olika filformateringsalternativ för de exporterade filerna när du [koppla](/help/destinations/ui/connect-destination.md) till ett filbaserat mål, som [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect), eller [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Du kan konfigurera olika filformateringsalternativ för exporterade filer med hjälp av användargränssnittet i Experience Platform. Du kan ändra flera egenskaper för de exporterade filerna så att de matchar kraven i filmottagningssystemet på din sida för att optimera läsningen och tolkningen av de filer som tas emot från Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Filformateringskonfiguration {#file-configuration}

Om du vill visa filformateringsalternativen startar du [ansluta till mål](/help/destinations/ui/connect-destination.md) arbetsflöde. Välj **Datatyp: Segment** och **Filtyp: CSV** för att visa de filformateringsinställningar som är tillgängliga för den exporterade filen `CSV` filer.

>[!IMPORTANT]
>
>Målet som du ansluter till kanske inte har alla dessa alternativ tillgängliga. Det är upp till målutvecklaren att avgöra vilka filformateringsalternativ som stöds i målet. Målutvecklaren kan avgöra vilka alternativ som är tillgängliga vid anslutning till målet. Obligatoriska alternativ är markerade med en asterisk i användargränssnittet för Experience Platform.
> 
>De nya molnlagringsmålen - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure-blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud-lagring](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - stöder för närvarande endast de sex CSV-alternativen som markeras nedan.

![Bild som visar några av de tillgängliga filformateringsalternativen.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Avgränsare {#delimiter}

Anger en avgränsare för varje fält och värde. Tillgängliga alternativ är:

* Colon `(:)`
* Komma `(,)`
* Pipe `(|)`
* Semikolon `(;)`
* Tabb `(\\t)`

### Citattecken

Anger ett enskilt tecken som används för att undvika citattecken där avgränsaren kan vara en del av värdet.

### Escape-tecken

Anger ett enskilt tecken som används för att undvika citattecken i ett redan citattecken.

### Tomt värde för utdata

Anger strängbeteckningen för ett tomt värde.

### Utdata för null-värde

Anger strängbeteckningen för ett null-värde i de exporterade filerna.

Exempelutdata med **[!UICONTROL null]** markerat: `male,NULL,TestLastName`
Exempelutdata med **&quot;&quot;** markerat: `male,"",TestLastName`
Exempelutdata med **[!UICONTROL Empty string]** markerat: `male,,TestLastName`

### Komprimeringsformat

Anger vilken komprimeringskodek som ska användas när data sparas i filen. De alternativ som stöds är GZIP och NONE.

### Kodning

*Visas inte i skärmbilden för användargränssnittet*. Anger kodning (teckenuppsättning) för sparade CSV-filer. Alternativen är UTF-8 eller UTF-16.

### Char to escape quote

*Visas inte i skärmbilden för användargränssnittet*. En flagga som anger om värden som innehåller citattecken alltid ska omslutas av citattecken.

Standard är att undvika alla värden som innehåller ett citattecken.

### Radavgränsare

*Visas inte i skärmbilden för användargränssnittet*. Definierar den radavgränsare som ska användas för skrivning. Maxlängden är 1 tecken.

### Ignorera inledande blanksteg

*Visas inte i skärmbilden för användargränssnittet*. En flagga som anger om inledande blanksteg från värden som exporteras ska hoppas över.

Exempelutdata med **[!UICONTROL True]** markerat: `"male","John","TestLastName"`
Exempelutdata med **[!UICONTROL False]** markerat: `" male","John","TestLastName"`

### Ignorera avslutande blanksteg

Visas inte på skärmbilden för användargränssnittet. En flagga som anger om efterföljande blanksteg från värden som exporteras ska hoppas över.

Exempelutdata med **[!UICONTROL True]** markerat: `"male","John","TestLastName"`
Exempelutdata med **[!UICONTROL False]** markerat: `"male ","John","TestLastName"`

### Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du konfigurerar alternativ för filexport för dina CSV-datafiler för att anpassa filinnehållet efter kraven i det underordnade filmottagningssystemet. Nu kan du läsa [filbaserade mål - självstudiekurs](/help/destinations/ui/activate-batch-profile-destinations.md) för att börja exportera filer till den önskade molnlagringsplatsen.
