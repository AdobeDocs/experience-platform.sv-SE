---
keywords: Experience Platform;hemmabruk;populära ämnen; ta bort dataflöden
description: På arbetsytan för källor kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade.
solution: Experience Platform
title: Ta bort dataflöden i användargränssnittet
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Ta bort dataflöden i användargränssnittet

The [!UICONTROL Sources] Med arbetsytan kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade.

I den här självstudiekursen beskrivs hur du tar bort dataflöden med [!UICONTROL Sources] arbetsyta.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
- [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

## Ta bort dataflöden

I [Experience Platform UI](https://platform.adobe.com), markera **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsytan och välj **[!UICONTROL Dataflows]** i det övre sidhuvudet.

![katalog](../../images/tutorials/delete/catalog.png)

The **[!UICONTROL Dataflows]** visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om måldatauppsättningen, källan, kontonamnet och datumet då de skapades.

Markera filterikonen (![filter-icon](../../images/tutorials/delete/filter.png)) längst upp till vänster för att öppna sorteringspanelen.

![dataflöden](../../images/tutorials/delete/dataflows.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att få tillgång till ett filtrerat urval av dataflöden som är kopplade till de särskilda källor du valde.

Välj den källa som du vill arbeta med för att visa en lista över de befintliga dataflödena. När du har identifierat det dataflöde du vill ta bort markerar du ellipserna (`...`) bredvid dataflödets namn.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

En listruta visas med alternativ för att redigera dataflödets schema, inaktivera dataflödet eller ta bort det helt.

Välj **[!UICONTROL Delete]** för att ta bort dataflödet.

![delete](../../images/tutorials/delete/delete.png)

En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![bekräfta](../../images/tutorials/delete/confirm.png)

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att borttagningen lyckades.

![bekräftad](../../images/tutorials/delete/confirmed.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!UICONTROL Sources] arbetsyta för att ta bort ett befintligt dataflöde.

Se självstudiekursen om [ta bort dataflöden med API:t för Flow Service](../../tutorials/api/delete-dataflows.md) för steg om hur du utför dessa åtgärder programmatiskt med API-anrop.
