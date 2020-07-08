---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en datauppsättning för att exportera ett målgruppssegment
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# Skapa en datauppsättning för att exportera ett målgruppssegment

Med Adobe Experience Platform kan ni enkelt segmentera kundprofiler i målgrupper baserat på specifika attribut. När segment har skapats kan ni exportera den målgruppen till en datauppsättning där den kan nås och hanteras. För att exporten ska lyckas måste datauppsättningen konfigureras korrekt.

I den här självstudiekursen går du igenom de steg som krävs för att skapa en datauppsättning som kan användas för att exportera ett målgruppssegment med hjälp av användargränssnittet i Experience Platform.

Den här självstudiekursen är direkt relaterad till de steg som beskrivs i självstudiekursen för [utvärdering och åtkomst av segmentresultat](./evaluate-a-segment.md). I självstudiekursen för utvärdering av ett segment beskrivs hur du skapar en datauppsättning med hjälp av Catalog-API:t, medan den här självstudiekursen beskriver stegen för att skapa en datauppsättning med hjälp av användargränssnittet i Experience Platform.

## Komma igång

För att kunna exportera ett segment måste datauppsättningen baseras på XDM Individual Profile Union Schema. Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar fälten för alla scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionsvyscheman finns i avsnittet Kundprofil i [realtid i Utvecklarhandbok](../../xdm/schema/composition.md#union)för schemaregister.

Om du vill visa unionsscheman i användargränssnittet klickar du på **Profiler** i den vänstra navigeringen och sedan på fliken *Unionsschema* enligt nedan.

![Fliken Unionsschema i användargränssnittet för Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Arbetsytan Datauppsättningar

Med arbetsytan Datauppsättningar i användargränssnittet i Experience Platform kan du visa och hantera alla datauppsättningar som din IMS-organisation har skapat, samt skapa nya.

Om du vill visa arbetsytan för datauppsättningar klickar du på **Datauppsättningar** i den vänstra navigeringen och sedan på fliken *Bläddra* . Datamängdens arbetsyta innehåller en lista med datauppsättningar, inklusive kolumner med *namn*, *Skapad* (datum och tid), *Källa*, *Schema* och *Senaste batchstatus***, samt datum och tid då datauppsättningen uppdaterades¥Last Updated¥. Beroende på bredden på varje kolumn kan du behöva rulla åt vänster eller höger för att se alla kolumner.

>[!NOTE]
>
>Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för att visa endast de datauppsättningar som har aktiverats för kundprofil i realtid.

![Visa alla datauppsättningar](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning klickar du på **Skapa datauppsättning** i det övre högra hörnet av arbetsytan Datauppsättningar.

![Klicka på Skapa datauppsättning](../images/tutorials/segment-export-dataset/dataset-click-create.png)

På skärmen *Skapa datauppsättning* klickar du på **Skapa datauppsättning från schema** för att fortsätta.

![Välj datakälla](../images/tutorials/segment-export-dataset/create-dataset.png)

## Välj XDM-schema för enskild profilunion

Om du vill välja XDM Individual Profile Union Schema för användning i din datamängd kan du hitta schemat &quot;XDM Individual Profile&quot; med typen &quot;Union&quot; på skärmen *Select Schema* .

Markerade alternativknappen bredvid **XDM-individuell profil** och klicka sedan på **Nästa** i det övre högra hörnet.

![Välj schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Konfigurera datauppsättning

På skärmen **Konfigurera datauppsättning** måste du ge datauppsättningen ett *namn* och kan även ge en *beskrivning* av datauppsättningen.

**Kommentarer om datauppsättningsnamn:**
- Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
- Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
- Det är bäst att ge ytterligare information om datauppsättningen med hjälp av beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning klickar du på **Slutför**.

![Konfigurera datauppsättning](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datauppsättningsaktivitet

En tom datauppsättning har nu skapats och du har återgått till fliken *Datauppsättningsaktivitet* på arbetsytan Datauppsättningar. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Till höger på arbetsytan Datauppsättningar visas fliken **Info** med information om din nya datauppsättning, till exempel *datauppsättnings-ID*, *namn*, *beskrivning*, *tabellnamn*******,¥Schema,¥Streaming¥ och¥Source¥. Fliken Info innehåller även information om när datauppsättningen *skapades* och dess *senaste ändrade* datum.

Observera **datauppsättnings-ID** eftersom det här värdet krävs för att slutföra arbetsflödet för målgruppsexport.

![Datauppsättningsaktivitet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nästa steg

Nu när du har skapat en datauppsättning baserad på XDM-schemat för enskilda profiler kan du använda **datauppsättnings-ID** för att fortsätta [utvärdera och komma åt segmentresultaten](./evaluate-a-segment.md) .

Nu kan du gå tillbaka till självstudiekursen för utvärdering av segmentresultat och hämta information från [Generera enskilda XDM-profiler för målgruppsmedlemmar](./evaluate-a-segment.md#generate-profiles-for-audience-members) under [exporten av ett segmentarbetsflöde](./evaluate-a-segment.md#export-a-segment) .
