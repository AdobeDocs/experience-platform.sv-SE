---
keywords: mål;mål;destinationsdetaljsida;målinformationssida
title: Visa målinformation
description: På informationssidan för ett enskilt mål finns en översikt över målinformationen. Målinformationen innehåller målnamn, ID, målgrupper mappade till målet och kontroller för att redigera aktiveringen och aktivera och inaktivera dataflödet.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Visa målinformation

## Översikt {#overview}

I Adobe Experience Platform användargränssnitt kan du visa och övervaka attributen och aktiviteterna för dina mål. Dessa uppgifter omfattar målets namn och ID, kontroller för att aktivera eller inaktivera destinationer och mycket annat. Detaljerna innehåller även mått för aktiverade profilposter, aktiverade identiteter, misslyckade och exkluderade identiteter samt en historik över dataflöden.

>[!NOTE]
>
>Målinformationssidan är en del av [!UICONTROL Destinations] arbetsytan i [!DNL Platform] [!DNL UI]. Se [[!UICONTROL Destinations] arbetsyta - översikt](./destinations-workspace.md) för mer information.

## Visa målinformation {#view-details}

Följ stegen nedan för att visa mer information om ett befintligt mål.

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Browse]** i det övre sidhuvudet för att visa dina befintliga mål.

   ![Bläddra bland mål](../assets/ui/details-page/browse-destinations.png)

1. Markera filterikonen ![Filterikon](../assets/ui/details-page/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/details-page/filter-destinations.png)

1. Markera namnet på målet som du vill visa.

   ![Välj mål](../assets/ui/details-page/destination-select.png)

1. Målets informationssida visas med de tillgängliga kontrollerna.

   ![Destinationsinformation](../assets/ui/details-page/destination-details.png)

## Höger räl {#right-rail}

Den högra listen visar grundläggande information om det valda målet.

![höger räl](../assets/ui/details-page/right-sidebar.png)

Följande tabell omfattar de kontroller och den information som tillhandahålls av den högra spåret:

