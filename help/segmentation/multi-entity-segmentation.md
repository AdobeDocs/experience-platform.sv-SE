---
solution: Experience Platform
title: Översikt över segmentering av flera enheter
description: Multientitetssegmentering är möjligheten att utöka profildata med ytterligare data baserat på produkter, butiker eller andra icke-profilklasser. När de är anslutna blir data från ytterligare klasser tillgängliga som om de vore inbyggda i profilschemat.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Översikt över segmentering av flera enheter

Flerenhetssegmentering är en avancerad funktion som ingår i Adobe Experience Platform [!DNL Segmentation Service]. Med den här funktionen kan du utöka [!DNL Real-Time Customer Profile] data med ytterligare&quot;icke-persondata&quot; (kallas även&quot;dimensionsenheter&quot;) som din organisation kan definiera, t.ex. data relaterade till produkter eller butiker. Segmentering för flera enheter ger flexibilitet när det gäller att definiera segmentdefinitioner baserat på data som är relevanta för era unika affärsbehov och kan utföras utan att ni behöver ha expertis inom databaser. Med segmentering av flera enheter kan du lägga till nyckeldata till segmentdefinitionerna utan att behöva göra kostsamma ändringar i dataströmmar eller vänta på en datasammanfogning.

## Komma igång

Segmentering på flera enheter kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som är involverade i segmentering. Läs följande dokumentation innan du fortsätter med den här guiden:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserat på aggregerade data från flera källor.
   * [Profilskyddsutkast](../profile/guardrails.md): Bästa tillvägagångssätt för att skapa datamodeller som stöds av [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Används för att bygga målgrupper utifrån [!DNL Real-Time Customer Profile] data.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../xdm/schema/composition.md#union): Lär dig de bästa sätten att skapa scheman som ska användas i Experience Platform. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../xdm/schema/best-practices.md).

## Användningsfall

För att illustrera värdet av segmentering av flera enheter bör du överväga tre vanliga användningsfall för marknadsföring som illustrerar utmaningarna i de flesta marknadsföringsprogram:

### Kombinera inköpsdata online och offline

En marknadsförare som har byggt upp en e-postkampanj kan ha försökt att skapa en målgrupp genom att använda de senaste kundbutikerna de senaste tre månaderna. Helst skulle den här målgruppen behöva både artikelnamnet och namnet på butiken där köpet gjordes. Tidigare hade utmaningen varit att hämta butiksidentifieraren från inköpshändelsen och tilldela den till en enskild kundprofil.

### Återmarknadsföring via e-post för övergivna varukorgar

Det är komplicerat att skapa och kvalificera användare i segmentdefinitioner för att få kundvagnen att sluta. Att veta vilka produkter som ska ingå i en personaliserad återannonskampanj kräver uppgifter om vilka produkter som övergetts av varje enskild person. Dessa data är kopplade till e-handelshändelser som tidigare krävde en utmaning att övervaka och extrahera data från.

## Skapa segmentdefinitioner för flera enheter

Om du vill skapa en segmentdefinition för flera enheter måste du definiera relationer mellan scheman innan du använder [!DNL Segmentation] API eller segmentbyggargränssnitt för att skapa segmentdefinitionen.

### Definiera relationer

Att definiera relationer inom strukturen för era XDM-scheman (Experience Data Model) är en viktig del av att skapa segment för flera enheter. För relationer måste fältet i målet markeras som den primära identiteten för det schemat. En identitet kan bara markeras på strängar och kan inte markeras på arrayer. Dessutom behöver relationer inte nödvändigtvis vara en-till-en, eftersom du kan koppla profiler och uppleva händelser till flera mål.

Du kan definiera relationer antingen med API:t för schemaregister eller med schemaredigeraren. Välj bland följande självstudiekurser för detaljerade steg som visar hur du definierar en relation mellan två scheman:

* [Definiera en relation mellan två scheman med API:t](../xdm/tutorials/relationship-api.md)
* [Definiera en relation mellan två scheman med hjälp av gränssnittet i Schemaredigeraren](../xdm/tutorials/relationship-ui.md)

### Skapa en segmentdefinition för flera enheter

När du har definierat de nödvändiga XDM-relationerna kan du börja skapa en segmentdefinition för flera enheter. Detta kan göras antingen med segmenterings-API:t eller segmentbyggargränssnittet. Mer information finns i följande handböcker:

* [Skapa en segmentdefinition med segmenterings-API](./tutorials/create-a-segment.md)
* [Skapa en segmentdefinition med hjälp av gränssnittet i segmentbyggaren](./ui/overview.md)

## Utvärdera och få tillgång till segmentdefinitioner för flera enheter

När du har skapat en segmentdefinition kan du utvärdera och komma åt resultaten med segmenterings-API:t. Utvärderingen av en segmentdefinition som består av flera enheter påminner mycket om utvärderingen av en standardsegmentdefinition. Den här processen kan bara utföras med segmenterings-API:t. En detaljerad guide som visar hur du använder API:t för att utvärdera och komma åt segmentdefinitioner finns i [utvärdera och komma åt segmentdefinitioner](./tutorials/evaluate-a-segment.md) självstudie.
