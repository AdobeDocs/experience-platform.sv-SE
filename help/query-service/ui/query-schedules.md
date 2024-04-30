---
title: Frågescheman
description: Lär dig hur du automatiserar schemalagda frågekörningar, tar bort eller inaktiverar ett frågeschema och använder tillgängliga schemaläggningsalternativ via Adobe Experience Platform-gränssnittet.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8d307b9c1c80c7b1672f2bf6b7acb4b85c4dae1b
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 0%

---

# Frågescheman

Du kan automatisera frågekörningar genom att skapa frågescheman. Schemalagda frågor körs på en anpassad cache för att hantera dina data baserat på frekvens, datum och tid. Du kan också välja en utdatamängd för dina resultat om det behövs. Frågor som har sparats som en mall kan schemaläggas från Frågeredigeraren.

>[!IMPORTANT]
>
>Du kan bara lägga till ett schema i en fråga som redan har skapats, sparats och körts.

Alla schemalagda frågor läggs till i listan i [!UICONTROL Scheduled queries] -fliken. Från den arbetsytan kan du övervaka statusen för alla schemalagda frågejobb via gränssnittet. På [!UICONTROL Scheduled queries] kan du hitta viktig information om frågekörningar och prenumerera på aviseringar. Den tillgängliga informationen omfattar status, schemainformation och felmeddelanden/koder om en körning misslyckas. Se [Övervaka dokument för schemalagda frågor](./monitor-queries.md) för mer information.

Det här arbetsflödet omfattar schemaläggningsprocessen i användargränssnittet för frågetjänsten. Läs mer om hur du lägger till scheman med API:t i [slutpunktsguide för schemalagda frågor](../api/scheduled-queries.md).

## Skapa ett frågeschema {#create-schedule}

Om du vill schemalägga en fråga väljer du en frågemall i [!UICONTROL Templates] eller [!UICONTROL Template] kolumn i [!UICONTROL Scheduled Queries] -fliken. Om du väljer mallnamnet kommer du till frågeredigeraren.

Om du öppnar en sparad fråga från Frågeredigeraren kan du skapa ett schema för frågan eller visa frågans schema från informationspanelen.

>[!TIP]
>
>Välj **[!UICONTROL View schedule]** om du vill navigera till arbetsytan för scheman och se en översikt över schemalagda frågor.

![Frågeredigeraren med [!UICONTROL View schedule] och [!UICONTROL Add schedule] markerad.](../images/ui/query-schedules/view-add-schedule.png)

Välj **[!UICONTROL Add schedule]** navigera till [sida med schemainformation](#schedule-details).

Du kan även välja **[!UICONTROL Schedules]** -fliken under frågans namn.

![Frågeredigeraren med fliken Scheman markerad.](../images/ui/query-schedules/schedules-tab.png)

Arbetsytan för scheman visas. Gränssnittet visar en lista över schemalagda körningar som mallen är kopplad till. Välj **[!UICONTROL Add Schedule]** för att skapa ett schema.

![Arbetsytan Schemaläggning i frågeredigeraren med Lägg till schema markerat.](../images/ui/query-schedules/add-schedule.png)

### Lägg till schemainformation {#schedule-details}

Sidan med schemainformation visas. På den här sidan kan du redigera olika detaljer för den schemalagda frågan. Information om [frekvens och veckodag för den schemalagda frågan](#scheduled-query-frequency) kör, start- och slutdatum, datauppsättningen som resultaten ska exporteras till och [fråga om statusaviseringar](#alerts-for-query-status).

![Panelen Schemainformation är markerad.](../images/ui/query-schedules/schedule-details.png)

#### Schemalagd frågefrekvens {#scheduled-query-frequency}

Du kan välja följande alternativ för **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: Den schemalagda frågan körs varje timme för den datumperiod du har valt.
- **[!UICONTROL Daily]**: Den schemalagda frågan kommer att köras var X:e dag vid den tidpunkt och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Weekly]**: Den valda frågan körs på veckodagarna, tidsperioden och den datumperiod som du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Monthly]**: Den valda frågan körs varje månad på den dag, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.
- **[!UICONTROL Yearly]**: Den valda frågan kommer att köras varje år på den dag, månad, tid och den datumperiod du har valt. Observera att den valda tiden är **UTC** och inte din lokala tidszon.

### Ange datauppsättningsinformation {#dataset-details}

