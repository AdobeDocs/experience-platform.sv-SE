---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments
solution: Experience Platform
title: Segmentering för flera enheter
topic: overview
description: Multientitetssegmentering är möjligheten att utöka profildata med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i profilschemat.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Segmentering för flera enheter

Multientitetssegmentering är möjligheten att utöka [!DNL Profile] data med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i [!DNL Profile] schemat.

Om du vill veta mer om segmentering för flera enheter kan du fortsätta att läsa dokumentationen och komplettera din inlärning genom att titta på videon nedan eller utforska [segmenteringsöversikten](./home.md).]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som använder segmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [!DNL Real-time Customer Profile](../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [Adobe Experience Platform segmenteringstjänst](./home.md): Gör att ni kan bygga segment utifrån kundprofilen i realtid.
- [!DNL Experience Data Model (XDM)](../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

## Definiera XDM-relationer

Att definiera relationer med strukturen i dina [!DNL Experience Data Model] (XDM) scheman är en viktig och viktig del av att skapa segment.

Den här processen kan utföras antingen med [!DNL Schema Registry] API:t eller [!DNL Schema Editor]. En detaljerad guide om hur du använder API:t för att definiera en relation mellan två scheman finns [i självstudiekursen om hur du definierar en relation mellan två scheman med API](../xdm/tutorials/relationship-api.md). En detaljerad guide om hur du använder [!DNL Schema Editor] för att definiera en relation mellan två scheman finns [i självstudiekursen om hur du definierar en relation mellan två scheman med hjälp av Schemaredigeraren](../xdm/tutorials/relationship-ui.md).

## Så här skapar du segment som använder XDM-relationer

När du har definierat dina XDM-relationer kan du använda API:t för att skapa ett segment [!DNL Segmentation Service] .

Detta kan göras antingen med [!DNL Segmentation] API:t eller med [!DNL Segment Builder] användargränssnittet. En detaljerad guide om hur du använder API:t för att skapa ett segment finns [i självstudiekursen om hur du skapar ett segment med segmenterings-API](./tutorials/create-a-segment.md). En detaljerad guide om hur du använder Segment Builder för att skapa ett segment finns [i användarhandboken](./ui/overview.md)för Segment Builder.

## Så här utvärderar och får du tillgång till segment för flera enheter

När du har skapat ett segment kan du utvärdera och komma åt segmentresultaten med hjälp av [!DNL Segmentation Service] -API:t. Utvärderingen av ett segment med flera enheter påminner mycket om utvärderingen av ett reguljärt segment.

Den här processen kan bara utföras med API:t [!DNL Segmentation Service] . En detaljerad guide om hur du använder API för att utvärdera och få tillgång till segment finns i självstudiekursen om [utvärdering och åtkomst av segment](./tutorials/evaluate-a-segment.md).