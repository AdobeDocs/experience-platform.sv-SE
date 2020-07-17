---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentering för flera enheter
topic: overview
translation-type: tm+mt
source-git-commit: f44e42a4faa3b10f147dbaf929048054ce0bec42
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Segmentering för flera enheter

Multientitetssegmentering är möjligheten att utöka profildata med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i profilschemat.

Om du vill veta mer om segmentering för flera enheter kan du fortsätta att läsa dokumentationen och komplettera din inlärning genom att titta på videon nedan eller utforska [segmenteringsöversikten](./home.md).]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för segmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [Segmenteringstjänsten](./home.md)Adobe Experience Platform: Gör att ni kan bygga segment utifrån kundprofilen i realtid.
- [Experience Data Model (XDM)](../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.

## Definiera XDM-relationer

Att definiera relationer med strukturen i era XDM-scheman (Experience Data Model) är en viktig och viktig del av att skapa segment.

Den här processen kan utföras antingen med API:t för schemaregister eller med Schemaredigeraren. En detaljerad guide om hur du använder API:t för att definiera en relation mellan två scheman finns [i självstudiekursen om hur du definierar en relation mellan två scheman med API](../xdm/tutorials/relationship-api.md). Om du vill ha en detaljerad guide om hur du använder Schemaredigeraren för att definiera en relation mellan två scheman kan du läsa [självstudiekursen om hur du definierar en relation mellan två scheman med Schemaredigeraren](../xdm/tutorials/relationship-ui.md).

## Så här skapar du segment som använder XDM-relationer

När du har definierat dina XDM-relationer kan du använda segmenteringstjänstens API för att skapa ett segment.

Detta kan göras antingen med segmenterings-API:t eller segmentbyggargränssnittet. En detaljerad guide om hur du använder API:t för att skapa ett segment finns [i självstudiekursen om hur du skapar ett segment med segmenterings-API](./tutorials/create-a-segment.md). En detaljerad guide om hur du använder Segment Builder för att skapa ett segment finns [i användarhandboken](./ui/overview.md)för Segment Builder.

## Så här utvärderar och får du tillgång till segment för flera enheter

När du har skapat ett segment kan du utvärdera och komma åt segmentresultaten med hjälp av [!DNL Segmentation Service] -API:t. Utvärderingen av ett segment med flera enheter påminner mycket om utvärderingen av ett reguljärt segment.

Den här processen kan bara utföras med API:t [!DNL Segmentation Service] . En detaljerad guide om hur du använder API för att utvärdera och få tillgång till segment finns i självstudiekursen om [utvärdering och åtkomst av segment](./tutorials/evaluate-a-segment.md).