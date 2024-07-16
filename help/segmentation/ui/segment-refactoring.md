---
solution: Experience Platform
title: Användargränssnittshandbok för tidsbegränsningar för motverkad segmentering
description: I Segment Builder finns en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Omfaktorisering av tidsbegränsningar {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Omfaktorisering av tidsbegränsningar"
>abstract="Tidsbegränsningar på regelnivå och gruppnivå har tagits bort för att förtydliga tidsbegränsningsanvändningen. Skriv om begränsningen som en tidsbegränsning på arbetsytans nivå eller på kortnivå."

Januari 2024-utgåvan av Adobe Experience Platform har gjort ändringar i Adobe Experience Platform Segmentation Service som lägger till nya begränsningar där tidsbegränsningar kan definieras. De här ändringarna påverkar nyligen skapade eller redigerade segment som har skapats med gränssnittet i segmentbyggaren. Den här guiden förklarar hur du kan mildra dessa ändringar.

Före januari 2024-versionen refererade alla tidsbegränsningar på regelnivå, gruppnivå och arbetsytenivå i hög grad till samma tidsstämpel. För att förtydliga tidsbegränsningsanvändningen har tidsbegränsningar på regelnivå och gruppnivå tagits bort. Om du vill hantera den här ändringen måste alla tidsbegränsningar **skrivas om som** Canvas-level **eller** card-level **.**

Tidigare kunde en enskild händelse ha flera bifogade tidsbegränsningsregler. Med den här senaste uppdateringen kommer försök att lägga till en tidsbegränsning i en regel nu att resultera i ett **fel**.

![Tidsbegränsningen på regelnivå är markerad. Det fel som sedan inträffar markeras också. ](../images/ui/segment-refactoring/rule-time-constraint.png)

Tidsbegränsningar kan nu bara tillämpas på arbetsytans eller kortets nivå.

När du tillämpar en tidsbegränsning på arbetsytans nivå kan du fortfarande välja alla tillgängliga tidsbegränsningar.

>[!NOTE]
>
>Om det bara finns **ett**-kort på arbetsytan är tidsbegränsningen för kortet **ekvivalent** att använda tidsbegränsningen på arbetsytans nivå.
>
>Om det finns **flera** kort på arbetsytan tillämpar du tidsbegränsningen på arbetsytans nivå på **alla** kort på arbetsytan.

![Tidsbegränsningen på arbetsytenivå är markerad.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Om du vill använda en tidsbegränsning på kortnivå väljer du det kort du vill använda tidsbegränsningen på. Behållaren **[!UICONTROL Event Rules]** visas. Nu kan du välja den tidsbegränsning som du vill tillämpa på kortet.

![Tidsbegränsningen på kortnivå är markerad.](../images/ui/segment-refactoring/card-time-constraint.png)
