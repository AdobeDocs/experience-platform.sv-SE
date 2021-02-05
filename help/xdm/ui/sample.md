---
solution: Experience Platform
title: Generera exempeldata för ett XDM-schema i användargränssnittet
description: Lär dig hur du genererar JSON-exempeldata baserat på ett befintligt schema i Adobe Experience Platform användargränssnitt.
topic: user guide
translation-type: tm+mt
source-git-commit: 87497ef8a0ebf8de8b6c2dff1650c0b982299e8a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Generera exempeldata för ett XDM-schema i användargränssnittet

För att kunna importera data till Adobe Experience Platform måste dataformatet och datastrukturen överensstämma med ett befintligt XDM-schema (Experience Data Model). Beroende på hur komplicerat schemat är för en viss datauppsättning kan det vara svårt att fastställa den exakta formen för de data som datauppsättningen förväntar sig vid intag.

För alla scheman som du definierar i användargränssnittet för Experience Platform kan du generera ett JSON-exempelobjekt som följer schemats struktur. Det här objektet kan fungera som en mall för alla data som hämtas till datauppsättningar som använder det aktuella schemat.

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen i plattformsgränssnittet. Under fliken **[!UICONTROL Browse]** letar du reda på schemat som du vill generera exempeldata för. Välj det i listan och den högra uppdateringen av fältet för att visa information om schemat. Här väljer du **[!UICONTROL Download sample file].**

![](../images/ui/sample/sample-data.png)

En JSON-exempelfil hämtas av webbläsaren. Du kan nu använda den här filen som referens för hur du strukturerar dina data när du importerar till datauppsättningar som använder det här schemat.

## Nästa steg

I den här guiden beskrivs hur du genererar en JSON-exempelfil från ett XDM-schema i plattformens användargränssnitt. Om du vill lära dig hur du genererar exempeldata med API:t för schemaregister läser du i [exempeldataslutpunktshandboken](../api/sample-data.md).

När du är redo att börja inhämta data kan du läsa självstudiekursen om [mappning av en CSV-fil till XDM](../../ingestion/tutorials/map-a-csv-file.md) för att lära dig hur du mappar en platt datafil (t.ex. en CSV) till ett XDM-schema och importerar den till Platform. Du kan också upprätta en [källanslutning](../../sources/home.md) för att hämta data från en extern källa och mappa dem till XDM.

Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] i gränssnittet finns i översikten för arbetsytan [[!UICONTROL Schemas]](./overview.md).