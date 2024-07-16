---
solution: Experience Platform
title: Generera exempeldata för ett XDM-schema i användargränssnittet
description: Lär dig hur du genererar JSON-exempeldata baserat på ett befintligt schema i Adobe Experience Platform användargränssnitt.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Generera exempeldata för ett XDM-schema i användargränssnittet {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Hämta exempelfil"
>abstract="Generera ett JSON-exempelobjekt som följer det valda schemats struktur. Det här objektet kan fungera som en mall för att säkerställa att dina data är korrekt formaterade för inmatning i datauppsättningar som använder det schemat. JSON-exempelfilen hämtas av webbläsaren."

För att kunna importera data till Adobe Experience Platform måste dataformatet och datastrukturen överensstämma med ett befintligt XDM-schema (Experience Data Model). Beroende på hur komplicerat schemat är för en viss datauppsättning kan det vara svårt att fastställa den exakta formen för de data som datauppsättningen förväntar sig vid intag.

För alla scheman som du definierar i användargränssnittet för Experience Platform kan du generera ett JSON-exempelobjekt som följer schemats struktur. Det här objektet kan fungera som en mall för alla data som hämtas till datauppsättningar som använder det aktuella schemat.

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen i plattformsgränssnittet. Gå till fliken **[!UICONTROL Browse]** och leta reda på schemat som du vill generera exempeldata för. Välj det i listan och den högra uppdateringen av spåret för att visa information om schemat. Välj **[!UICONTROL Download sample file]** härifrån.

![Fliken Bläddra på arbetsytan Scheman med ett schema markerat och hämtningsexempelfilen markerad.](../images/ui/sample/sample-data.png)

En JSON-exempelfil hämtas av webbläsaren. Du kan nu använda den här filen som referens för hur du strukturerar dina data när du importerar till datauppsättningar som använder det här schemat.

## Nästa steg

I den här guiden beskrivs hur du genererar en JSON-exempelfil från ett XDM-schema i plattformens användargränssnitt. Om du vill lära dig hur du genererar exempeldata med API:t för schemaregister läser du [exempeldatans slutpunktshandbok](../api/sample-data.md).

När du är redo att börja inhämta data, se självstudiekursen [Mappa en CSV-fil till XDM](../../ingestion/tutorials/map-csv/overview.md) för att lära dig hur du mappar en platt datafil (till exempel en CSV-fil) till ett XDM-schema och importerar den till plattformen. Du kan också upprätta en [källanslutning](../../sources/home.md) för att hämta data från en extern källa och mappa dem till XDM.

Mer information om funktionerna för arbetsytan [!UICONTROL Schemas] i gränssnittet finns i [[!UICONTROL Schemas] -arbetsytans översikt ](./overview.md).
