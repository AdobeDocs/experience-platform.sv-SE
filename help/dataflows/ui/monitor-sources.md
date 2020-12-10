---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du visar befintliga dataflöden från arbetsytan Källor.
solution: Experience Platform
title: Övervaka dataflöden
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4d99526a592e173e3b46e1fa2a3f869b1fe5d4f2
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---


# Övervaka dataflöden för källor i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du visar befintliga dataflöden från [!UICONTROL Sources] arbetsytan.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../sources/home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Övervaka dataflöden

Logga in i användargränssnittet [för](https://platform.adobe.com) Experience Platform och välj sedan **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt [!UICONTROL Sources] arbetsytan. Välj **[!UICONTROL Dataflows]** i den övre rubriken om du vill visa befintliga dataflöden.

![catalog-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om källa, användarnamn, antal dataflöden och status.

Se följande tabell för mer information om status:

| Status | Beskrivning |
| ------ | ----------- |
| Aktiverad | Statusen anger att ett dataflöde är aktivt och att det hämtar data enligt det schema som det angavs. `Enabled` |
| Handikappade | Statusen anger att ett dataflöde är inaktivt och inte innehåller några data. `Disabled` |
| Bearbetar | Statusen visar att ett dataflöde ännu inte är aktivt. `Processing` Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` anger att aktiveringsprocessen för ett dataflöde har avbrutits. |

Välj trattsymbolen längst upp till vänster för att sortera.

![dataflows-list](../assets/ui/monitor-sources/dataflows-list.png)

Sorteringspanelen visas. Välj den källa som du vill komma åt på rullningsmenyn och välj dataflödet i listan till höger. Du kan också markera ellipsknappen (`...`) för att visa fler tillgängliga alternativ för det valda dataflödet.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

Sidan innehåller information om hur många poster som har importerats och vilka poster som har misslyckats samt information om dataflödets status och bearbetningstid. **[!UICONTROL Dataflow activity]** Välj kalenderikonen ovanför dataflödet för att justera tidsramen för dina inmatningsposter.

![datflow-activity](../assets/ui/monitor-sources/dataflow-activity.png)

I kalendern kan du visa olika tidsramar för inkapslade poster. Du kan välja ett av de två förinställda alternativen &quot;[!UICONTROL Last 7 days]&quot; eller &quot;[!UICONTROL Last 30 days]&quot;. Du kan också ange en anpassad tidsram i kalendern. Välj önskad tidsram och välj **[!UICONTROL Apply]** för att fortsätta.

![flödeskalender](../assets/ui/monitor-sources/flow-calendar.png)

Som standard **[!UICONTROL Dataflow activity]** visas den **[!UICONTROL Properties]** panel som är associerad med dataflödet. Välj flödeskörningen i listan för att se tillhörande metadata, inklusive information om dess unika körnings-ID.

Välj **[!UICONTROL Dataflow run start]** för att komma åt **[!UICONTROL Dataflow run overview]**.

![körningar](../assets/ui/monitor-sources/run-metadata.png)

Informationen **[!UICONTROL Dataflow run overview]** visas om dataflödet, inklusive dess metadata, status för partiellt intag och tilldelat feltröskelvärde. Den övre rubriken innehåller även en felsammanfattning. Den **[!UICONTROL Error summary]** innehåller det specifika felet på den översta nivån som visar i vilket steg som inmatningsprocessen påträffade ett fel.

![dataflow-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

I följande tabell finns felen som du kan se i **[!UICONTROL Error summary]**.

| Fel | Beskrivning |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Ett fel uppstod när data kopierades från en källa. |
| `CONNECTOR-2001-500` | Ett fel uppstod när kopierade data bearbetades till [!DNL Platform]. Det här felet kan gälla parsning, validering eller omformning. |

Den nedre halvan av skärmen innehåller information om **[!UICONTROL Dataflow run errors]**. Härifrån kan du även visa de filer som har importerats, förhandsgranska och ladda ned feldiagnostik eller ladda ned filmanifestet.

I **[!UICONTROL Dataflow run errors]** avsnittet visas felkoden, antalet poster som misslyckades och information som beskriver felet.

Välj det här alternativet **[!UICONTROL Preview error diagnostics]** om du vill ha mer information om felet.

![Dataflödeskörningsfel](../assets/ui/monitor-sources/dataflow-run-errors.png)

Panelen **[!UICONTROL Error diagnostics preview]** visas. På den här skärmen visas specifik information om felet i fråga, inklusive filnamn, felkod, namnet på den kolumn där felet inträffade samt en beskrivning av felet.

I det här avsnittet finns även en förhandsgranskning av kolumnen som innehåller felet.

>[!IMPORTANT]
>
>För att kunna aktivera måste **[!UICONTROL Error diagnostics preview]** du aktivera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]** när du konfigurerar ett dataflöde. Om du gör det kan systemet skanna alla poster som hämtas under flödeskörningen.

![Preview-error-diagnostics](../assets/ui/monitor-sources/preview-error-diagnostics.png)

När du har förhandsgranskat felen kan du välja **[!UICONTROL Download]** från **[!UICONTROL dataflow runs overview]** panelen för att få tillgång till fullständig feldiagnostik och hämta filmanifestet. Mer information finns i dokumenten om [feldiagnostik](../../ingestion/batch-ingestion/partial.md#retrieve-errors) och [hämtning av metadata](../../ingestion/batch-ingestion/partial.md#download-metadata) .

![Preview-error-diagnostics](../assets/ui/monitor-sources/download.png)

Mer information om övervakning av dataflöden och förtäring finns i självstudiekursen om [övervakning av dataflöden](../../ingestion/quality/monitor-data-ingestion.md)för direktuppspelning.

## Nästa steg

Genom att följa den här självstudiekursen har du fått åtkomst till befintliga konton och dataflöden från **[!UICONTROL Sources]** arbetsytan. Inkommande data kan nu användas av [!DNL Platform] tjänster längre fram i kedjan som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md)