Hantera frågeresultaten genom att antingen lägga till data i en befintlig datauppsättning eller skapa en ny datauppsättning och lägga till data i den.

Välj **[!UICONTROL Create and append into new dataset]** om du vill skapa en datauppsättning när du kör en fråga för första gången. Efterföljande körningar fortsätter att infoga data i datauppsättningen. Ange slutligen ett namn och en beskrivning för datauppsättningen.

>[!IMPORTANT]
>
> Eftersom du använder en befintlig eller skapar en ny datauppsättning gör du det **not** måste innehålla antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av frågan, eftersom datauppsättningarna redan har angetts. Inklusive antingen `INSERT INTO` eller `CREATE TABLE AS SELECT` som en del av dina schemalagda frågor resulterar i ett fel.

![Panelen Schemainformation med datauppsättningsinformation och [!UICONTROL Create and append into new dataset] alternativen är markerade.](../images/ui/query-schedules/dataset-details-create-and-append.png)

Du kan också välja **[!UICONTROL Append into existing dataset]** följt av datamängdsikonen (![Datamängdikonen.](../images/ui/query-schedules/dataset-icon.png)).

![Panelen Schemainformation med datauppsättningsinformation och Lägg till i befintlig datauppsättning markerad.](../images/ui/query-schedules/dataset-details-existing.png)

The **[!UICONTROL Select output dataset]** visas.

Därefter kan du antingen bläddra bland befintliga datauppsättningar eller använda sökfältet för att filtrera alternativen. Markera den rad i datauppsättningen som du vill använda. Datauppsättningsinformationen visas i panelen till höger. Välj **[!UICONTROL Done]** för att bekräfta ditt val.

