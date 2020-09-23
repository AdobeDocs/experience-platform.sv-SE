---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentering för flera enheter
topic: overview
description: Multientitetssegmentering är möjligheten att utöka profildata med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i profilschemat.
translation-type: tm+mt
source-git-commit: 4dd5a91146b116953ba180e3f39d24b4e1ec289e
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Segmentering för flera enheter

Segmentering för flera enheter är en avancerad funktion som ingår i Adobe Experience Platform [!DNL Segmentation Service]. Med den här funktionen kan du utöka [!DNL Real-time Customer Profile] data med ytterligare&quot;icke-persondata&quot; (kallas även&quot;dimensionsenheter&quot;) som din organisation kan definiera, till exempel data relaterade till produkter eller butiker. Multientitetssegmentering ger flexibilitet när det gäller att definiera målgruppssegment baserat på data som är relevanta för era unika affärsbehov och kan utföras utan att ni behöver ha expertis inom databaser. Med segmentering av flera enheter kan ni lägga till nyckeldata till era segment utan att behöva göra kostsamma ändringar i dataströmmar eller vänta på en datasammanfogning.

## Komma igång

Segmentering på flera enheter kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som är inblandade i segmentering. Läs följande dokumentation innan du fortsätter med den här guiden:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
   * [Profilskyddsutkast](../profile/guardrails.md): Bästa tillvägagångssätt för att skapa datamodeller som stöds av [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmenteringstjänst]](./home.md): Gör att ni kan skapa segment utifrån [!DNL Real-time Customer Profile] data.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../xdm/schema/composition.md#union): Lär dig de bästa sätten att skapa scheman som ska användas i Experience Platform.

## Användningsfall

För att illustrera värdet av segmentering av flera enheter bör du överväga tre vanliga användningsfall för marknadsföring som illustrerar utmaningarna i de flesta marknadsföringsprogram:

### Kombinera inköpsdata online och offline

En marknadsförare som har skapat en e-postkampanj kan ha försökt att skapa ett segment för en målgrupp genom att använda de senaste kundbutikerna de senaste tre månaderna. Helst skulle det här segmentet kräva både artikelnamnet och namnet på butiken där köpet gjordes. Tidigare hade utmaningen varit att hämta butiksidentifieraren från inköpshändelsen och tilldela den till en enskild kundprofil.

### Återmarknadsföring via e-post för övergivna varukorgar

Det är ofta komplicerat att skapa och kvalificera användare i segment där kundvagnen överges. Att veta vilka produkter som ska ingå i en personaliserad återannonskampanj kräver uppgifter om vilka produkter som övergetts av varje enskild person. Dessa data är kopplade till e-handelshändelser som tidigare krävde en utmaning att övervaka och extrahera data från.

## Skapa segment med flera enheter

Om du vill skapa ett segment med flera enheter först måste du definiera relationerna mellan scheman innan du använder gränssnittet för [!DNL Segmentation] API eller segmentbyggaren för att skapa segmentdefinitionen.

### Definiera relationer

Att definiera relationer inom strukturen för era XDM-scheman (Experience Data Model) är en viktig del av att skapa segment för flera enheter. För relationer måste fältet i målet markeras som den primära identiteten för det schemat. En identitet kan bara markeras på strängar och kan inte markeras på arrayer. Dessutom behöver relationer inte nödvändigtvis vara en-till-en, eftersom du kan koppla profiler och uppleva händelser till flera mål.

Du kan definiera relationer antingen med API:t för schemaregister eller med schemaredigeraren. Välj bland följande självstudiekurser för detaljerade steg som visar hur du definierar en relation mellan två scheman:

* [Definiera en relation mellan två scheman med API:t](../xdm/tutorials/relationship-api.md)
* [Definiera en relation mellan två scheman med hjälp av gränssnittet i Schemaredigeraren](../xdm/tutorials/relationship-ui.md)

### Skapa ett segment med flera enheter

När du har definierat de nödvändiga XDM-relationerna kan du börja skapa ett segment med flera enheter. Detta kan göras antingen med segmenterings-API:t eller segmentbyggargränssnittet. Mer information finns i följande handböcker:

* [Skapa ett segment med segmenterings-API](./tutorials/create-a-segment.md)
* [Skapa ett segment med hjälp av gränssnittet i segmentbyggaren](./ui/overview.md)

## Utvärdera och få tillgång till segment med flera enheter

När du har skapat ett segment kan du utvärdera och komma åt segmentresultaten med segmenterings-API:t. Utvärderingen av ett segment med flera enheter påminner mycket om utvärderingen av ett standardsegment. Den här processen kan bara utföras med segmenterings-API:t. Om du vill ha en detaljerad guide om hur du använder API för att utvärdera och få tillgång till segment kan du läsa självstudiekursen [Utvärdera och få tillgång till segment](./tutorials/evaluate-a-segment.md) .
