---
keywords: redigera aktivering, redigera mål, redigera mål
title: Redigera aktiveringsdataflöden
type: Tutorial
seo-title: Edit activation dataflows
description: Följ stegen i den här artikeln när du vill redigera ett befintligt aktiveringsdataflöde i Adobe Experience Platform.
seo-description: Follow the steps in this article to edit an existing activation dataflow in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 2d944c7bd237efbbd4a770b3a6dd03c4133bc901
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Redigera aktiveringsdataflöden {#edit-activation-flows}

I Adobe Experience Platform kan du redigera olika komponenter i befintliga aktiveringsdataflöden till mål, t.ex. exporterade segment och profilattribut, exportfrekvens, om aktiveringsdataflödet är aktiverat eller inaktiverat, med mera.

Följ stegen nedan för att redigera befintliga aktiveringsdataflöden:

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Browse]** i det övre sidhuvudet för att visa befintliga måldataflöden.

   ![Bläddra bland mål](../assets/ui/edit-activation/browse-destinations.png)

2. Markera filterikonen ![Filterikon](../assets/ui/edit-activation/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/edit-activation/filter-destinations.png)

3. Välj namnet på måldataflödet som du vill redigera.

   ![Välj mål](../assets/ui/edit-activation/destination-select.png)

4. The **[!UICONTROL Dataflow runs]** målsidan visas med de tillgängliga kontrollerna. Nu kan du redigera flera komponenter i måldataflödet:

   * Välj **[!UICONTROL Activate segments]** i den högra listen för att ändra vilka segment eller profilattribut som ska skickas till målet. Den här åtgärden tar dig till aktiveringsarbetsflödet, som skiljer sig åt beroende på måltyp. Mer information finns i stödlinjerna för:
      * [aktivera målgruppsdata till segmenterade direktuppspelningsmål](./activate-segment-streaming-destinations.md) (t.ex. Facebook eller Twitter)
      * [aktivera målgruppsdata till batchprofilbaserade mål](./activate-batch-profile-destinations.md) (t.ex. Amazon S3 eller Oracle Eloqua)
      * [aktivera målgruppsdata för direktuppspelning av profilbaserade mål](./activate-streaming-profile-destinations.md) (till exempel HTTP API eller Amazon Kinesis).
   * Dessutom kan du redigera namnet och beskrivningen för måldataflödet.
   * Du kan använda **[!UICONTROL Enabled]/[!UICONTROL Disabled]** växla för att starta och pausa all dataexport till målet.

   ![Destinationsinformation](../assets/ui/edit-activation/destination-details.png)

5. Se [Aktiveringsöversikt](activation-overview.md) om du vill ha mer information om hur du aktiverar nya segment för dina destinationer.
