---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en datauppsättning för att exportera ett målgruppssegment
topic: tutorial
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Skapa en datauppsättning för att exportera ett målgruppssegment

[!DNL Adobe Experience Platform] kan ni enkelt segmentera kundprofiler i målgrupper baserat på specifika attribut. När segment har skapats kan ni exportera den målgruppen till en datauppsättning där den kan nås och hanteras. För att exporten ska lyckas måste datauppsättningen konfigureras korrekt.

I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av [!DNL Experience Platform] användargränssnittet.

Den här självstudiekursen är direkt relaterad till de steg som beskrivs i självstudiekursen för [utvärdering och åtkomst av segmentresultat](./evaluate-a-segment.md). I självstudiekursen för utvärdering av ett segment beskrivs hur du skapar en datauppsättning med API:t, medan den här självstudiekursen beskriver stegen för att skapa en datauppsättning med [!DNL Catalog Service] [!DNL Experience Platform] användargränssnittet.

## Komma igång

För att kunna exportera ett segment måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema]. Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar fälten för alla scheman som delar samma klass, i det här fallet [!DNL XDM Individual Profile] klassen. Mer information om unionsvyscheman finns i avsnittet Kundprofil i [realtid i Utvecklarhandbok](../../xdm/schema/composition.md#union)för schemaregister.

Om du vill visa unionsscheman i användargränssnittet klickar du **[!UICONTROL Profiles]** i den vänstra navigeringen och sedan på **[!UICONTROL Union schema]** fliken enligt nedan.

![Fliken Unionsschema i användargränssnittet för Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Arbetsytan Datauppsättningar

Med arbetsytan Datauppsättningar i [!DNL Experience Platform] användargränssnittet kan du visa och hantera alla datauppsättningar som din IMS-organisation har skapat, samt skapa nya.

Om du vill visa arbetsytan för datauppsättningar klickar du **[!UICONTROL Datasets]** i den vänstra navigeringen och sedan på **[!UICONTROL Browse]** fliken. Arbetsytan för datauppsättningar innehåller en lista med datauppsättningar, inklusive kolumner som visar **[!UICONTROL Name]**, **[!UICONTROL Created]** (datum och tid), **[!UICONTROL Source]**, **[!UICONTROL Schema]** och **[!UICONTROL Last Batch Status]**, samt datum och tid då datauppsättningen skapades **[!UICONTROL Last Updated]**. Beroende på bredden på varje kolumn kan du behöva rulla åt vänster eller höger för att se alla kolumner.

>[!NOTE]
>
>Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för att visa endast de datauppsättningar som är aktiverade för [!DNL Real-time Customer Profile].

![Visa alla datauppsättningar](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning klickar du **[!UICONTROL Create Dataset]** i det övre högra hörnet av [!UICONTROL Datasets] arbetsytan.

![Klicka på Skapa datauppsättning](../images/tutorials/segment-export-dataset/dataset-click-create.png)

På **[!UICONTROL Create Dataset]** skärmen klickar du på **[!UICONTROL Create Dataset from Schema]** för att fortsätta.

![Välj datakälla](../images/tutorials/segment-export-dataset/create-dataset.png)

## Välj XDM-schema för enskild profilunion

Om du vill välja [!DNL XDM Individual Profile Union Schema] den som ska användas i datauppsättningen söker du efter schemat&quot;[!UICONTROL XDM Individual Profile]&quot; med typen&quot;[!UICONTROL Union]&quot; på **[!UICONTROL Select Schema]** skärmen.

Markerade alternativknappen bredvid **[!UICONTROL XDM Individual Profile]** och klicka sedan **[!UICONTROL Next]** i det övre högra hörnet.

![Välj schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Konfigurera datauppsättning

På **[!UICONTROL Configure Dataset]** skärmen måste du ge datauppsättningen en **[!UICONTROL Name]** och kan även tillhandahålla en **[!UICONTROL Description]** av datauppsättningarna.

**Kommentarer om datauppsättningsnamn:**
- Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
- Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
- Det är bäst att ge ytterligare information om datauppsättningen med hjälp av beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning klickar du på **[!UICONTROL Finish]**.

![Konfigurera datauppsättning](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datauppsättningsaktivitet

En tom datauppsättning har nu skapats och du har returnerats till **[!UICONTROL Dataset Activity]** fliken i [!UICONTROL Datasets] arbetsytan. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Till höger på arbetsytan Datauppsättningar ser du fliken **[!UICONTROL Info]** med information om den nya datauppsättningen, till exempel **[!UICONTROL Dataset ID]**, **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL Table Name]**, **[!UICONTROL Schema]**, **[!UICONTROL Streaming]** och **[!UICONTROL Source]**. Fliken innehåller även information om när datauppsättningen skapades [!UICONTROL Info] och dess **[!UICONTROL Created]** **[!UICONTROL Last Modified]** datum.

Observera **[!UICONTROL Dataset ID]** detta eftersom det här värdet krävs för att slutföra arbetsflödet för målgruppsexport.

![Datauppsättningsaktivitet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nästa steg

Nu när du har skapat en datauppsättning baserat på [!DNL XDM Individual Profile Union Schema]kan du använda **[!UICONTROL Dataset ID]** för att fortsätta [utvärdera och komma åt segmentresultaten](./evaluate-a-segment.md) .

Nu kan du gå tillbaka till självstudiekursen för utvärdering av segmentresultat och hämta från [genereringsprofilerna för målgruppsmedlemmar](./evaluate-a-segment.md#generate-profiles) i steget för att exportera ett segmentarbetsflöde.
