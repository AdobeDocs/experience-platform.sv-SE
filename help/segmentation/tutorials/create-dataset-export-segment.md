---
solution: Experience Platform
title: Skapa en datauppsättning för export av en publik
type: Tutorial
description: Lär dig hur du skapar en datauppsättning som kan användas för att exportera en målgrupp med hjälp av användargränssnittet i Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Skapa en datauppsättning för att exportera en målgrupp

Med [!DNL Adobe Experience Platform] kan du segmentera kundprofiler i målgrupper baserat på specifika attribut. När en segmentdefinition har skapats kan du exportera den resulterande målgruppen till en datauppsättning där den kan nås och hanteras. För att exporten ska lyckas måste datauppsättningen konfigureras korrekt.

I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera en målgrupp med användargränssnittet för [!DNL Experience Platform].

Den här självstudiekursen är direkt relaterad till de steg som beskrivs i självstudiekursen [Utvärdera och komma åt segmenteringsresultat](./evaluate-a-segment.md). I självstudiekursen för utvärdering av segmentdefinitioner finns steg för att skapa en datauppsättning med API:t [!DNL Catalog Service], medan den här självstudiekursen visar steg för att skapa en datauppsättning med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Datauppsättningen måste vara baserad på [!DNL XDM Individual Profile Union Schema] för att du ska kunna exportera en målgrupp. Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar fälten för alla scheman som delar samma klass. Mer information om unionsscheman finns i guiden [Grundläggande om schemakomposition](../../xdm/schema/composition.md#union).

Om du vill visa unionsscheman i användargränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen och sedan **[!UICONTROL Union Schema]** enligt nedan.

![Fliken för unionens schema är markerad.](../images/tutorials/segment-export-dataset/union.png)

## Arbetsytan Datauppsättningar

På arbetsytan [!UICONTROL Datasets] kan du visa och hantera alla datauppsättningar för din organisation.

Välj **[!UICONTROL Datasets]** i den vänstra navigeringen för att komma åt arbetsytan och välj sedan **[!UICONTROL Browse]**. På den här fliken visas en lista med datauppsättningar och deras information. Beroende på bredden på varje kolumn kan du behöva rulla åt vänster eller höger för att se alla kolumner.

>[!NOTE]
>
>Markera filterikonen bredvid sökfältet om du vill använda filterfunktioner för att visa endast de datauppsättningar som är aktiverade för [!DNL Real-Time Customer Profile].

![Arbetsytan för datauppsättningar visas.](../images/tutorials/segment-export-dataset/browse.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning väljer du **[!UICONTROL Create Dataset]**.

![Knappen Skapa datauppsättning är markerad.](../images/tutorials/segment-export-dataset/create-dataset.png)

Välj **[!UICONTROL Create Dataset from Schema]** på nästa skärm.

![Alternativet Skapa datauppsättning från schema är markerat.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Välj XDM-schema för enskild profilunion

Om du vill välja [!DNL XDM Individual Profile Union Schema] som ska användas i din datauppsättning, söker du efter schemat [!UICONTROL XDM Individual Profile] på skärmen **[!UICONTROL Select Schema]**. När du har valt schemat kan du bekräfta om det är unionsschemat under **[!UICONTROL API Usage]** i den högra listen. Om sökvägen [!UICONTROL Schema] slutar med `_union` är det ett unionsschema.

>[!NOTE]
>
>Trots att fackliga scheman per definition ingår i kundprofilen i realtid anges de som&quot;Inte aktiverat&quot; på grund av att de inte är aktiverade för profilen på samma sätt som traditionella scheman.

Markera alternativknappen bredvid **[!UICONTROL XDM Individual Profile]** och välj sedan **[!UICONTROL Next]**.

![Schemat för enskild XDM-profil är markerat.](../images/tutorials/segment-export-dataset/select-schema.png)

## Konfigurera datauppsättning

På nästa skärm måste du ge datauppsättningen ett namn. Du kan också lägga till en valfri beskrivning.

**Kommentarer om datauppsättningsnamn:**

* Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
* Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
* Du bör ange ytterligare information om datauppsättningen med beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning väljer du **[!UICONTROL Finish]**.

![Sidan Konfigurera datauppsättning visas. Konfigurationsalternativen är markerade.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datauppsättningsaktivitet

När datauppsättningen har skapats visas aktivitetssidan för den datauppsättningen. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Den högra listen innehåller information om din nya datauppsättning, t.ex. datauppsättnings-ID, namn, beskrivning, schema med mera. Observera **[!UICONTROL Dataset ID]** eftersom det här värdet krävs för att slutföra arbetsflödet för målgruppsexport.

![Sidan för datauppsättningsaktivitet visas. Datauppsättnings-ID är markerat eftersom det här värdet måste noteras för framtida steg.](../images/tutorials/segment-export-dataset/activity.png)

## Nästa steg

Nu när du har skapat en datauppsättning baserad på [!DNL XDM Individual Profile Union Schema] kan du använda datauppsättnings-ID:t för att fortsätta [utvärdera och komma åt segmentdefinitionsresultat](./evaluate-a-segment.md).

Återgå till självstudiekursen för att utvärdera segmentdefinitionsresultat och fortsätt med att gå från steget [skapa profiler för målgruppsmedlemmar](./evaluate-a-segment.md#generate-profiles) i arbetsflödet för att exportera en målgrupp.
