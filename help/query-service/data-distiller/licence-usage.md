---
title: Övervaka användning av batchfrågelicens
description: Adobe Experience Platform användargränssnitt innehåller en kontrollpanel där du kan visa viktig information om hur din organisation använder din Data Distiller-licens.
source-git-commit: 74175e5e2ce31427ef6ea8d93055d6ca3a8406f4
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Övervaka användning av batchfrågelicens {#monitor-license-usage}

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

![Kontrollpanelen för licensanvändning med widgeten Beräkna timmar markerad.](../images/data-distiller/compute-hours.png)
