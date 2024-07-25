---
keywords: Experience Platform;hem;populära ämnen; ta bort dataflöden
description: På arbetsytan för källor kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade.
solution: Experience Platform
title: Ta bort dataflöden i användargränssnittet
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Ta bort dataflöden i användargränssnittet

Med arbetsytan [!UICONTROL Sources] kan du ta bort befintliga grupper och strömmande dataflöden som innehåller fel eller har blivit föråldrade.

I den här självstudien beskrivs hur du tar bort dataflöden med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
- [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

## Ta bort dataflöden

I [Experience Platform-gränssnittet](https://platform.adobe.com) väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources] och sedan **[!UICONTROL Dataflows]** i den övre rubriken.

![katalog](../../images/tutorials/delete/catalog.png)

Sidan **[!UICONTROL Dataflows]** visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om måldatauppsättning, källa, kontonamn och datum när de skapades.

Välj filterikonen (![filter-icon](/help/images/icons/filter.png)) längst upp till vänster för att öppna sorteringspanelen.

![dataflöden](../../images/tutorials/delete/dataflows.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att få tillgång till ett filtrerat urval av dataflöden som är kopplade till de särskilda källor som du har valt.

Välj den källa som du vill arbeta med för att visa en lista över de befintliga dataflödena. När du har identifierat dataflödet som du vill ta bort markerar du ellipserna (`...`) bredvid dataflödets namn.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

En listruta visas med alternativ för att redigera dataflödets schema, inaktivera dataflödet eller ta bort det helt.

Välj **[!UICONTROL Delete]** om du vill ta bort dataflödet.

![delete](../../images/tutorials/delete/delete.png)

En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![bekräfta](../../images/tutorials/delete/confirm.png)

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att borttagningen lyckades.

![bekräftad](../../images/tutorials/delete/confirmed.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att ta bort ett befintligt dataflöde.

I självstudiekursen [Ta bort dataflöden med API:t för Flow Service ](../../tutorials/api/delete-dataflows.md) finns anvisningar om hur du utför dessa åtgärder programmatiskt med API-anrop.
