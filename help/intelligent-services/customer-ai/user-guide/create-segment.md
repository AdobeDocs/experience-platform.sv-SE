---
keywords: Experience Platform;insikter;kundinformation;populära ämnen;kundsegment
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Skapa kundsegment med prediktiva poäng
topic: Create a segment
description: När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Skapa kundsegment med förutbestämda poäng

När en förutsägelsekörning är klar används automatiskt förväntade benägenhetspoäng av profiler. Genom att förbättra profiler med kundens AI-poäng kan man skapa kundsegment för att hitta målgrupper baserat på deras benägenhetspoäng. I det här avsnittet beskrivs hur du skapar segment med hjälp av segmentverktyget. En mer robust självstudiekurs om hur du skapar segment finns i [användarhandboken för Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om du vill använda den här metoden måste kundprofilen i realtid aktiveras för datauppsättningen.

Klicka på **[!UICONTROL Segments]** i den vänstra navigeringen i plattformsgränssnittet och klicka sedan på **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

**Segmentbyggaren** visas. Klicka på mappen **[!UICONTROL Fields]** i den vänstra kolumnen och under fliken **[!UICONTROL Attributes]** och klicka sedan på mappen **[!UICONTROL XDM Individual Profile]** i namnområdet för din organisation. Mappen **[!UICONTROL Customer AI]** innehåller resultatet av förutsägelsekörningar och namnges efter instansen som poängen tillhör. Klicka på en instansmapp för att komma åt resultatet av den önskade instansen.

![](../images/user-guide/results.png)

Placerad i mitten av Segment Builder, dra och släpp attributet **[!UICONTROL Score]** på *regelbyggararbetsytan* för att definiera en regel.

Ange ett namn för segmentet under den högra kolumnen *Segmentegenskaper*.

![](../images/user-guide/properties.png)

Ovanför kolumnen *Fält* till vänster klickar du på ikonen **kugghjulet** och väljer en *sammanslagningsprincip* i listrutan. Klicka på **[!UICONTROL Save]** för att skapa segmentet.

![](../images/user-guide/merge_policy.png)

## Nästa steg

Genom att följa den här självstudiekursen har du hittat målgrupper baserat på deras benägenhetspoäng med hjälp av segmentbyggaren. Nu kan ni inrikta er på era målgrupper genom att aktivera dem för destinationer. Mer information finns i [målöversikten](../../../destinations/home.md).