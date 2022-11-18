---
title: Övervaka användning av batchfrågelicens
description: Adobe Experience Platform användargränssnitt innehåller en kontrollpanel där du kan visa viktig information om hur din organisation använder din Data Distiller-licens.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: 9d543b5c7c7f39e809b6a13b8adc46b9a99f51c7
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# (Beta) Övervaka användningen av batchfrågelicenser {#monitor-license-usage}

>[!IMPORTANT]
>
>Möjligheten att övervaka användningen av batchfrågelicenser via användargränssnittet är i betaversionen. Dess funktioner och dokumentation kan komma att ändras.

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om användningen av frågetjänstens licens.

Detaljerade instruktioner om hur du får åtkomst till och interagerar med kontrollpanelen för licensanvändning i användargränssnittet, samt hur du får mer information om tillgängliga mätvärden som visas på kontrollpanelen, finns på [kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md).

Läs [översikt över instrumentpaneler](../../dashboards/home.md) om du vill se en sammanfattning av alla panelfunktioner i Experience Platform.

## Widgetar {#widgets}

Kontrollpanelen för licensanvändning består av widgetar som visar skrivskyddade mått med viktig information om organisationens licensanvändning. Vilka mätvärden som visas beror på organisationens specifika licensiering.

Välj en alternativknapp för att välja en sandlåda för analys och använd listrutan för att välja en tidsperiod för analysen. De tillgängliga alternativen är 30 dagar, 90 dagar, 12 månader, det sista året, den fullständiga avtalsperioden eller ett anpassat datum.

## Beräkningstimmar {#compute-hours}

The [!UICONTROL Compute hours] widgeten använder ett linjediagram för att visualisera organisationens batchbearbetningstid varje dag. Widgeten visar tre mätvärden som anges av en siffra i den övre vänstra delen av widgeten. Dessa är

- [!UICONTROL Actual]: Det totala antalet beräkningstimmar för den tidsperiod som valts i översiktslistrutan. Det här måttet anges också i diagrammet med en heldragen linje.
- [!UICONTROL Licensed]: Det totala antalet arbetstimmar som tillåts av din organisations licensavtal. Det här måttet visas också i diagrammet med en prickad linje.
- [!UICONTROL Usage]: Detta är procentandelen av din användning i förhållande till den maximala beräkningstid som licensen tillåter.

>[!IMPORTANT]
>
>The [!UICONTROL Compute hours] widgeten gäller endast för kunder som har Data Distiller-licens för batchfrågor.

![Kontrollpanelen för licensanvändning med widgeten för beräknade timmar markerad.](../images/data-distiller/compute-hours.png)
