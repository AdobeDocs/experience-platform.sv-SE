---
keywords: redigera aktivering, redigera mål, redigera mål
title: Redigera aktiveringsdataflöden
type: Tutorial
description: Följ stegen i den här artikeln när du vill redigera ett befintligt aktiveringsdataflöde i Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Redigera aktiveringsdataflöden {#edit-activation-flows}

I Adobe Experience Platform kan du redigera olika komponenter i befintliga aktiveringsdataflöden till mål, t.ex. exporterade målgrupper och profilattribut, exportfrekvens, om aktiveringsdataflödet är aktiverat eller inaktiverat, med mera.

## Redigera dataflöden {#edit-dataflows}

Följ stegen nedan för att redigera befintliga aktiveringsdataflöden:

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Browse]** i det övre sidhuvudet för att visa befintliga måldataflöden.

   ![Bläddra bland mål](../assets/ui/edit-activation/browse-destinations.png)

2. Markera filterikonen ![Filterikon](../assets/ui/edit-activation/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/edit-activation/filter-destinations.png)

3. Välj namnet på måldataflödet som du vill redigera.

   ![Välj mål](../assets/ui/edit-activation/destination-select.png)

4. The **[!UICONTROL Dataflow runs]** målsidan visas med de tillgängliga kontrollerna. Nu kan du redigera flera komponenter i måldataflödet:

   * Välj **[!UICONTROL Activate audiences]** till höger för att ändra vilka målgrupper eller profilattribut som ska skickas till målet. Den här åtgärden tar dig till aktiveringsarbetsflödet, som skiljer sig åt beroende på måltyp. Mer information finns i stödlinjerna för:
      * [aktivera målgruppsdata till målgruppsdirektuppspelningsmål](./activate-segment-streaming-destinations.md) (t.ex. Facebook eller Twitter)
      * [aktivera målgruppsdata till batchprofilbaserade mål](./activate-batch-profile-destinations.md) (t.ex. Amazon S3 eller Oracle Eloqua)
      * [aktivera målgruppsdata för direktuppspelning av profilbaserade mål](./activate-streaming-profile-destinations.md) (till exempel HTTP API eller Amazon Kinesis).

   * Dessutom kan du redigera namnet och beskrivningen för måldataflödet.
   * Du kan använda **[!UICONTROL Enabled]/[!UICONTROL Disabled]** växla för att starta och pausa all dataexport till målet.

   ![Destinationsinformation](../assets/ui/edit-activation/destination-details.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du använt **[!UICONTROL destinations]** arbetsyta för att uppdatera befintliga måldataflöden.

Mer information om destinationer finns i [destinationer, översikt](../catalog/overview.md).
