---
keywords: Experience Platform;hem;populära ämnen;direktuppspelning;molnlagringskontakt;molnlagring
solution: Experience Platform
title: Skapa ett direktuppspelat dataflöde för en molnlagringskälla i användargränssnittet
type: Tutorial
description: Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med molnlagringsbasen.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 6419ae7648a91dc7f9432281c1960beccc65bdb0
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Skapa ett direktuppspelat dataflöde för en molnlagringskälla i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en Adobe Experience Platform-datauppsättning. I den här självstudiekursen beskrivs hur du skapar ett direktuppspelat dataflöde för en molnlagringskälla i användargränssnittet.

Innan du provar den här självstudiekursen måste du skapa en giltig och autentiserad anslutning mellan ditt molnlagringskonto och din plattform. Om du inte redan har en autentiserad anslutning kan du gå till någon av följande självstudiekurser för att få information om hur du autentiserar ditt molnbaserade lagringskonton:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataflöden](../../../../../dataflows/home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras för olika tjänster, från källor till [!DNL Identity Service], till [!DNL Profile]och till [!DNL Destinations].
- [Dataprep](../../../../../data-prep/home.md): Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM). Dataförinställning visas som ett steg för&quot;Karta&quot; i dataöverföringsprocesserna, inklusive arbetsflödet för CSV-inmatning.
- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Lägg till data

>[!NOTE]
>
>Du kan bara skapa ett källdataflöde per konsumentgrupp för en given händelsehubb.

När du har skapat ditt autentiserade molnlagringskonto för direktuppspelning kan du **[!UICONTROL Select data]** visas, där du får ett gränssnitt där du kan välja vilken dataström du vill ta med till plattformen.

- Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
- Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

![gränssnitt](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Markera den dataström som du vill använda och välj sedan **[!UICONTROL Choose file]** för att överföra ett exempelschema.

>[!TIP]
>
>Om dina data är XDM-kompatibla kan du hoppa över överföringen av ett exempelschema och välja **[!UICONTROL Next]** för att fortsätta.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

När schemat har överförts uppdateras förhandsgranskningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda [!UICONTROL Search field] för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Mappning

The **[!UICONTROL Mapping]** visas med ett gränssnitt för att mappa källdata till en plattformsdatauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

### Ny datauppsättning

Om du vill importera data till en ny datauppsättning väljer du **[!UICONTROL New dataset]** och ange ett namn och en beskrivning för datauppsättningen i de angivna fälten. Om du vill lägga till ett schema kan du ange ett befintligt schemanamn i **[!UICONTROL Select schema]** -dialogrutan. Du kan också välja **[!UICONTROL Schema advanced search]** om du vill söka efter ett lämpligt schema.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

The [!UICONTROL Select schema] visas så att du får en lista över tillgängliga scheman att välja mellan. Välj ett schema i listan för att uppdatera den högra listen så att den visar information som är specifik för det schema du valde, inklusive information om huruvida schemat är aktiverat för [!DNL Profile].

När du har identifierat och valt det schema som du vill använda väljer du **[!UICONTROL Done]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

The [!UICONTROL Target dataset] siduppdateringar med det valda schemat som visas som en del av datauppsättningen. Under det här steget kan du aktivera datauppsättningen för [!DNL Profile] och skapa en helhetsbild av ett företags attribut och beteenden. Data från alla aktiverade datauppsättningar inkluderas i [!DNL Profile] och ändringarna tillämpas när du sparar dataflödet.

Växla **[!UICONTROL Profile dataset]** för att aktivera måldatauppsättningen för [!DNL Profile].

![new-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Befintlig datauppsättning

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** väljer du datamängdikonen.

![befintlig datamängd](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

The **[!UICONTROL Select dataset]** visas med en lista över tillgängliga datauppsättningar att välja mellan. Välj en datauppsättning från listan för att uppdatera högerspåret så att den visar information som är specifik för den datauppsättning du valde, inklusive information om huruvida datauppsättningen kan aktiveras för [!DNL Profile].

När du har identifierat och valt den datauppsättning du vill använda väljer du **[!UICONTROL Done]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

När du har valt datauppsättningen väljer du [!DNL Profile] växla för att aktivera datauppsättningen för [!DNL Profile].

![existing-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Mappa standardfält

När din datauppsättning och ditt schema är upprättat, **[!UICONTROL Map standard fields]** -gränssnittet visas så att du kan konfigurera mappningsfält manuellt för dina data.

>[!TIP]
>
>Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall.

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

När källdata har mappats väljer du **[!UICONTROL Next]**.

![mappning](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Dataflödesdetaljer

The **[!UICONTROL Dataflow detail]** visas så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Ange värden för dataflödet och välj **[!UICONTROL Next]**.

![dataflöde-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Granska

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection]**: Visar ditt kontonamn, typ av källa och annan information som är specifik för den strömmande molnlagringskällan som du använder.
- **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och målschemat som du använder för dataflödet.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** så att dataflödet kan skapas.

![recension](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Övervaka och ta bort dataflödet

När du har skapat ett direktuppspelat molnlagringsdataflöde kan du övervaka de data som hämtas genom det. Mer information om övervakning och borttagning av dataflöden för direktuppspelning finns i självstudiekursen om [övervaka strömmande dataflöden](../../monitor-streaming.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att strömma data från en molnlagringskälla. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan som [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [[!DNL Real-Time Customer Profile] översikt](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)