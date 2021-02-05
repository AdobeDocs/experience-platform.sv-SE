---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;segmentbyggare;Segmentbyggare
solution: Experience Platform
title: Användargränssnittshandbok för tidsbegränsningar för motverkad segmentering
topic: ui guide
description: 'I Segment Builder finns en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Omfaktorisering av tidsbegränsningar

I oktober 2020-versionen av Adobe Experience Platform har prestandaändringar gjorts i Adobe Experience Platform Segmentation Service som lägger till nya begränsningar för användningen av operatorerna OR och AND. De här ändringarna påverkar nyligen skapade eller redigerade segment som har skapats med gränssnittet i segmentbyggaren. Den här guiden förklarar hur du kan mildra dessa ändringar.

Före oktober 2020-versionen refererade alla tidsbegränsningar på regelnivå, gruppnivå och händelsenivå i stor utsträckning till samma tidsstämpel. För att förtydliga tidsbegränsningsanvändningen har tidsbegränsningar på regelnivå och gruppnivå tagits bort. För att kunna hantera den här ändringen måste alla tidsbegränsningar skrivas om som tidsbegränsningar på händelsenivå.

Tidigare kunde en enskild händelse ha flera bifogade tidsbegränsningsregler.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Som du ser har det här segmentet två begränsningar på regelnivån: En för [!UICONTROL Today] och den andra för [!UICONTROL Yesterday].

Det föregående segmentet motsvarar följande segment - båda tidsbegränsningarna på händelsenivå har anslutits med operatorn AND. Den första tidsbegränsningen på händelsenivå refererar till en klickningshändelse vars namn är &quot;Utbildning&quot; och som inträffar idag, medan tidsbegränsningen på andra händelsenivå refererar till en klickhändelse vars namn är lika med &quot;Pets&quot; och inträffade i går.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Den här omfaktoriseringen av tidsbegränsningar påverkar också tidsbegränsningar som är kopplade med en OR-operator.