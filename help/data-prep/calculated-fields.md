---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Dataförhandsgranskning
topic-legacy: overview
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 2cc72708b77396e70d006ecd1e21fd2d495ddf61
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---


# Beräknade fält

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till.

Om du vill skapa ett beräkningsfält väljer du **[!UICONTROL Add calculated field]**.

![](./images/calculated-fields/add-calculated-field.png)

Panelen **[!UICONTROL Create calculated field]** visas. Den vänstra dialogrutan innehåller de fält, funktioner och operatorer som stöds i beräkningsfält. Välj en av flikarna för att börja lägga till funktioner, fält eller operatorer i uttrycksredigeraren.

![](./images/calculated-fields/create-calculated-field.png)

| Tabb | Beskrivning |
| --- | ----------- |
|  -funktion | På fliken Funktioner visas de funktioner som är tillgängliga för att omforma data. Om du vill veta mer om de funktioner du kan använda i beräkningsfält kan du läsa guiden på [med hjälp av datapersonfunktioner (Mapper)](./functions.md). |
| Fält | Fliken Fält visar de fält och attribut som är tillgängliga i källschemat. |
| Operatör | På fliken Operatorer visas de operatorer som är tillgängliga för att omforma data. |

Du kan lägga till fält, funktioner och operatorer manuellt med uttrycksredigeraren i mitten. Välj redigeraren för att börja skapa ett uttryck.

![](./images/calculated-fields/write-calculated-field.png)

Välj **[!UICONTROL Save]** för att fortsätta.

Mappningsskärmen visas igen med det nya källfältet. Tillämpa motsvarande målfält och välj **[!UICONTROL Finish]** för att slutföra mappningen.

![](./images/calculated-fields/new-calculated-field.png)