---
keywords: redigera aktivering, redigera mål, redigera mål
title: Redigera aktiveringsdataflöden
type: Tutorial
description: Följ stegen i den här artikeln när du vill redigera ett befintligt aktiveringsdataflöde i Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Redigera aktiveringsdataflöden {#edit-activation-flows}

I Adobe Experience Platform kan du redigera olika komponenter i befintliga aktiveringsdataflöden till mål, t.ex. exporterade målgrupper och profilattribut, exportfrekvens, om aktiveringsdataflödet är aktiverat eller inaktiverat, med mera.

## Redigera dataflöden {#edit-dataflows}

Följ stegen nedan för att redigera befintliga aktiveringsdataflöden:

1. Logga in på [Experience Platform-gränssnittet](https://platform.adobe.com/) och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Browse]** i den övre rubriken om du vill visa befintliga måldataflöden.

   ![Bläddra bland mål](../assets/ui/edit-activation/browse-destinations.png)

2. Välj filterikonen ![Filterikon](/help/images/icons/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtrera mål](../assets/ui/edit-activation/filter-destinations.png)

3. Välj namnet på måldataflödet som du vill redigera.

   ![Välj mål](../assets/ui/edit-activation/destination-select.png)

4. Målsidan **[!UICONTROL Dataflow runs]** visas med de tillgängliga kontrollerna. Nu kan du redigera flera komponenter i måldataflödet:

   * Välj **[!UICONTROL Activate audiences]** i den högra listen för att ändra vilka målgrupper eller profilattribut som ska skickas till målet. Den här åtgärden tar dig till aktiveringsarbetsflödet, som skiljer sig åt beroende på måltyp. Mer information finns i stödlinjerna för:
      * [aktivera målgruppsdata för målgruppsdirektuppspelningsmål](./activate-segment-streaming-destinations.md) (till exempel Facebook eller Twitter);
      * [aktivera målgruppsdata till gruppprofilbaserade mål](./activate-batch-profile-destinations.md) (t.ex. Amazon S3 eller Oracle Eloqua);
      * [aktiverar målgruppsdata för direktuppspelning av profilbaserade mål](./activate-streaming-profile-destinations.md) (till exempel HTTP API eller Amazon Kinesis).

   * Dessutom kan du redigera namnet och beskrivningen för måldataflödet.
   * Du kan använda växlingsknappen **[!UICONTROL Enabled]/[!UICONTROL Disabled]** för att starta och pausa all dataexport till målet.

   ![Målinformation](../assets/ui/edit-activation/destination-details.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du använt arbetsytan **[!UICONTROL destinations]** för att uppdatera befintliga måldataflöden.

Mer information om mål finns i [målöversikten](../catalog/overview.md).
