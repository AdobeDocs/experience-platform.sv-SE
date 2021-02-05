---
keywords: Experience Platform;hem;populära ämnen;Segmenteringstjänst;segmentering;Segmentering;skapa en datauppsättning;exportera målgruppssegment;exportsegment;
solution: Experience Platform
title: Skapa en datauppsättning för export av ett målgruppssegment
topic: tutorial
type: Tutorial
description: I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av användargränssnittet i Experience Platform.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# Skapa en datauppsättning för att exportera ett målgruppssegment

[!DNL Adobe Experience Platform] kan ni enkelt segmentera kundprofiler i målgrupper baserat på specifika attribut. När segment har skapats kan ni exportera den målgruppen till en datauppsättning där den kan nås och hanteras. För att exporten ska lyckas måste datauppsättningen konfigureras korrekt.

I den här självstudien går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av användargränssnittet i [!DNL Experience Platform].

Den här självstudiekursen är direkt relaterad till de steg som beskrivs i självstudiekursen för [utvärdering och åtkomst av segmentresultat](./evaluate-a-segment.md). I självstudiekursen för utvärdering av ett segment beskrivs hur du skapar en datauppsättning med hjälp av API:t [!DNL Catalog Service], medan den här självstudiekursen visar steg för att skapa en datauppsättning med hjälp av användargränssnittet [!DNL Experience Platform].

## Komma igång

För att kunna exportera ett segment måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema]. Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar fälten för alla scheman som delar samma klass, i det här fallet klassen [!DNL XDM Individual Profile]. Mer information om unionsvyscheman finns i avsnittet [Kundprofil i realtid i Utvecklarhandbok för schemaregister](../../xdm/schema/composition.md#union).

Om du vill visa unionsscheman i användargränssnittet klickar du på **[!UICONTROL Profiles]** i den vänstra navigeringen och sedan på fliken **[!UICONTROL Union schema]** enligt nedan.

![Fliken Unionsschema i användargränssnittet för Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Arbetsytan Datauppsättningar

Med arbetsytan Datauppsättningar i [!DNL Experience Platform]-gränssnittet kan du visa och hantera alla datauppsättningar som din IMS-organisation har skapat, samt skapa nya.

Om du vill visa arbetsytan för datauppsättningar klickar du på **[!UICONTROL Datasets]** i den vänstra navigeringen och sedan på fliken **[!UICONTROL Browse]**. Arbetsytan för datauppsättningar innehåller en lista med datauppsättningar, inklusive kolumner med namn, skapad (datum och tid), källa, schema och senaste batchstatus, samt datum och tid då datauppsättningen senast uppdaterades. Beroende på bredden på varje kolumn kan du behöva rulla åt vänster eller höger för att se alla kolumner.

>[!NOTE]
>
>Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för att visa endast de datauppsättningar som är aktiverade för [!DNL Real-time Customer Profile].

![Visa alla datauppsättningar](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning klickar du på **[!UICONTROL Create Dataset]** i det övre högra hörnet på arbetsytan **[!UICONTROL Datasets]**.

![Klicka på Skapa datauppsättning](../images/tutorials/segment-export-dataset/dataset-click-create.png)

På skärmen **[!UICONTROL Create Dataset]** klickar du på **[!UICONTROL Create Dataset from Schema]** för att fortsätta.

![Välj datakälla](../images/tutorials/segment-export-dataset/create-dataset.png)

## Välj XDM-schema för enskild profilunion

Om du vill välja [!DNL XDM Individual Profile Union Schema] som ska användas i datauppsättningen söker du efter schemat [!UICONTROL XDM Individual Profile] med typen [!UICONTROL Union] på **[!UICONTROL Select Schema]**-skärmen.

Markerade alternativknappen bredvid **[!UICONTROL XDM Individual Profile]** och klicka sedan på **[!UICONTROL Next]** i det övre högra hörnet.

![Välj schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Konfigurera datauppsättning

På skärmen **[!UICONTROL Configure Dataset]** måste du ge datauppsättningen ett namn och du kan även ge en beskrivning av datauppsättningen.

**Kommentarer om datauppsättningsnamn:**
- Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
- Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
- Det är bäst att ge ytterligare information om datauppsättningen med hjälp av beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning klickar du på **[!UICONTROL Finish]**.

![Konfigurera datauppsättning](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datauppsättningsaktivitet

En tom datauppsättning har skapats och du har returnerats till fliken **[!UICONTROL Dataset Activity]** på arbetsytan **[!UICONTROL Datasets]**. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Till höger på arbetsytan Datauppsättningar visas fliken **[!UICONTROL Info]** med information om din nya datauppsättning, till exempel datauppsättnings-ID, namn, beskrivning, tabellnamn, schema, direktuppspelning och källa. Fliken **[!UICONTROL Info]** innehåller även information om när datauppsättningen skapades och dess senaste ändringsdatum.

Observera **[!UICONTROL Dataset ID]** eftersom det här värdet krävs för att slutföra arbetsflödet för målgruppsexport.

![Datauppsättningsaktivitet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nästa steg

Nu när du har skapat en datauppsättning baserad på [!DNL XDM Individual Profile Union Schema] kan du använda datauppsättnings-ID:t för att fortsätta med [utvärderingen och åtkomsten till segmentresultaten](./evaluate-a-segment.md)-självstudiekursen.

Återgå till självstudiekursen för att utvärdera segmentresultaten och fortsätt med att välja bland [genereringsprofiler för målgruppsmedlemmar](./evaluate-a-segment.md#generate-profiles) steg i processen för att exportera ett segmentarbetsflöde.
