---
keywords: Experience Platform;hem;populära ämnen;Segmenteringstjänst;segmentering;Segmentering;skapa en datauppsättning;exportera målgruppssegment;exportsegment;
solution: Experience Platform
title: Skapa en datauppsättning för export av ett målgruppssegment
topic-legacy: tutorial
type: Tutorial
description: I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av användargränssnittet i Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: f7d204442c8bc2355671ba2adffff4c40ce08784
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Skapa en datauppsättning för att exportera ett målgruppssegment

[!DNL Adobe Experience Platform] gör att ni kan segmentera kundprofiler i målgrupper baserat på specifika attribut. När ett segment har skapats kan du exportera den målgruppen till en datauppsättning där den kan nås och hanteras. För att exporten ska lyckas måste datauppsättningen konfigureras korrekt.

I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av [!DNL Experience Platform] Gränssnitt.

Den här självstudiekursen är direkt relaterad till de steg som beskrivs i självstudiekursen om [utvärdera och komma åt segmentresultat](./evaluate-a-segment.md). Självstudiekursen för segmentutvärdering innehåller steg för att skapa en datauppsättning med [!DNL Catalog Service] API, medan den här självstudiekursen beskriver steg för att skapa en datauppsättning med [!DNL Experience Platform] Gränssnitt.

## Komma igång

För att kunna exportera ett segment måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema]. Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar fälten för alla scheman som delar samma klass. Mer information om unionsscheman finns i handboken om [grunderna för schemakomposition](../../xdm/schema/composition.md#union).

Om du vill visa unionsscheman i användargränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen väljer du **[!UICONTROL Union Schema]** enligt nedan.

![Fliken för unionsschema är markerad.](../images/tutorials/segment-export-dataset/union.png)

## Arbetsytan Datauppsättningar

The [!UICONTROL Datasets] kan du visa och hantera alla datauppsättningar för din organisation.

Välj **[!UICONTROL Datasets]** i den vänstra navigeringen för att komma åt arbetsytan väljer du **[!UICONTROL Browse]**. På den här fliken visas en lista med datauppsättningar och deras information. Beroende på bredden på varje kolumn kan du behöva rulla åt vänster eller höger för att se alla kolumner.

>[!NOTE]
>
>Markera filterikonen bredvid sökfältet om du bara vill visa de datauppsättningar som är aktiverade för [!DNL Real-time Customer Profile].

![Arbetsytan för datauppsättningar visas.](../images/tutorials/segment-export-dataset/browse.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning väljer du **[!UICONTROL Create Dataset]**.

![Knappen Skapa datauppsättning är markerad.](../images/tutorials/segment-export-dataset/create-dataset.png)

På nästa skärm väljer du **[!UICONTROL Create Dataset from Schema]**.

![Alternativet Skapa datauppsättning från schema är markerat.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Välj XDM-schema för enskild profilunion

Så här väljer du [!DNL XDM Individual Profile Union Schema] som du kan använda i din datauppsättning finns i[!UICONTROL XDM Individual Profile]&quot; på **[!UICONTROL Select Schema]** skärm. När du har valt schemat kan du bekräfta om det är det föreningsschema som finns under **[!UICONTROL API Usage]** i rätt spår. Om [!UICONTROL Schema] banändpunkter med `_union`, det är ett föreningsschema.

>[!NOTE]
>
>Trots att fackliga scheman per definition deltar i kundprofiler i realtid, listas de som&quot;Inte aktiverade&quot; på grund av att de inte är aktiverade för profil på samma sätt som traditionella scheman.

Markera alternativknappen bredvid **[!UICONTROL XDM Individual Profile]** väljer **[!UICONTROL Next]**.

![Schemat för enskild XDM-profil är markerat.](../images/tutorials/segment-export-dataset/select-schema.png)

## Konfigurera datauppsättning

På nästa skärm måste du ge datauppsättningen ett namn. Du kan också lägga till en valfri beskrivning.

**Anteckningar om datauppsättningsnamn:**

* Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
* Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
* Det är bäst att ge ytterligare information om datauppsättningen med hjälp av beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning väljer du **[!UICONTROL Finish]**.

![Sidan Konfigurera datauppsättning visas. Konfigurationsalternativen är markerade.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datauppsättningsaktivitet

När datauppsättningen har skapats visas aktivitetssidan för den datauppsättningen. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Den högra listen innehåller information om din nya datauppsättning, t.ex. datauppsättnings-ID, namn, beskrivning, schema med mera. Observera **[!UICONTROL Dataset ID]**, eftersom det här värdet krävs för att slutföra arbetsflödet för målgruppsexport.

![Sidan med datauppsättningsaktivitet visas. Datauppsättnings-ID markeras eftersom det här värdet måste noteras för framtida steg.](../images/tutorials/segment-export-dataset/activity.png)

## Nästa steg

Nu när du har skapat en datauppsättning baserad på [!DNL XDM Individual Profile Union Schema]kan du använda datauppsättnings-ID:t för att fortsätta [utvärdera och komma åt segmentresultat](./evaluate-a-segment.md) självstudiekurs.

Nu kan du gå tillbaka till självstudiekursen för utvärdering av segmentresultat och hämta information från [skapa profiler för målgruppsmedlemmar](./evaluate-a-segment.md#generate-profiles) steg i exporten av ett segmentarbetsflöde.
