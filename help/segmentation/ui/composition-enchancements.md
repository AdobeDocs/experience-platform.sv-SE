---
title: Förbättringar av målgruppssammansättning
description: Läs om förbättringarna i Audience Composition med målgruppsberikning och snabbare aktivering.
hide: true
hidefromtoc: true
source-git-commit: 065990790307124e0992731139abe9641a742a1b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Förbättringar av målgruppssammansättning

Du har nu tillgång till **två**-förbättringar för Audience Composition:

- [Målgruppsberikning](#audience-enrichment)
- [Snabbare aktivering](#faster-activation)

## Målgruppsberikning {#audience-enrichment}

Med målgruppsutveckling kan du ta fram en array med värden som gör att dina profiler kan kvalificera sig för den målgrupp du skapat.

Om du vill lägga till fler målgrupper i kompositionen markerar du det översta **[!UICONTROL Audience]**-blocket på arbetsytan. När målgruppen har fått ett namn väljer du **[!UICONTROL Build rule]** för att öppna regelbyggararbetsytan.

![Målgruppsblocket är markerat, liksom knappen Bygg regel.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

Linjalens arbetsyta visas. Nu kan du skapa filtervillkor för målgruppsberikning. Det här filtervillkoret **måste** innehålla ett attribut som finns i en array. Attributet som är en array beror på organisationens schemastruktur. När du har skapat filtervillkoren väljer du **[!UICONTROL Delivery]** på den högra panelen.

![Regelbyggararbetsytan visar ett exempel på en målgrupp som kan ha berikande funktioner. Knappen Leverans är också markerad.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Välj den objektarray som du vill använda för berikning i listan till vänster. Om det bara finns en array i profilen markeras arrayen automatiskt. Välj **[!UICONTROL Save]** om du vill återgå till målgruppsdisposition.

<!-- , as well as the fields you want to be used in the enrichment. -->

![Schematrädet för anrikningsträdet visas.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Inom målgruppssammansättningen är ditt [!UICONTROL Audience]-block nu av typen [!UICONTROL Rule builder with enhancement]. Välj **[!UICONTROL Publish]** om du vill aktivera målgruppen med nästa dagliga batch.

![Målgruppsblocket är markerat, vilket visar att en målgrupp med berikning har lagts till.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Beteendedetaljer och skyddsutkast

Tänk på följande när du använder målgruppsberikning:

- Du kan bara använda målgruppsberikning inom målgrupper som skapats i Audience Composition
- Det första blocket som används i kompositionen **måste** vara en regelbaserad målgrupp.
- Du **kan inte** använda några andra åtgärder i kompositionen.
- När du har publicerat **kan du inte** redigera kompositionen på den regelbaserade målgruppen.

   - Du *kan* kopiera kompositionen till ett utkast och redigera utkastet om du vill ändra baskompositionen eller regelbaserade målgrupper.

- Endast **en**-objektmatris kan användas för att generera anrikningsnyttolasten inom en enskild målgrupp

   - Nyttolastarrayen kan kapslas i ett objekt (upp till sju lager i profilschemat), men **kan inte** finnas i en annan array.
   - Nyttolastmatrisen **måste** ha 50 eller färre rader.
   - Alla kolumnutdata i nyttolasten **måste** vara av primitiv typ.
   - Endast de första **tjugo** kolumnerna i arrayen returneras.

- Endast **tio** publikkompositioner är tillgängliga för användning för tillfället

## Snabbare aktivering {#faster-activation}

Snabbare aktivering gör att ni kan aktivera er målgrupp till en nedladdningsbar målgrupp direkt efter att kompositionen har utvärderats. Om målet är inställt på att aktiveras efter segmentutvärderingen behöver du alltså inte längre vänta i 24 timmar på att utvärderingsjobbet ska slutföras.

Mer information finns i guiden [Aktivera målgrupper för batchprofiler](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
