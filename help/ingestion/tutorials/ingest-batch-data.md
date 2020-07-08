---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Infoga data i Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---


# Infoga data i Adobe Experience Platform

Med Adobe Experience Platform kan du enkelt importera data till Platform som gruppfiler. Exempel på data som ska importeras kan vara profildata från en platt fil i ett CRM-system (t.ex. en parquet-fil) eller data som överensstämmer med ett känt XDM-schema (Experience Data Model) i schemaregistret.

## Komma igång

Du måste ha tillgång till Experience Platform för att kunna slutföra den här självstudiekursen. Om du inte har tillgång till en IMS-organisation i Experience Platform, tala med systemadministratören innan du fortsätter.

Om du föredrar att importera data med hjälp av API:er för datainmatning börjar du med att läsa [Utvecklarhandboken](../batch-ingestion/api-overview.md)för gruppinmatning.

## Arbetsytan Datauppsättningar

På arbetsytan Datauppsättningar i Experience Platform kan du visa och hantera alla datauppsättningar som din IMS-organisation har skapat, samt skapa nya.

Visa arbetsytan Datauppsättningar genom att klicka på **Datauppsättningar** i den vänstra navigeringen. Arbetsytan Datauppsättningar innehåller en lista med datauppsättningar, inklusive kolumner som visar _Namn_, _Skapad_ (datum och tid), _Källa_, _Schema_ och _Senaste gruppstatus___, samt datum och tid då datauppsättningen uppdaterades¥Last Updated¥.

>[!NOTE]
>
>Klicka på filterikonen bredvid sökfältet för att använda filterfunktioner för att visa endast de datauppsättningar som har aktiverats för profilen.

