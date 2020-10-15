---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;data flows
description: Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du visar befintliga konton och dataflöden från arbetsytan Källor.
solution: Experience Platform
title: Övervaka konton och dataflöden
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 2514c282d16a1b6ddb2232e46e6283ab2ab3d356
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# Övervaka konton och dataflöden i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du visar befintliga konton och dataflöden från [!UICONTROL Sources] arbetsytan.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) System](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Övervaka konton

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa konton och dataflöden med. Varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Välj **[!UICONTROL Accounts]** i den övre rubriken om du vill visa befintliga konton.

![katalog](../../images/tutorials/monitor/catalog-accounts.png)

Sidorna **[!UICONTROL Accounts]** visas. På den här sidan finns en lista med visningsbara konton, inklusive information om källa, användarnamn, antal dataflöden och datum när de skapades.

Välj trattikonen längst upp till vänster för att starta sorteringsfönstret.

![konton](../../images/tutorials/monitor/accounts-list.png)

På sorteringspanelen kan du komma åt konton från en viss källa. Välj den källa du vill arbeta med och välj kontot i listan till höger.

>[!TIP]
>
> Använd ![spektrumkontrollknappen](../../images/tutorials/monitor/spectrum-control.png) i **[!UICONTROL Name]** kolumnen för att skapa ett nytt källdataflöde för det valda kontot.

![välj konton](../../images/tutorials/monitor/accounts-sort.png)

Dessutom kan du redigera befintlig kontoinformation och uppdatera dina kontoinloggningsuppgifter. Välj pennikonen för den kontoinformation som du vill redigera.

![](../../images/tutorials/monitor/click-edit.png)

Den **[!UICONTROL Edit account details]** modala visas. Från den här sidan kan du uppdatera din befintliga kontoinformation och autentiseringsuppgifter.

>[!NOTE]
>
> Det finns information om redigeringskonton för alla batchkällanslutningar.

![](../../images/tutorials/monitor/edit-account.png)

På **[!UICONTROL Accounts]** sidan kan du visa en lista över befintliga dataflöden eller måldatauppsättningar som är kopplade till kontot du har öppnat. Markera ellipsknappen (`...`) för att visa fler tillgängliga alternativ för det valda dataflödet. Dessa alternativ beskrivs närmare nedan:

| Kontroll | Beskrivning |
| ------- | ----------- |
| [!UICONTROL Edit schedule] | Gör att du kan redigera dataflödets intag. |
| [!UICONTROL Disable dataflow] | Gör att du kan inaktivera datainmatning för det valda dataflödet. |
| [!UICONTROL Delete] | Gör att du kan ta bort det markerade dataflödet. |

![dataflöden](../../images/tutorials/monitor/dataflows.png)

## Övervaka dataflöden

Dataflöden kan nås direkt från **[!UICONTROL Catalog]** sidan utan att visas **[!UICONTROL Accounts]**. Välj **[!UICONTROL Dataflows]** i den övre rubriken om du vill visa en lista med dataflöden.

