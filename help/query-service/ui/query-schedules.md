---
title: Frågescheman
description: Lär dig hur du automatiserar schemalagda frågekörningar, tar bort eller inaktiverar ett frågeschema och använder tillgängliga schemaläggningsalternativ via Adobe Experience Platform-gränssnittet.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 75ef9c58aa7c5f1cc628d1f13b6c5f56b362458a
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Frågescheman

Du kan automatisera frågekörningar genom att skapa frågescheman. Schemalagda frågor körs på en anpassad cache för att hantera dina data baserat på frekvens, datum och tid. Du kan också välja en utdatamängd för dina resultat om det behövs. Frågor som har sparats som en mall kan schemaläggas från Frågeredigeraren.

>[!IMPORTANT]
>
>Du kan bara lägga till ett schema i en fråga som redan har skapats, sparats och körts.

Alla schemalagda frågor läggs till i listan i [!UICONTROL Scheduled queries] -fliken. Från den arbetsytan kan du övervaka statusen för alla schemalagda frågejobb via gränssnittet. På [!UICONTROL Scheduled queries] kan du hitta viktig information om frågekörningar och prenumerera på aviseringar. Den tillgängliga informationen omfattar status, schemainformation och felmeddelanden/koder om en körning misslyckas. Se [Övervaka dokument för schemalagda frågor](./monitor-queries.md) för mer information.

## Skapa frågescheman {#create-schedule}

Om du vill lägga till ett schema i en fråga väljer du en frågemall i [!UICONTROL Templates] eller [!UICONTROL Scheduled Queries] för att gå till Frågeredigeraren.

Läs mer om hur du lägger till scheman med API:t i [slutpunktsguide för schemalagda frågor](../api/scheduled-queries.md).

När en sparad fråga öppnas från Frågeredigeraren [!UICONTROL Schedules] -fliken visas under frågenamnet. Välj **[!UICONTROL Schedules]**.

![Frågeredigeraren med fliken Scheman markerad.](../images/ui/query-schedules/schedules-tab.png)

Arbetsytan för scheman visas. Välj **[!UICONTROL Add Schedule]** för att skapa ett schema.

![Arbetsytan Schemaläggning i frågeredigeraren med Lägg till schema markerat.](../images/ui/query-schedules/add-schedule.png)

Sidan med schemainformation visas. På den här sidan kan du välja frekvens för den schemalagda frågan, start- och slutdatum, veckodag som den schemalagda frågan ska köras samt vilken datamängd som frågan ska exporteras till.

![Panelen Schemainformation är markerad.](../images/ui/query-schedules/schedule-details.png)

Du kan välja följande alternativ för **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: Den schemalagda frågan körs varje timme för den datumperiod du har valt.
- **[!UICONTROL Daily]**: Den schemalagda frågan kommer att köras var X:e dag vid den tidpunkt och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Weekly]**: Den valda frågan körs på veckodagarna, tidsperioden och den datumperiod som du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Monthly]**: Den valda frågan körs varje månad på den dag, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Yearly]**: Den valda frågan kommer att köras varje år på den dag, månad, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.

För utdatauppsättningen kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

>[!IMPORTANT]
>
> Eftersom du använder en befintlig eller skapar en ny datauppsättning gör du det **not** måste innehålla antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av frågan, eftersom datauppsättningarna redan har angetts. Inklusive antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av dina schemalagda frågor resulterar i ett fel.

Om du inte har tillgång till parametriserade frågor fortsätter du till [ta bort eller inaktivera ett schema](#delete-schedule) -avsnitt.

### Ange parametrar för en schemalagd parametriserad fråga {#set-parameters}

>[!IMPORTANT]
>
>Funktionen för parametriserat frågegränssnitt är för närvarande tillgänglig i en **Endast begränsad version** och inte är tillgängligt för alla kunder.

Om du skapar en schemalagd fråga för en parametriserad fråga måste du nu ange parametervärden för dessa frågekörningar.

![Avsnittet Schemainformation i arbetsflödet för schemaskapande med avsnittet Frågeparametrar markerat.](../images/ui/query-schedules/scheduled-query-parameter.png)

När du har bekräftat alla dessa uppgifter väljer du **[!UICONTROL Save]** för att skapa ett schema. Du återgår till arbetsytan för scheman som innehåller information om det nya schemat, inklusive schema-ID, själva schemat och schemats utdatamängd. Du kan använda schema-ID för att söka efter mer information om körningarna av själva den schemalagda frågan. Läs mer i [guide för körningsslutpunkter för schemalagda frågor](../api/runs-scheduled-queries.md).

![Arbetsytan för scheman med det nya schemat markerat.](../images/ui/query-schedules/schedules-workspace.png)

## Ta bort eller inaktivera ett schema {#delete-schedule}

Du kan ta bort eller inaktivera ett schema från arbetsytan Scheman för en viss fråga eller från [!UICONTROL Scheduled Queries] arbetsyta som visar alla schemalagda frågor.

Så här öppnar du [!UICONTROL Schedules] -fliken för den valda frågan måste du välja namnet på en frågemall från antingen [!UICONTROL Templates] eller [!UICONTROL Scheduled Queries] -fliken. Detta navigerar till frågeredigeraren för den frågan. I frågeredigeraren väljer du **[!UICONTROL Schedules]** för att komma åt arbetsytan för scheman.

Välj ett schema bland raderna i tillgängliga scheman. Du kan använda växlingsknappen för att inaktivera eller aktivera den schemalagda frågan.

>[!IMPORTANT]
>
>Du måste inaktivera schemat innan du kan ta bort ett schema för en fråga.

Välj **[!UICONTROL Delete a schedule]** om du vill ta bort det inaktiverade schemat.

![Arbetsytan för scheman med Inaktivera schema och Ta bort schema markerat.](../images/ui/query-schedules/delete-schedule.png)

Alternativt kan du [!UICONTROL Scheduled Queries] På -fliken finns en samling med infogade åtgärder för varje schemalagd fråga. De tillgängliga textbundna åtgärderna omfattar [!UICONTROL Disable schedule] eller [!UICONTROL Enable schedule], [!UICONTROL Delete schedule]och [!UICONTROL Subscribe] till aviseringar för den schemalagda frågan. Fullständiga anvisningar om hur du tar bort eller inaktiverar en schemalagd fråga via fliken Schemalagda frågor finns i [guide för övervakning av schemalagd fråga](./monitor-queries.md#inline-actions).