![Visa alla datauppsättningar](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Skapa en datauppsättning

Om du vill skapa en datauppsättning klickar du på **Skapa datauppsättning** i det övre högra hörnet av arbetsytan Datauppsättningar.

På skärmen **Skapa datauppsättning** väljer du om du vill skapa datauppsättning från schema eller Skapa datauppsättning från CSV-fil.

I den här självstudiekursen används ett schema för att skapa datauppsättningen. Klicka på **Skapa datauppsättning från schema** för att fortsätta.

![Välj datakälla](../images/tutorials/ingest-batch-data/create_dataset.png)

## Välj dataschema

På skärmen **Välj schema** väljer du ett schema genom att klicka på alternativknappen bredvid det schema du vill använda. För den här självstudiekursen görs datauppsättningen med hjälp av schemat Förmånsmedlemmar. Att använda sökfältet för att filtrera scheman är ett praktiskt sätt att hitta exakt det schema du söker.

När du har markerat alternativknappen bredvid schemat som du vill använda klickar du på **Nästa**.

![Välj schema](../images/tutorials/ingest-batch-data/select_schema.png)

## Konfigurera datauppsättning

På skärmen **Konfigurera datauppsättning** måste du ge datauppsättningen ett **namn** och kan även ge en **beskrivning** av datauppsättningen.

**Kommentarer om datauppsättningsnamn:**

- Datauppsättningsnamnen ska vara korta och beskrivande så att datauppsättningen kan hittas i biblioteket senare.
- Datauppsättningsnamnen måste vara unika, vilket innebär att de också måste vara tillräckligt specifika för att de inte ska återanvändas i framtiden.
- Det är bäst att ge ytterligare information om datauppsättningen med hjälp av beskrivningsfältet, eftersom det kan hjälpa andra användare att skilja mellan datauppsättningar i framtiden.

När datauppsättningen har ett namn och en beskrivning klickar du på **Slutför**.

![Konfigurera datauppsättning](../images/tutorials/ingest-batch-data/configure_dataset.png)

## Datauppsättningsaktivitet

En tom datauppsättning har nu skapats och du har återgått till fliken **Datauppsättningsaktivitet** på arbetsytan Datauppsättningar. Du bör se namnet på datauppsättningen i det övre vänstra hörnet av arbetsytan, tillsammans med ett meddelande om att&quot;Inga grupper har lagts till&quot;. Detta förväntas eftersom du inte har lagt till några batchar i den här datauppsättningen än.

Till höger på arbetsytan Datauppsättningar visas fliken **Info** med information om din nya datauppsättning, till exempel _datauppsättnings-ID_, _namn_, _beskrivning_, _tabellnamn_______,¥Schema,¥Streaming¥ och¥Source¥. Fliken Info innehåller även information om när datauppsättningen _skapades_ och dess _senaste ändrade_ datum.

På fliken Info finns också en _profilväxel_ som används för att aktivera datauppsättningen för användning med kundprofil i realtid. Användning av den här växeln och kundprofilen i realtid förklaras mer ingående i det följande avsnittet.

![Datauppsättningsaktivitet](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Aktivera datauppsättning för kundprofil i realtid

Datauppsättningar används för inmatning av data i Experience Platform, och dessa data används i slutändan för att identifiera individer och sammanfoga information från flera olika källor. Den sammanfogade informationen kallas kundprofil i realtid. För att Platform ska veta vilken information som ska ingå i realtidsprofilen kan datauppsättningar markeras för inkludering med **profilväxeln** .

Den här växlingen är som standard inaktiverad. Om du väljer att växla till Profil kommer alla data som hämtas in till datauppsättningen att användas för att identifiera en individ och sammanfoga deras realtidsprofil.

Mer information om kundprofil i realtid och hur du arbetar med identiteter finns i dokumentationen för [identitetstjänsten](../../identity-service/home.md) .

Om du vill aktivera datauppsättningen för kundprofil i realtid klickar du på **profilväxlingen** på fliken **Info** .

![Växla profil](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

En dialogruta visas där du ombeds bekräfta att du vill aktivera datauppsättningen för kundprofil i realtid.

![Dialogrutan Aktivera profil](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Klicka på **Aktivera** och växlingsknappen blir blå, vilket anger att den är aktiverad.

![Aktiverad för profil](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Lägg till data i datauppsättning

Data kan läggas till i en datauppsättning på flera olika sätt. Du kan välja att använda API:er för datainmatning eller en ETL-partner som Unifi eller Informatica. För den här självstudiekursen läggs data till i datauppsättningen med hjälp av fliken **Lägg till data** i användargränssnittet.

Klicka på fliken **Lägg till data** för att börja lägga till data i datauppsättningen. Nu kan du dra och släppa filer eller bläddra på datorn efter de filer du vill lägga till.

>[!NOTE]
>
>Platform har stöd för två filtyper för dataöverföring, parquet eller JSON. Du kan lägga till upp till fem filer i taget, där den maximala filstorleken för varje fil är 10 GB.

![Fliken Lägg till data](../images/tutorials/ingest-batch-data/add_data.png)

## Överföra en fil

När du drar och släpper (eller bläddrar och väljer) en parquet eller JSON-fil som du vill ladda upp, börjar Platform omedelbart att bearbeta filen och en dialogruta för **överföring** visas på fliken **Lägg till data** som visar filöverföringen.

![Överför dialogruta](../images/tutorials/ingest-batch-data/uploading.png)

## Datauppsättningsmått

När filen har laddats upp visar fliken **Datauppsättningsaktivitet** inte längre att&quot;Inga batchar har lagts till&quot;. I stället visas datamängdsmått på fliken Datauppsättningsaktivitet. Alla mätvärden visar &quot;0&quot; i det här skedet eftersom batchen ännu inte har lästs in.

Längst ned på fliken finns en lista med _batch-ID_ för de data som precis har importerats via processen [&quot;Lägg till data i datauppsättning&quot;](#add-data-to-dataset) . Här finns även information som rör batchen, inklusive _inkapslat_ datum, antal _poster som har kapslats_ och aktuell _batchstatus_.

![Datauppsättningsmått](../images/tutorials/ingest-batch-data/batch_loading.png)

## Batchinformation

Klicka på _batch-ID_ för att visa en **gruppöversikt** med ytterligare information om gruppen. När batchen har lästs in uppdateras informationen om batchen så att antalet _poster som har kapslats_ och _filstorleken_ visas. Status __ ändras också till Slutfört eller Misslyckat. Om batchen misslyckas innehåller avsnittet _Felkod_ detaljer om eventuella fel under importen.

Mer information och vanliga frågor om batchförbrukning finns i felsökningsguiden för [batchmatning](../batch-ingestion/troubleshooting.md).

Om du vill gå tillbaka till skärmen **Datauppsättningsaktivitet** klickar du på namnet på datauppsättningen (_bonusinformation_) i den synliga sökvägen.

![Gruppöversikt](../images/tutorials/ingest-batch-data/batch_overview.png)

## Förhandsgranska datauppsättning

När datauppsättningen är klar visas ett alternativ för att **förhandsgranska datauppsättningen** högst upp på fliken **Datauppsättningsaktivitet** .

Klicka på **Förhandsgranska datauppsättning** för att öppna en dialogruta med exempeldata inifrån datauppsättningen. Om datauppsättningen skapades med ett schema visas information om datauppsättningsschemat till vänster i förhandsgranskningen. Du kan expandera schemat med hjälp av pilarna för att se schemastrukturen. Varje kolumnrubrik i förhandsvisningsdata representerar ett fält i datauppsättningen.

![Information om datauppsättning](../images/tutorials/ingest-batch-data/dataset_details.png)

## Nästa steg

Nu när du har skapat en datauppsättning och kapslat in data i Experience Platform kan du upprepa de här stegen för att skapa en ny datauppsättning eller infoga fler data i den befintliga datauppsättningen.

Läs översikten över [batchförbrukning om du vill veta mer om batchförbrukning](../batch-ingestion/overview.md).
