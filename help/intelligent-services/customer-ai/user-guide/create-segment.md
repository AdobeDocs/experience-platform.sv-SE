---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: Skapa kundsegment med förutbestämda poäng
topic: Create a segment
description: När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget.
translation-type: tm+mt
source-git-commit: d29f7c7243ec798abe60fff895b36277996cb4a0
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Skapa kundsegment med förutbestämda poäng

När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget. En mer robust självstudiekurs om hur du skapar segment finns i användarhandboken för [Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om du vill använda den här metoden måste kundprofilen i realtid aktiveras för datauppsättningen.

Klicka i det vänstra navigeringsfältet i Plattformsgränssnittet **[!UICONTROL Segments]** och klicka sedan på **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

Segmentbyggaren **** visas. I den vänstra **[!UICONTROL Fields]** kolumnen och under **[!UICONTROL Attributes]** fliken klickar du på mappen med namnet **[!UICONTROL XDM Individual Profile]** och sedan på mappen med organisationens namnområde. Mappen med namnet **[!UICONTROL Customer AI]** innehåller resultatet av prediktionskörningar och namnges efter instansen som poängen tillhör. Klicka på en instansmapp för att komma åt resultatet av den önskade instansen.

![](../images/user-guide/results.png)

Placerad i mitten av Segment Builder, dra och släpp **[!UICONTROL Score]** -attributet på *regelbyggarens arbetsyta* för att definiera en regel.

Ange ett namn för segmentet under den högra kolumnen *Segmentegenskaper* .

![](../images/user-guide/properties.png)

Ovanför den vänstra kolumnen *Fält* klickar du på **kugghjulsikonen** och väljer en *kopplingsprincip* i listrutan. Klicka **[!UICONTROL Save]** för att skapa segmentet.

![](../images/user-guide/merge_policy.png)

## Nästa steg

Genom att följa den här självstudiekursen har du hittat målgrupper baserat på deras benägenhetspoäng med hjälp av segmentbyggaren. Nu kan ni inrikta er på era målgrupper genom att aktivera dem för destinationer. Mer information finns i [destinationsöversikten](../../../destinations/home.md) .