| Höger rälsartikel | Beskrivning |
| --- | --- |
| [!UICONTROL Activate audiences] | Välj den här kontrollen om du vill redigera vilka målgrupper som mappas till målet, uppdatera exportscheman eller lägga till och ta bort mappade attribut och identiteter. Visa stödlinjerna på [aktivera målgruppsdata till målgruppsdirektuppspelningsmål](./activate-segment-streaming-destinations.md), [aktivera målgruppsdata till batchprofilbaserade mål](./activate-batch-profile-destinations.md)och [aktivera målgruppsdata för direktuppspelning av profilbaserade mål](./activate-streaming-profile-destinations.md) för mer information. |
| [!UICONTROL Delete] | Gör att du kan ta bort det här dataflödet och ta bort mappar för de målgrupper som tidigare aktiverats, om det finns några. |
| [!UICONTROL Destination name] | Det här fältet kan redigeras för att uppdatera målets namn. |
| [!UICONTROL Description] | Det här fältet kan redigeras för att uppdatera eller lägga till en valfri beskrivning till målet. |
| [!UICONTROL Destination] | Representerar målplattformen som målgrupperna skickas till. Se [målkatalog](../catalog/overview.md) för mer information. |
| [!UICONTROL Status] | Anger om målet är aktiverat eller inaktiverat. |
| [!UICONTROL Marketing actions] | Anger de marknadsföringsåtgärder (användningsfall) som gäller för den här destinationen i datastyrningssyfte. |
| [!UICONTROL Category] | Anger måltypen. Se [målkatalog](../catalog/overview.md) för mer information. |
| [!UICONTROL Connection type] | Anger det formulär som era målgrupper skickas till. Möjliga värden är [!UICONTROL Cookie] och [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Anger hur ofta målgrupperna skickas till målet. Möjliga värden är [!UICONTROL Streaming] och [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Representerar det ID-namnutrymme som accepteras av målet, till exempel `GAID`, `IDFA`, eller `email`. Mer information om godkända ID-namnutrymmen finns i [Översikt över namnutrymmet identity](../../identity-service/features/namespaces.md). |
| [!UICONTROL Created by] | Anger den användare som skapade det här målet. |
| [!UICONTROL Created] | Anger UTC-datum/tid när det här målet skapades. |

{style="table-layout:auto"}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] växla {#enabled-disabled-toggle}

Du kan använda **[!UICONTROL Enabled]/[!UICONTROL Disabled]** växla för att starta och pausa all dataexport till målet.

![Aktivera eller inaktivera dataflödets växlingsknapp](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs] {#dataflow-runs}

The [!UICONTROL Dataflow runs] -fliken innehåller mätdata om dataflödet som körs till batchmål och direktuppspelningsmål. Se [Övervaka dataflöden](monitor-dataflows.md) för detaljer och måttdefinitioner.

>[!NOTE]
>
>* Funktionen för destinationsövervakning stöds för närvarande för alla destinationer i Experience Platform *utom* den [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Anpassad personalisering](/help/destinations/catalog/personalization/custom-personalization.md) och [Experience Cloud målgrupper](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinationer.
>* För [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)och [HTTP-API](/help/destinations/catalog/streaming/http-destination.md) destinationer uppskattas de värden som är relaterade till identiteter som har uteslutits, misslyckats och aktiverats. Högre volymer av aktiveringsdata leder till större noggrannhet i mätvärdena.

![Vy för körning av dataflöde](../assets/ui/details-page/dataflow-runs.png)

### Varaktighet för dataflöde {#dataflow-runs-duration}

Det finns en skillnad i hur länge dataflödet visas mellan direktuppspelning och filbaserade mål.

### Strömmande mål {#streaming}

Med **[!UICONTROL Processing duration]** som anges för de flesta direktuppspelade dataflöden är ungefär fyra timmar, vilket visas i bilden nedan, så är den faktiska bearbetningstiden för dataflödeskörningar mycket kortare. Dataflödeskörningsfönstren är öppna längre om Experience Platform behöver göra nya anrop till målet och även se till att det inte missar några senare data för samma tidsfönster.

![Bild av dataflödet kör sidan med kolumnen Bearbetningstid markerad för ett direktuppspelningsmål.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Mer information finns i [dataflödet körs till direktuppspelningsmål](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) i övervakningsdokumentationen.

### Filbaserade mål {#file-based}

För dataflöden som går till filbaserade mål gäller följande: **[!UICONTROL Processing duration]** beror på storleken på de data som exporteras och systeminläsningen. Observera också att dataflödet går till filbaserade mål uppdelas per målgrupp.

![Bild av dataflödet kör sida med kolumnen Bearbetningstid markerad för ett filbaserat mål.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Mer information finns i [dataflödet körs till batchbaserade (filbaserade) mål](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) i övervakningsdokumentationen.

## [!UICONTROL Activation data] {#activation-data}

The [!UICONTROL Activation data] På -fliken visas en lista med målgrupper som har mappats till målet, inklusive startdatum och slutdatum (om tillämpligt) samt annan relevant information för dataexporten, t.ex. exporttyp, schema och frekvens. Om du vill visa information om en viss målgrupp väljer du namnet i listan.

>[!TIP]
>
>Om du vill visa och redigera information om attribut och identiteter som är mappade till ett mål väljer du **[!UICONTROL Activate audiences]** i [höger räl](#right-rail).

![Batchmål för aktiveringsdatavyn](../assets/ui/details-page/activation-data-batch.png)

![Mål för direktuppspelning av aktiveringsdatavy](../assets/ui/details-page/activation-data-streaming.png)

### [!BADGE Beta]{type=Informative} Ta bort flera målgrupper från aktiveringsflöden {#bulk-remove}

>[!NOTE]
>
Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen.

Om du vill ta bort flera målgrupper från befintliga aktiveringsflöden markerar du målgrupperna och väljer sedan **[!UICONTROL Remove audiences]**.

![Markering av alternativet Ta bort målgrupper i fönstret Aktiveringsdata.](../assets/ui/details-page/bulk-remove-audiences.png)

### Exportera flera filer on demand till batchmål {#bulk-export}

Du kan [exportera flera filer on demand](../ui/export-file-now.md) från **[!UICONTROL Activation data]** sida. Om du vill göra det väljer du de målgrupper som du vill exportera filer för on-demand och väljer **[!UICONTROL Export file now]** -kontroll för att aktivera en engångs-export som levererar en fil för varje vald målgrupp till batchdestinationen.

![Bild som markerar knappen Exportera fil nu.](../assets/ui/details-page/bulk-export-file-now.png)

### Redigera aktiveringsscheman för flera målgrupper som exporterats till batchdestinationer {#bulk-edit-schedule}

Om du vill redigera det befintliga aktiveringsschemat för flera målgrupper samtidigt markerar du önskade målgrupper och väljer sedan **[!UICONTROL Edit schedule]**. Mer information om hur du definierar eller redigerar ett exportschema finns i [schemalägga export av målgrupper](../ui/activate-batch-profile-destinations.md#scheduling) -avsnitt.

![Aktiveringsdataskärm som markerar alternativet att redigera aktiveringsplaner för flera målgrupper.](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
Mer information om hur du utforskar en målgrupps informationssida finns i [Översikt över målgruppsportalen](../../segmentation/ui/audience-portal.md#segment-details).