![Dialogrutan Välj utdatamängd med sökfältet, en datamängdsrad och Klar markerat.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Karantänfrågor om de kontinuerligt misslyckas {#quarantine}

När du skapar ett schema kan du registrera din fråga i karantänfunktionen för att skydda systemresurser och förhindra eventuella störningar. karantänfunktionen identifierar och isolerar automatiskt frågor som misslyckas upprepade gånger genom att placera dem i en [!UICONTROL Quarantined] tillstånd. Genom att sätta frågor i karantän efter tio på varandra följande misslyckanden kan du ingripa, granska och åtgärda problem innan du tillåter fler körningar. Detta bidrar till att upprätthålla er effektivitet och dataintegritet.

![Arbetsytan Frågor och scheman med [!UICONTROL Query Quarantine] markerat och Ja markerat.](../images/ui/query-schedules/quarantine-enroll.png)

När en fråga har registrerats för karantänfunktionen kan du prenumerera på aviseringar för den här frågestatusändringen. Om en schemalagd fråga inte är registrerad i karantän visas den inte som ett alternativ på [dialogrutan Varningar](./monitor-queries.md#alert-subscription).

Du kan även registrera en schemalagd fråga i karantänfunktionen från de infogade åtgärderna i [!UICONTROL Scheduled Queries] -fliken. Se [dokumentation för bildskärmsfrågor](./monitor-queries.md#alert-subscription) för mer information.

### Ange aviseringar för status för en schemalagd fråga {#alerts-for-query-status}

Du kan även prenumerera på frågeararm som en del av inställningarna för den schemalagda frågan. Det innebär att du får meddelanden om statusändringar för din fråga. Varningar kan tas emot som popup-meddelanden eller e-postmeddelanden. De tillgängliga varningsalternativen för frågans tillstånd är bland annat start, lyckad och misslyckad. Markera kryssrutan om du vill prenumerera på aviseringar om den schemalagda frågans status.

![Panelen Schemaläggningsinformation med varningsalternativen markerade.](../images/ui/query-editor/alerts.png)

En översikt över varningar i Adobe Experience Platform, inklusive strukturen för hur varningsregler definieras, finns i [varningsöversikt](../../observability/alerts/overview.md). Vägledning om hur du hanterar aviseringar och varningsregler i Adobe Experience Platform-gränssnittet finns i [Användargränssnittshandbok för aviseringar](../../observability/alerts/ui.md).

### Ange parametrar för en schemalagd parametriserad fråga {#set-parameters}

>[!IMPORTANT]
>
>Funktionen för parametriserat frågegränssnitt är för närvarande tillgänglig i en **Endast begränsad version** och inte är tillgängligt för alla kunder. Om du inte har tillgång till parametriserade frågor fortsätter du till [ta bort eller inaktivera ett schema](#delete-schedule) -avsnitt.

Om du skapar en schemalagd fråga för en parametriserad fråga måste du nu ange parametervärden för dessa frågekörningar.

![Avsnittet Schemainformation i arbetsflödet för schemaskapande med avsnittet Frågeparametrar markerat.](../images/ui/query-schedules/scheduled-query-parameter.png)

När du har bekräftat din schemainformation väljer du **[!UICONTROL Save]** för att skapa ett schema. Du återgår till mallens flik för scheman. På den här arbetsytan visas information om det nya schemat, inklusive schema-ID, själva schemat och schemats utdatamängd.

## Visa schemalagda frågekörningar {#scheduled-query-runs}

Från mallens [!UICONTROL Schedules] väljer du schema-ID för att navigera till listan med frågekörningar för den nyligen schemalagda frågan.

![Arbetsytan för scheman med det nya schemat markerat.](../images/ui/query-schedules/schedules-workspace.png)

Om du vill visa en lista över en frågemalls schemalagda körningar går du till **[!UICONTROL Scheduled queries]** och välj ett mallnamn i listan.

![Fliken Schemalagda frågor med en namngiven mall markerad.](../images/ui/query-schedules/view-scheduled-runs.png)

Listan över frågekörningar för den schemalagda frågan visas.

![Informationsavsnittet på arbetsytan för schemalagda frågor med en lista över frågekörningar markerade för en schemalagd fråga.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Se [guide för övervakning av schemalagd fråga](./monitor-queries.md#inline-actions) om du vill ha fullständig information om hur du övervakar statusen för alla frågejobb via användargränssnittet.

Välj en **[!UICONTROL Query run ID]** i listan för att navigera till frågekörningsöversikten. För en fullständig uppdelning av den information som finns tillgänglig på [översikt över frågekörning](./monitor-queries.md#query-run-overview)finns i dokumentationen för övervakningsplanerade frågor.

Om du vill övervaka schemalagda frågor med hjälp av API:t för frågetjänsten läser du [guide för körningsslutpunkter för schemalagda frågor](../api/runs-scheduled-queries.md).

## Aktivera, inaktivera eller ta bort ett schema {#delete-schedule}

Du kan aktivera, inaktivera eller ta bort ett schema från arbetsytan Scheman för en viss fråga eller från [!UICONTROL Scheduled Queries] arbetsyta som visar alla schemalagda frågor.

Så här öppnar du [!UICONTROL Schedules] -fliken för den valda frågan måste du välja namnet på en frågemall från antingen [!UICONTROL Templates] eller [!UICONTROL Scheduled Queries] -fliken. Detta navigerar till frågeredigeraren för den frågan. I frågeredigeraren väljer du **[!UICONTROL Schedules]** för att komma åt arbetsytan för scheman.

Välj ett schema bland raderna med tillgängliga scheman för att fylla i informationspanelen. Använd växlingsknappen för att inaktivera (eller aktivera) den schemalagda frågan.

### Ta bort inaktiverade frågor

>[!IMPORTANT]
>
>Du måste inaktivera schemat innan du kan ta bort ett schema för en fråga.

![Listan över en malls scheman med informationspanelen markerad.](../images/ui/query-schedules/schedule-details-panel.png)

En bekräftelsedialogruta visas. Välj **[!UICONTROL Disable]** för att bekräfta åtgärden.

![Bekräftelsedialogrutan Inaktivera schema.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Välj **[!UICONTROL Delete a schedule]** om du vill ta bort det inaktiverade schemat.

![Arbetsytan för scheman med Ta bort schema markerat.](../images/ui/query-schedules/delete-schedule.png)

Alternativt kan du [!UICONTROL Scheduled Queries] På -fliken finns en samling med infogade åtgärder för varje schemalagd fråga. De tillgängliga textbundna åtgärderna omfattar [!UICONTROL Disable schedule] eller [!UICONTROL Enable schedule], [!UICONTROL Delete schedule]och [!UICONTROL Subscribe] till aviseringar för den schemalagda frågan. Fullständiga anvisningar om hur du tar bort eller inaktiverar en schemalagd fråga via fliken Schemalagda frågor finns i [guide för övervakning av schemalagd fråga](./monitor-queries.md#inline-actions).