![catalog-dataflows](../../images/tutorials/monitor/catalog-dataflows.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om källa, användarnamn, antal dataflöden och status.

Se följande tabell för mer information om status:

| Status | Beskrivning |
| ------ | ----------- |
| Aktiverad | Statusen anger att ett dataflöde är aktivt och att det hämtar data enligt det schema som det angavs. `Enabled` |
| Handikappade | Statusen anger att ett dataflöde är inaktivt och inte innehåller några data. `Disabled` |
| Bearbetar | Statusen visar att ett dataflöde ännu inte är aktivt. `Processing` Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` anger att aktiveringsprocessen för ett dataflöde har avbrutits. |

Välj trattsymbolen längst upp till vänster för att sortera.

![dataflows-list](../../images/tutorials/monitor/dataflows-list.png)

Sorteringspanelen visas. Välj den källa som du vill komma åt på rullningsmenyn och välj dataflödet i listan till höger. Du kan också markera ellipsknappen (`...`) för att visa fler tillgängliga alternativ för det valda dataflödet.

![sort-dataflows](../../images/tutorials/monitor/dataflows-sort.png)

Sidan innehåller information om hur många poster som har importerats och vilka poster som har misslyckats samt information om dataflödets status och bearbetningstid. **[!UICONTROL Dataflow activity]** Välj kalenderikonen ovanför dataflödet för att justera tidsramen för dina inmatningsposter.

![datflow-activity](../../images/tutorials/monitor/dataflow-activity.png)

I kalendern kan du visa olika tidsramar för inkapslade poster. Du kan välja ett av de två förinställda alternativen &quot;[!UICONTROL Last 7 days]&quot; eller &quot;[!UICONTROL Last 30 days]&quot;. Du kan också ange en anpassad tidsram i kalendern. Välj önskad tidsram och välj **[!UICONTROL Apply]** för att fortsätta.

![flödeskalender](../../images/tutorials/monitor/flow-calendar.png)

Som standard **[!UICONTROL Dataflow activity]** visas den **[!UICONTROL Properties]** panel som är associerad med dataflödet. Välj flödeskörningen i listan för att se tillhörande metadata, inklusive information om dess unika körnings-ID.

Välj **[!UICONTROL Dataflow run start]** för att komma åt **[!UICONTROL Dataflow run overview]**.

![körningar](../../images/tutorials/monitor/run-metadata.png)

Informationen **[!UICONTROL Dataflow run overview]** visas om dataflödet, inklusive dess metadata, status för partiellt intag och tilldelat feltröskelvärde. Den övre rubriken innehåller även en felsammanfattning. Den **[!UICONTROL Error summary]** innehåller det specifika felet på den översta nivån som visar i vilket steg som inmatningsprocessen påträffade ett fel.

![dataflow-run-overview](../../images/tutorials/monitor/dataflow-run-overview.png)

I följande tabell finns felen som du kan se i **[!UICONTROL Error summary]**.

| Fel | Beskrivning |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Ett fel uppstod när data kopierades från en källa. |
| `CONNECTOR-2001-500` | Ett fel uppstod när kopierade data bearbetades till [!DNL Platform]. Det här felet kan gälla parsning, validering eller omformning. |

Den nedre halvan av skärmen innehåller information om **[!UICONTROL Dataflow run errors]**. Härifrån kan du även visa de filer som har importerats, förhandsgranska och ladda ned feldiagnostik eller ladda ned filmanifestet.

I **[!UICONTROL Dataflow run errors]** avsnittet visas felkoden, antalet poster som misslyckades och information som beskriver felet.

Välj det här alternativet **[!UICONTROL Preview error diagnostics]** om du vill ha mer information om felet.

![Dataflödeskörningsfel](../../images/tutorials/monitor/dataflow-run-errors.png)

Panelen **[!UICONTROL Error diagnostics preview]** visas. På den här skärmen visas specifik information om felet i fråga, inklusive filnamn, felkod, namnet på den kolumn där felet inträffade samt en beskrivning av felet.

I det här avsnittet finns även en förhandsgranskning av kolumnen som innehåller felet.

>[!IMPORTANT]
>
>För att kunna aktivera måste **[!UICONTROL Error diagnostics preview]** du aktivera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]** när du konfigurerar ett dataflöde. Om du gör det kan systemet skanna alla poster som hämtas under flödeskörningen.

![Preview-error-diagnostics](../../images/tutorials/monitor/preview-error-diagnostics.png)

När du har förhandsgranskat felen kan du välja **[!UICONTROL Download]** från **[!UICONTROL dataflow runs overview]** panelen för att få tillgång till fullständig feldiagnostik och hämta filmanifestet. Mer information finns i dokumenten om [feldiagnostik](../../../ingestion/batch-ingestion/partial.md#retrieve-errors) och [hämtning av metadata](../../../ingestion/batch-ingestion/partial.md#download-metadata) .

![Preview-error-diagnostics](../../images/tutorials/monitor/download.png)

Mer information om övervakning av dataflöden och förtäring finns i självstudiekursen om [övervakning av dataflöden](../../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Nästa steg

Genom att följa den här självstudiekursen har du fått åtkomst till befintliga konton och dataflöden från **[!UICONTROL Sources]** arbetsytan. Inkommande data kan nu användas av [!DNL Platform] tjänster längre fram i kedjan som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../data-science-workspace/home.md)
