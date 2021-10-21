---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Importera och använda externa målgrupper
description: Följ den här självstudiekursen för att lära dig hur du använder externa målgrupper med Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# Importera och använda externa målgrupper

Adobe Experience Platform har stöd för import av externa målgrupper, som sedan kan användas som komponenter för en ny segmentdefinition. Det här dokumentet innehåller en självstudiekurs om hur du konfigurerar Experience Platform för att importera och använda externa målgrupper.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika [!DNL Adobe Experience Platform] tjänster som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Segmenteringstjänst](../home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Kundprofil i realtid](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).
- [Datauppsättningar](../../catalog/datasets/overview.md): Konstruktionen för lagring och hantering av databeständighet i Experience Platform.
- [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Hur Experience Platform importerar och lagrar data från klient- och serverenheter i realtid.

### Segmentdata kontra segmentmetadata

Innan du börjar importera och använda externa målgrupper är det viktigt att förstå skillnaden mellan segmentdata och segmentmetadata.

Segmentdata avser de profiler som uppfyller kriterierna för att kvalificera segment, och är därför en del av målgruppen.

Metadata för segment är information om själva segmentet, som innehåller namn, beskrivning, uttryck (om tillämpligt), datum då segmentet skapades, datum för senaste ändring och ett ID. ID:t länkar segmentmetadata till de enskilda profiler som uppfyller segmentkvalificeringen och är en del av den slutliga målgruppen.

| Segmentdata | Segmentmetadata |
| ------------ | ---------------- |
| Profiler som uppfyller kraven för segment | Information om själva segmentet |

## Skapa ett identitetsnamnutrymme för den externa målgruppen

Det första steget för att använda externa målgrupper är att skapa ett identitetsnamnutrymme. Med identitetsnamnutrymmen kan plattformen associera varifrån ett segment kommer.

Följ instruktionerna i [guide för identitetsnamnutrymme](../../identity-service/namespaces.md#manage-namespaces). När du skapar ditt identitetsnamnutrymme lägger du till källinformationen i identitetsnamnutrymmet och markerar dess [!UICONTROL Type] som **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Skapa ett schema för segmentmetadata

När du har skapat ett identitetsnamnutrymme måste du skapa ett nytt schema för det segment som du ska skapa.

Börja med att välja **[!UICONTROL Schemas]** i det vänstra navigeringsfältet, följt av **[!UICONTROL Create schema]** i det övre högra hörnet av arbetsytan Scheman. Här väljer du **[!UICONTROL Browse]** om du vill se ett fullständigt urval av tillgängliga schematyper.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Eftersom du skapar en segmentdefinition, som är en fördefinierad klass, väljer du **[!UICONTROL Use existing class]**. Nu väljer du **[!UICONTROL Segment definition]** klass, följt av **[!UICONTROL Assign class]**.

![](../images/tutorials/external-audiences/assign-class.png)

Nu när schemat har skapats måste du ange vilket fält som ska innehålla segment-ID:t. Det här fältet bör markeras som primär identitet och tilldelas de namnutrymmen som du skapade tidigare.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

När du har markerat `_id` som primär identitet väljer du schemats titel, följt av växlingens etikett **[!UICONTROL Profile]**. Välj **[!UICONTROL Enable]** för att aktivera schemat för [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Det här schemat är nu aktiverat för profilen, med den primära identifieringen tilldelad till det icke-personliga ID-namnområdet som du skapade. Detta innebär att segmentmetadata som importeras till plattformen med det här schemat kommer att importeras till profilen utan att sammanfogas med andra personrelaterade profildata.

## Skapa en datauppsättning för schemat

När du har konfigurerat schemat måste du skapa en datauppsättning för segmentets metadata.

Om du vill skapa en datauppsättning följer du instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#create). Du kommer att följa **[!UICONTROL Create dataset from schema]** med det schema som du skapade tidigare.

![](../images/tutorials/external-audiences/select-schema.png)

När du har skapat datauppsättningen fortsätter du att följa instruktionerna i [användarhandbok för datauppsättning](../../catalog/datasets/user-guide.md#enable-profile) för att aktivera den här datauppsättningen för kundprofil i realtid.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Konfigurera och importera målgruppsdata

När datauppsättningen är aktiverad kan data nu skickas till plattformen antingen via användargränssnittet eller med Experience Platform API:er. Om du vill importera dessa data till plattformen måste du skapa en direktuppspelningsanslutning.

Om du vill skapa en direktuppspelningsanslutning följer du instruktionerna i [API, genomgång](../../sources/tutorials/api/create/streaming/http.md) eller [Självstudiekurs om användargränssnitt](../../sources/tutorials/ui/create/streaming/http.md).

När du har skapat en direktuppspelningsanslutning får du tillgång till din unika slutpunkt för direktuppspelning som du kan skicka data till. Läs mer om hur du skickar data till dessa slutpunkter i [självstudiekurs om att direktuppspela postdata](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Skapa segment med importerade målgrupper

När de importerade målgrupperna har konfigurerats kan de användas som en del av segmenteringsprocessen. Om du vill hitta externa målgrupper går du till segmentbyggaren och väljer **[!UICONTROL Audiences]** i **[!UICONTROL Fields]** -avsnitt.

![](../images/tutorials/external-audiences/external-audiences.png)

## Nästa steg

Nu när ni kan använda externa målgrupper i era segment kan ni använda segmentverktyget för att skapa segment. Läs mer om hur du skapar segment i [självstudiekurs om hur du skapar segment](./create-a-segment.md).
