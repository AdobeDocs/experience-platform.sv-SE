---
title: Frågescheman
description: Lär dig hur du automatiserar schemalagda frågekörningar, tar bort eller inaktiverar ett frågeschema och använder tillgängliga schemaläggningsalternativ via Adobe Experience Platform-gränssnittet.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Frågescheman

Du kan automatisera frågekörningar genom att skapa frågescheman. Schemalagda frågor körs på en anpassad cache för att hantera dina data baserat på frekvens, datum och tid. Du kan också välja en utdatamängd för dina resultat om det behövs. Frågor som har sparats som en mall kan schemaläggas från Frågeredigeraren.

>[!IMPORTANT]
>
>Nedan följer en lista över begränsningar för schemalagda frågor när du använder Frågeredigeraren. De gäller inte för [!DNL Query Service] API:<br/>Du kan bara lägga till ett schema i en fråga som redan har skapats, sparats och körts.<br/>Du **inte** lägga till ett schema i en parametriserad fråga.<br/>Schemalagda frågor **inte** innehåller ett anonymt block.

Alla schemalagda frågor läggs till i listan i [!UICONTROL Scheduled queries] -fliken. Från den arbetsytan kan du övervaka statusen för alla schemalagda frågejobb via gränssnittet. På [!UICONTROL Scheduled queries] kan du hitta viktig information om frågekörningar och prenumerera på aviseringar. Den tillgängliga informationen omfattar status, schemainformation och felmeddelanden/koder om en körning misslyckas. Se [Övervaka dokument för schemalagda frågor](./monitor-queries.md) för mer information.

## Skapa frågescheman {#create-schedule}

Om du vill lägga till ett schema i en fråga väljer du en frågemall i [!UICONTROL Templates] -fliken eller [!UICONTROL Scheduled Queries] för att gå till Frågeredigeraren.

Läs mer om hur du lägger till scheman med API:t i [slutpunktsguide för schemalagda frågor](../api/scheduled-queries.md).

När en sparad fråga öppnas från Frågeredigeraren [!UICONTROL Schedules] -fliken visas under frågenamnet. Välj **[!UICONTROL Schedules]**.

![Frågeredigeraren med fliken Scheman markerad.](../images/ui/query-schedules/schedules-tab.png)

Arbetsytan för scheman visas. Välj **[!UICONTROL Add Schedule]** för att skapa ett schema.

![Arbetsytan Schemaläggning i frågeredigeraren med Lägg till schema markerat.](../images/ui/query-schedules/add-schedule.png)

Sidan med schemainformation visas. På den här sidan kan du välja frekvens för den schemalagda frågan, start- och slutdatum, veckodag som den schemalagda frågan ska köras samt vilken datamängd som frågan ska exporteras till.

![Panelen Schemainformation är markerad.](../images/ui/query-schedules/schedule-details.png)

Du kan välja följande alternativ för **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: Den schemalagda frågan kommer att köras varje timme för den datumperiod du har valt.
- **[!UICONTROL Daily]**: Den schemalagda frågan kommer att köras var X:e dag vid den tidpunkt och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Weekly]**: Den valda frågan körs på de veckodagar, tidpunkter och datumperioder som du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Monthly]**: Den valda frågan kommer att köras varje månad på den dag, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Yearly]**: Den valda frågan kommer att köras varje år på den dag, månad, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.

För utdatauppsättningen kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

>[!IMPORTANT]
>
> Eftersom du använder en befintlig eller skapar en ny datauppsättning gör du det **not** måste innehålla antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av frågan, eftersom datauppsättningarna redan har angetts. Inklusive antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av dina schemalagda frågor resulterar i ett fel.

När du har bekräftat alla dessa uppgifter väljer du **[!UICONTROL Save]** för att skapa ett schema. Du återgår till arbetsytan för scheman som innehåller information om det nya schemat, inklusive schema-ID, själva schemat och schemats utdatamängd. Du kan använda schema-ID för att söka efter mer information om körningarna av själva den schemalagda frågan. Läs mer i [guide för körningsslutpunkter för schemalagda frågor](../api/runs-scheduled-queries.md).

![Arbetsytan för scheman med det nya schemat markerat.](../images/ui/query-schedules/schedules-workspace.png)

## Ta bort eller inaktivera ett schema {#delete-schedule}

Du kan ta bort eller inaktivera ett schema från arbetsytan för scheman. Du måste välja en frågemall i [!UICONTROL Templates] -fliken eller [!UICONTROL Scheduled Queries] för att gå till Frågeredigeraren och välja **[!UICONTROL Schedule]** för att komma åt arbetsytan för scheman.

Välj ett schema bland raderna i tillgängliga scheman. Du kan använda växlingsknappen för att inaktivera eller aktivera den schemalagda frågan.

>[!IMPORTANT]
>
>Du måste inaktivera schemat innan du kan ta bort ett schema för en fråga.

Välj **[!UICONTROL Delete a schedule]** om du vill ta bort det inaktiverade schemat.

![Arbetsytan för scheman med Inaktivera schema och Ta bort schema markerat.](../images/ui/query-schedules/delete-schedule.png)


