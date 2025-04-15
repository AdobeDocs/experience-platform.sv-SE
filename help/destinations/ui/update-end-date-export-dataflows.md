---
title: Uppdatera slutdatumet för datauppsättningsexportdataflöden (åtgärd krävs senast 1 maj 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Lär dig hur du uppdaterar slutdatumet för datauppsättningsexportdataflöden med det aktuella slutdatumet den 1 maj 2025.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Uppdatera slutdatumet för datauppsättningsexportdataflöden (åtgärd krävs senast 1 maj 2025)

>[!IMPORTANT]
>
>Åtgärdsobjekten på den här sidan gäller om din organisation ställer in datauppsättningsexportdataflöden före versionen från september 2024 av Experience Platform.

## Vad händer?

I [september 2024-utgåvan av Experience Platform](/help/release-notes/latest/latest.md#destinations) introducerades alternativet att ange ett `endTime`-datum för datauppsättningsdataflöden för export. Adobe har också infört standardslutdatumet 1 maj 2025 för alla datauppsättningsexportdataflöden som skapats *före versionen från september 2024*. Dessa dataflöden visar för närvarande ett meddelande som liknar det som visas nedan.

![Gränssnittsmeddelanden om att slutdatumet för exportdatauppsättningens dataflöde behöver uppdateras.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Åtgärdsobjekt**: För något av dessa dataflöden måste du uppdatera slutdatumet manuellt innan det upphör att gälla, annars avbryts exporten. Använd användargränssnittet i Experience Platform för att identifiera vilka dataflöden som ska stoppas 1 maj 2025.

## Varför meddelas jag?

Din organisation har identifierats som att ha aktiva datauppsättningsexportdataflöden med slutdatumet 1 maj 2025.

## Använd användargränssnittet för att uppdatera slutdatumet

Använd Experience Platform-gränssnittet för att identifiera dataflöden med slutdatumet 1 maj 2025 och uppdatera dem till ett framtida datum.

### Hitta de dataflöden som behöver uppdateras

Navigera till **Destinationer > Bläddra** och leta efter datatypen **Datasets** i kolumnen **Datatyp**, som visas nedan. Välj önskade dataflöden för att inspektera dem.

![Datauppsättningsexportfält är markerade på fliken Bläddra.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Uppdatera slutdatumet för dataflödena

Så här uppdaterar du slutdatumet för dataflöden:

1. Välj **Exportera datamängder** i de dataflöden som du har valt att inspektera i föregående steg.
   ![Kontrollen Exportera datauppsättningar är markerad på fliken Bläddra.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. Gå till steget **Schemaläggning** i arbetsflödet och välj **Redigera schema**.
   ![Redigera schemakontroll markerad i schemaläggningssteget.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Välj ett önskat slutdatum efter 1 maj 2025 och välj **Spara**.
   ![Välj slutdatumkontroll markerat i schemaläggningssteget.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Fortsätt till slutet av arbetsflödet och spara uppdateringarna.

Mer information om schemaläggningssteget finns i självstudiekursen [för export av datauppsättningar](/help/destinations/api/export-datasets.md#scheduling).

## Använd API:t för att uppdatera slutdatumet

### Hitta de dataflöden som behöver uppdateras

### Uppdatera slutdatumet för dataflödena
