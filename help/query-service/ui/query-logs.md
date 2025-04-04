---
title: Frågeloggar
description: Frågeloggar genereras automatiskt varje gång en fråga körs och är tillgängliga via användargränssnittet som hjälp vid felsökning. I det här dokumentet beskrivs hur du använder och navigerar i avsnittet Loggar för frågetjänst i användargränssnittet.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Frågeloggar

Adobe Experience Platform har en logg över alla frågehändelser som inträffar via både API och gränssnittet. Den här informationen är tillgänglig i gränssnittet för frågetjänsten på fliken [!UICONTROL Logs].

Loggfilerna genereras automatiskt av en frågehändelse och innehåller information om t.ex. vilken SQL som används, status för frågan, hur lång tid det tog och senaste körningstid. Du kan använda frågeloggdata som ett kraftfullt verktyg för felsökning av ineffektiva frågor eller problemfrågor. Mer omfattande logginformation finns som en del av granskningsloggen och finns i [granskningsloggens dokumentation](../../landing/governance-privacy-security/audit-logs/overview.md).

## Kontrollera frågeloggar {#check-query-logs}

Om du vill kontrollera frågeloggarna väljer du [!UICONTROL Queries] för att navigera till arbetsytan för frågetjänsten och väljer [!UICONTROL Log] bland de tillgängliga alternativen.

>[!NOTE]
>
>Både systemfrågor och kontrollpanelfrågor är exkluderade som standard. I avsnittet [filters](#filter-logs) finns mer information om hur du förfinar de visade loggarna baserat på dina inställningar.

![Användargränssnittet för Experience Platform med frågor och logg markerat.](../images/ui/query-log/logs.png)

## Anpassa och söka {#customize-and-search}

Frågetjänstloggar presenteras i ett anpassbart tabellformat. Om du vill anpassa tabellkolumnerna väljer du inställningsikonen (![En inställningsikon.](/help/images/icons/column-settings.png)) till höger om skärmen. En [!UICONTROL Customize Table]-dialogruta visas där varje kolumn kan avmarkeras.

Du kan också söka efter loggar som relaterar till särskilda frågemallar genom att skriva mallnamnet i sökfältet.

![Arbetsytan för frågeloggen med sökfältet och listrutan för hantering av kolumntabeller är markerad.](../images/ui/query-log/customize-logs.png)

En [beskrivning för var och en av loggtabellkolumnerna ](./overview.md#log) finns i loggavsnittet i frågetjänstens översikt.

## Identifiera loggdata

Varje rad representerar loggdata för en frågekörning som är associerad med en frågemall. Markera en rad i tabellen för att fylla i den högra sidofältet med loggdata för den körningen.

![Arbetsytan i frågeloggen med en markerad rad och loggdata i det högra sidofältet markerade.](../images/ui/query-log/log-details.png)

På panelen med logginformation kan du utföra olika åtgärder. Du kan köra frågan som CTAS, vilket skapar en ny utdatamängd, se eller kopiera hela SQL-frågan som användes i körningen, eller ta bort frågan.

>[!NOTE]
>
>Alternativet för [!UICONTROL Run as CTAS] är bara tillgängligt för en SELECT-fråga.

![Arbetsytan Frågelogg med en markerad rad, Kör som CTAS, Ta bort fråga och ikonen Kopiera SQL markerad.](../images/ui/query-log/edit-output-dataset.png)

Du kan också välja ett frågemallnamn i kolumnen [!UICONTROL Name] för att navigera direkt till vyn [!UICONTROL Query log details].

>[!NOTE]
>
>Om frågan skapades med API:t och inget mallnamn angavs under initieringen visas i stället det första dussintalet tecken i SQL-frågan.

![Vyn med information om frågeloggen.](../images/ui/query-log/query-log-details.png)

## Redigera loggar {#edit-logs}

Bredvid varje rads mallnamn eller SQL-kodfragment finns en pennikon (![En pennikon.](/help/images/icons/edit.png)) som du kan använda för att navigera till frågeredigeraren. Frågan fylls sedan i automatiskt i redigeraren för redigering.

![Arbetsytan i frågeloggen med en pennikon markerad.](../images/ui/query-log/edit-query.png)

## Filterloggar {#filter-logs}

Du kan filtrera listan med frågeloggar baserat på olika inställningar. Välj filterikonen (![Filterikonen.](/help/images/icons/filter.png)) längst upp till vänster på arbetsytan för att öppna en uppsättning filteralternativ i den vänstra listen.

![Arbetsytan i frågeloggen med filterikonen markerad.](../images/ui/query-log/log-filter.png)

Listan med tillgängliga filter visas.

![Arbetsytan för frågeloggen med filteralternativen visade och markerade.](../images/ui/query-log/log-filter-settings.png)

Följande tabell innehåller en beskrivning av varje filter.

| Filter | Beskrivning |
| ------ | ----------- |
| [!UICONTROL Exclude dashboard queries] | Den här kryssrutan är aktiverad som standard och utesluter loggar som genereras av frågor som används för att generera insikter. Dessa frågor genereras av systemet och döljer posterna för användargenererade loggar som krävs för övervakning, administration och felsökning. Om du vill visa systemgenererade loggar avmarkerar du kryssrutan. |
| [!UICONTROL Exclude system queries] | Den här kryssrutan är aktiverad som standard och utesluter loggar som genereras av systemet. Systemgenererade frågor innehåller ofta bakgrundsuppgifter eller underhållsåtgärder som kanske inte är relevanta för användarövervakning, administration eller felsökning. Om du behöver inspektera systemgenererade loggar avmarkerar du den här kryssrutan för att inkludera dem i loggvyn. |
| [!UICONTROL Start date] | Om du vill filtrera loggarna efter frågor som har skapats under en viss period anger du datumen [!UICONTROL Start] och [!UICONTROL End] i avsnittet [!UICONTROL Start date]. |
| [!UICONTROL Completed date] | Om du vill filtrera loggarna efter frågor som har slutförts under en viss period anger du datumen [!UICONTROL Start] och [!UICONTROL End] i avsnittet [!UICONTROL Completed date]. |
| [!UICONTROL Status] | Om du vill filtrera loggar baserat på [!UICONTROL Status] i frågan väljer du lämplig alternativknapp. De tillgängliga alternativen är [!UICONTROL Submitted], [!UICONTROL In progress], [!UICONTROL Success] och [!UICONTROL Failed]. Du kan bara filtrera loggar baserat på ett statusvillkor åt gången. |
| [!UICONTROL Client] | Om du vill filtrera loggar baserat på den frågeklient som används anger du något av följande godkända värden i fritextfältet: `API`, `Adobe Query Service UI` eller `QsAccel`. |
| [!UICONTROL My queries] | Använd växlingsknappen [!UICONTROL My queries] för att filtrera loggarna efter frågor som du har utfört. |
| [!UICONTROL query log ID] | Om du vill filtrera baserat på ett frågas unika logg-ID anger du logg-ID i fritextfältet. Den här informationen finns i [!UICONTROL Log details]. |

Alla filter som används visas ovanför de filtrerade loggresultaten.

![Fliken Logg på arbetsytan Frågor med listan över använda filter markerad.](../images/ui/query-log/applied-log-filters.png)

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur frågeloggar används i användargränssnittet för frågetjänsten.

Se [användargränssnittsöversikt](./overview.md) eller [API-handboken för frågetjänsten](../api/getting-started.md) om du vill veta mer om funktionerna i frågetjänsten.

Se dokumentet [övervaka frågor](./monitor-queries.md) för att lära dig hur frågetjänsten förbättrar synligheten för schemalagda frågekörningar.
