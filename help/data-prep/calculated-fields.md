---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Dataförhandsgranskning
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# Beräknade fält

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till.

Välj **[!UICONTROL Add calculated field]** om du vill skapa ett beräknat fält.

![](./images/calculated-fields/add-calculated-field.png)

Panelen **[!UICONTROL Create calculated field]** visas. Den vänstra dialogrutan innehåller de fält, funktioner och operatorer som stöds i beräkningsfält. Välj en av flikarna för att börja lägga till funktioner, fält eller operatorer i uttrycksredigeraren.

![](./images/calculated-fields/create-calculated-field.png)

| Tabb | Beskrivning |
| --- | ----------- |
| Funktion | På fliken Funktioner visas de funktioner som är tillgängliga för att omforma data. Om du vill veta mer om de funktioner du kan använda i beräknade fält kan du läsa guiden för [med hjälp av datapersonfunktioner (Mapper)](./functions.md). |
| Fält | Fliken Fält visar de fält och attribut som är tillgängliga i källschemat. |
| Operatör | På fliken Operatorer visas de operatorer som är tillgängliga för att omforma data. |

Du kan lägga till fält, funktioner och operatorer manuellt med uttrycksredigeraren i mitten. Välj redigeraren för att börja skapa ett uttryck.

![](./images/calculated-fields/write-calculated-field.png)

Välj **[!UICONTROL Save]** om du vill fortsätta.

Mappningsskärmen visas igen med det nya källfältet. Tillämpa motsvarande målfält och välj **[!UICONTROL Finish]** för att slutföra mappningen.

![](./images/calculated-fields/new-calculated-field.png)
