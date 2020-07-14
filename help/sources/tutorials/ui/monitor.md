---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Övervaka och ta bort dataflöden
topic: overview
translation-type: tm+mt
source-git-commit: f08ad2c9cc48c08bcdc0e278481992e8789000b5
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Övervaka och ta bort dataflöden

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du visar befintliga konton och dataflöden från *[!UICONTROL Sources]* arbetsytan. I den här självstudiekursen beskrivs även hur du tar bort dataflöden från *[!UICONTROL Sources]* arbetsytan.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Övervaka konton

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa konton och dataflöden med. Varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Välj *[!UICONTROL Accounts]* i den övre rubriken om du vill visa befintliga konton.

![katalog](../../images/tutorials/monitor/catalog.png)

Sidorna *[!UICONTROL Accounts]* visas. På den här sidan finns en lista med visningsbara konton, inklusive information om källa, användarnamn, antal dataflöden och datum när de skapades.

Välj trattikonen längst upp till vänster för att starta sorteringsfönstret.

![konton](../../images/tutorials/monitor/accounts-list.png)

På sorteringspanelen kan du komma åt konton från en viss källa. Välj den källa du vill arbeta med och välj kontot i listan till höger.

![välj konton](../../images/tutorials/monitor/accounts-sort.png)

På *[!UICONTROL Accounts]* sidan kan du visa en lista över befintliga dataflöden som är kopplade till kontot du har öppnat. Välj det dataflöde som du vill visa.

![kontosida](../../images/tutorials/monitor/dataflows.png)

Skärmen visas *[!UICONTROL Dataflow activity]* . På den här sidan visas hur många meddelanden som används i form av ett diagram.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

## Övervaka dataflöden

Dataflöden kan nås direkt från *[!UICONTROL Catalog]* sidan utan att visas *[!UICONTROL Accounts]*. Välj *[!UICONTROL Dataflows]* i den övre rubriken om du vill visa en lista över befintliga dataflöden.

![catalog-dataflows](../../images/tutorials/monitor/catalog-dataflows.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om källa, användarnamn, antal dataflöden och status. Välj trattsymbolen längst upp till vänster för att sortera.

![dataflows-list](../../images/tutorials/monitor/dataflows-list.png)

Sorteringspanelen visas. Välj den källa som du vill komma åt på rullningsmenyn och välj dataflödet i listan till höger.

![sort-dataflows](../../images/tutorials/monitor/dataflows-sort.png)

Skärmen visas *[!UICONTROL Dataflow activity]* . På den här sidan visas hur många meddelanden som används i form av ett diagram.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

Mer information om övervakning av dataflöden och förtäring finns i självstudiekursen om [övervakning av dataflöden](../../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Ta bort ett dataflöde

Du kan ta bort dataflöden som har skapats felaktigt eller som inte längre är nödvändiga genom att gå till dataflödesskärmen. Leta reda på det dataflöde som du vill ta bort med hjälp av sorteringstrattsikonen och välj det dataflöde som du vill öppna **[!UICONTROL Properties]** panelen.

Om du vill ta bort ett dataflöde väljer du **[!UICONTROL Delete]** bland egenskaperna högst upp till höger.

![delete-dataflows](../../images/tutorials/monitor/dataflows-sort-delete.png)

Ett slutligt bekräftelsemeddelande visas. Bekräfta genom **[!UICONTROL Delete]** att klicka.

![bekräfta-ta bort](../../images/tutorials/monitor/confirm-delete.png)

Efter en stund visas en grön bekräftelseruta längst ned på skärmen som bekräftar att borttagningen lyckades.

![borttagningen lyckades](../../images/tutorials/monitor/deletion-confirmed.png)

Du kan också ta bort ett dataflöde från *[!UICONTROL Accounts]* skärmen. Leta reda på kontot som du vill komma åt med hjälp av sorteringstrattsikonen och välj kontot i listan.

![välj konton](../../images/tutorials/monitor/accounts-sort.png)

Sidan visas *[!UICONTROL Accounts]* . Markera det dataflöde som du vill ta bort och välj sedan **[!UICONTROL Delete]** från egenskapspanelen för att slutföra processen.

![konton-ta bort](../../images/tutorials/monitor/accounts-delete.png)

Slutför processen genom att följa de bekräftelsesteg som beskrivs ovan.

## Nästa steg

Genom att följa den här självstudiekursen har du fått åtkomst till befintliga konton och dataflöden från *[!UICONTROL Sources]* arbetsytan. Inkommande data kan nu användas av [!DNL Platform] tjänster längre fram i kedjan som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../data-science-workspace/home.md)