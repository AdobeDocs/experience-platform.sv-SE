---
keywords: Experience Platform;home;popular topics; delete dataflows
description: På arbetsytan för källor kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade.
solution: Experience Platform
title: Ta bort dataflöden
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Ta bort dataflöden i användargränssnittet

På arbetsytan kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade. [!UICONTROL Sources]

I den här självstudiekursen beskrivs hur du tar bort dataflöden med hjälp av [!UICONTROL Sources] arbetsytan.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
- [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Ta bort dataflöden

I användargränssnittet [för](https://platform.adobe.com)Experience Platform väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att få åtkomst till [!UICONTROL Sources] arbetsytan och väljer sedan **[!UICONTROL Dataflows]** i den övre rubriken.

![katalog](../../images/tutorials/delete/catalog.png)

Sidan visas **[!UICONTROL Dataflows]** . På den här sidan finns en lista med visningsbara dataflöden, inklusive information om måldatauppsättningen, källan, kontonamnet och datumet då de skapades.

Välj filterikonen (![filterikonen](../../images/tutorials/delete/filter.png)) längst upp till vänster för att öppna sorteringspanelen.

![dataflöden](../../images/tutorials/delete/dataflows.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att få tillgång till ett filtrerat urval av dataflöden som är kopplade till de särskilda källor du valde.

Välj den källa som du vill arbeta med för att visa en lista över befintliga dataflöden. När du har identifierat dataflödet som du vill ta bort markerar du ellipserna (`...`) bredvid dataflödets namn.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

En listruta visas med alternativ för att redigera dataflödets schema, inaktivera dataflödet eller ta bort det helt.

Välj **[!UICONTROL Delete]** att ta bort dataflödet.

![delete](../../images/tutorials/delete/delete.png)

En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![bekräfta](../../images/tutorials/delete/confirm.png)

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att borttagningen lyckades.

![bekräftad](../../images/tutorials/delete/confirmed.png)

## Nästa steg

I den här självstudiekursen har du använt arbetsytan för att ta bort ett befintligt dataflöde [!UICONTROL Sources] .

I självstudiekursen om hur du [tar bort dataflöden med API:t](../../tutorials/api/delete-dataflows.md) för Flow Service finns anvisningar om hur du utför dessa åtgärder programmatiskt med API-anrop.