---
keywords: Experience Platform;insikter;kundinformation;populära ämnen;kundsegment
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Skapa kundsegment med prediktiva poäng
description: När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Skapa kundsegment med förutbestämda poäng

När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget. En mer robust självstudiekurs om hur du skapar segment finns i [Användarhandbok för Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om du vill använda den här metoden måste kundprofilen i realtid aktiveras för datauppsättningen.

I plattformsgränssnittet klickar du på **[!UICONTROL Segments]** i den vänstra navigeringen och klicka sedan på **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

The **Segment Builder** visas. Från vänster **[!UICONTROL Fields]** kolumn och under **[!UICONTROL Attributes]** klickar du på mappen med namnet **[!UICONTROL XDM Individual Profile]** och klicka sedan på mappen med organisationens namnområde. Mappen med namnet **[!UICONTROL Customer AI]** innehåller resultatet av prediktionskörningar och namnges efter den instans som poängen tillhör. Klicka på en instansmapp för att komma åt resultatet av den önskade instansen.

![](../images/user-guide/results.png)

I mitten av Segment Builder drar och släpper du **[!UICONTROL Score]** på *arbetsyta för regelbyggaren* för att definiera en regel.

Under höger hand *Segmentegenskaper* anger du ett namn för segmentet.

![](../images/user-guide/properties.png)

Ovanför vänster hand *Fält* klickar du på **växel** -ikonen och välj en *Kopplingsprincip* i listrutan. Klicka **[!UICONTROL Save]** för att skapa segmentet.

![](../images/user-guide/merge_policy.png)

## Nästa steg

Genom att följa den här självstudiekursen har du hittat målgrupper baserat på deras benägenhetspoäng med hjälp av segmentbyggaren. Nu kan ni inrikta er på era målgrupper genom att aktivera dem för destinationer. Se [destinationer, översikt](../../../destinations/home.md) för mer information.
