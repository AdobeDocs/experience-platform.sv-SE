---
title: Frågeloggar
description: Frågeloggar genereras automatiskt varje gång en fråga körs och är tillgängliga via användargränssnittet som hjälp vid felsökning. I det här dokumentet beskrivs hur du använder och navigerar i avsnittet Loggar för frågetjänst i användargränssnittet.
source-git-commit: 22deca5f9bcf6bcf97cca01b97fce9d22800b767
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# Frågeloggar

Adobe Experience Platform har en logg över alla frågehändelser som inträffar via både API och gränssnittet. Den här informationen är tillgänglig i användargränssnittet för frågetjänsten från [!UICONTROL Logs] -fliken.

Loggfilerna genereras automatiskt av en frågehändelse och innehåller information om t.ex. vilken SQL som används, status för frågan, hur lång tid det tog och senaste körningstid. Du kan använda frågeloggdata som ett kraftfullt verktyg för felsökning av ineffektiva frågor eller problemfrågor. Mer omfattande logginformation finns i loggen i [granskningsloggens dokumentation](../../landing/governance-privacy-security/audit-logs/overview.md).

## Kontrollera frågeloggar

Om du vill kontrollera frågeloggarna väljer du [!UICONTROL Queries] för att gå till arbetsytan för frågetjänsten och välja [!UICONTROL Log] bland de tillgängliga alternativen.

![Plattformsgränssnittet med frågor och logg markerat.](../images/ui/query-log/logs.png)

## Anpassa och söka {#customize-and-search}

Frågetjänstloggar presenteras i ett anpassbart tabellformat. Om du vill anpassa tabellkolumnerna väljer du inställningsikonen (![En inställningsikon.](../images/ui/query-log/settings-icon.png)) till höger på skärmen. A [!UICONTROL Customize Table] visas där varje kolumn kan avmarkeras.

Du kan också söka efter loggar som relaterar till särskilda frågemallar genom att skriva mallnamnet i sökfältet.

![Arbetsytan i Loggboken med sökfältet och listrutan Hantera kolumntabeller är markerad.](../images/ui/query-log/customize-logs.png)

A [beskrivning för var och en av loggtabellkolumnerna](./overview.md#log) finns i loggavsnittet i översikten över frågetjänsten.

## Identifiera loggdata

Varje rad representerar loggdata för en frågekörning som är associerad med en frågemall. Markera en rad i tabellen för att fylla i den högra sidofältet med loggdata för den körningen.

![Arbetsytan i frågeloggen med en markerad rad och loggdata i den högra sidofältet markerade.](../images/ui/query-log/log-details.png)

På panelen med logginformation kan du välja en ny utdatamängd och se eller kopiera hela SQL-frågan som användes i körningen.

![Arbetsytan för frågeloggen med en rad markerad och utdatamängden och SQL-frågan markerad.](../images/ui/query-log/edit-output-dataset.png)

Du kan också välja ett frågemallsnamn i dialogrutan [!UICONTROL Name] för att navigera direkt till [!UICONTROL Query log details] vy.

>[!NOTE]
>
>Om frågan skapades med API:t och inget mallnamn angavs under initieringen visas i stället det första dussintalet tecken i SQL-frågan.

![Vyn med information om frågeloggen.](../images/ui/query-log/query-log-details.png)

Bredvid varje rads mallnamn eller SQL-kodfragment finns en pennikon (![En pennikon.](../images/ui/query-log/edit-icon.png)) som du kan använda för att navigera till Frågeredigeraren. Frågan fylls sedan i automatiskt i redigeraren för redigering.

![Arbetsytan för frågeloggen med en pennikon markerad.](../images/ui/query-log/edit-query.png)

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur frågeloggar används i användargränssnittet för frågetjänsten.

Se [Översikt över användargränssnittet](./overview.md)eller [API-guide för frågetjänst](../api/getting-started.md) om du vill veta mer om funktionerna i frågetjänsten.

Se [övervaka frågedokument](./monitor-queries.md) om du vill veta hur frågetjänsten förbättrar synligheten för schemalagda frågekörningar.
