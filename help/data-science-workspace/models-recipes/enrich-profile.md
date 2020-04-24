---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics
solution: Experience Platform
title: Berika kundprofilen i realtid med maskininlärningsinsikter
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Berika kundprofilen i realtid med maskininlärningsinsikter

Adobe Experience Platform Data Science Workspace innehåller verktyg och resurser för att skapa, utvärdera och använda maskininlärningsmodeller för att generera dataprognoser och insikter. När maskininlärningsinsikter hämtas in i en profilaktiverad datauppsättning, hämtas samma data också in som profilposter, som sedan kan segmenteras i deluppsättningar av relaterade element med hjälp av Experience Platform Segmentation Service.

I det här dokumentet finns en stegvis självstudiekurs för att berika kundprofilen i realtid med maskininlärningsinsikter. Stegen är indelade i följande avsnitt:

1. [Skapa ett utdatamaterial och en datauppsättning](#create-an-output-schema-and-dataset)
2. [Konfigurera ett utdataschema och en datauppsättning](#configure-an-output-schema-and-dataset)
3. [Skapa segment med segmentverktyget](#create-segments-using-the-segment-builder)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika aspekter av Adobe Experience Platform som används för att importera profildata och skapa segment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

* [Kundprofil](../../rtcdp/overview.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Identitetstjänst](../../identity-service/home.md): Möjliggör kundprofil i realtid genom att överbrygga identiteter från olika datakällor som hämtas in till Platform.
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

Förutom de ovannämnda dokumenten rekommenderar vi att du även granskar följande handböcker om scheman och schemaläggningsprogrammet:

* [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Beskriver XDM-scheman, byggstenar, principer och bästa metoder för att skapa scheman som ska användas i Experience Platform.
* [Schemaredigeraren, genomgång](../../xdm/tutorials/create-schema-ui.md): Innehåller detaljerade anvisningar om hur du skapar scheman med Schemaredigeraren i Experience Platform.

## Skapa ett utdatamaterial och en datauppsättning {#create-an-output-schema-and-dataset}

Det första steget mot att berika kundprofilen i realtid med poängsättningsinsikter är att veta vilket verkligt objekt (som en person) era data definierar. Genom att förstå era data kan ni beskriva och utforma en struktur som betyder för era data, ungefär som att utforma en relationsdatabas.

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Det här avsnittet innehåller grundläggande instruktioner om hur du skapar ett schema med schemaverktyget. En mer ingående självstudiekurs finns i självstudiekursen om hur du [skapar ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md).

1. På Adobe Experience Platform klickar du på fliken **Schema** för att öppna schemaläsaren. Klicka på **Skapa schema** för att komma åt *Schemaredigeraren*, där du interaktivt kan skapa och skapa scheman.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. I fönstret *Disposition* klickar du på **Tilldela** för att bläddra bland de tillgängliga klasserna.
   * Om du vill tilldela en befintlig klass klickar du på och markerar den önskade klassen och klickar sedan på **Tilldela klass**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Om du vill skapa en anpassad klass klickar du på **Skapa ny klass** i mitten av webbläsarfönstret. Ange ett klassnamn, en beskrivning och välj klassens beteende. Klicka på **Tilldela klass** när du är klar.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)
   Nu bör schemats struktur innehålla några klassfält och du är redo att tilldela mixins. En blandning är en grupp med ett eller flera fält som beskriver ett visst koncept.

3. Klicka på *Lägg till* i underavsnittet **Blandningar** i fönstret *Disposition* .
   * Om du vill tilldela en befintlig blandning klickar du på och markerar den önskade blandningen och klickar sedan på **Lägg till blandning**. Till skillnad från klasser kan flera blandningar tilldelas till ett enda schema så länge det är lämpligt.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Om du vill skapa en ny mixin klickar du på **Skapa ny mixning** i mitten av webbläsarfönstret. Ange ett namn och en beskrivning för blandningen och klicka sedan på **Tilldela mixning** när du är klar.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Om du vill lägga till blandningsfält klickar du på namnet på blandningen i *kompositionsfönstret* . Du kan sedan lägga till blandade fält genom att klicka på **Lägg till fält** i *strukturfönstret* . Se till att du anger blandningsegenskaper i enlighet med detta.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. När du är klar med att skapa schemat klickar du på fältet på den översta nivån i schemat i fönstret *Struktur* för att visa schemats egenskaper i det högra egenskapsfönstret. Ange ett namn och en beskrivning och klicka på **Spara** för att skapa schemat.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Skapa en utdatamängd med ditt nyligen skapade schema genom att klicka på **Datauppsättningar** i den vänstra navigeringskolumnen och sedan klicka på **Skapa datauppsättning**. På nästa skärm väljer du **Skapa datauppsättning från schema**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. Använd schemaläsaren för att söka efter och markera det nya schemat och klicka sedan på **Nästa**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Ange ett namn och en valfri beskrivning och klicka sedan på **Slutför** för att skapa datauppsättningen.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Nu när du har skapat en utdataschemauppsättning kan du fortsätta till nästa avsnitt för att konfigurera och aktivera dem för profilanrikning.

## Konfigurera ett utdataschema och en datauppsättning {#configure-an-output-schema-and-dataset}

Innan du kan aktivera en datauppsättning för profil måste du konfigurera datasetens schema så att det har ett primärt identitetsfält och sedan aktivera schemat för profil. Om du vill skapa och aktivera ett nytt schema kan du gå till självstudiekursen om hur du [skapar ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md). Följ annars instruktionerna nedan för att aktivera ett befintligt schema och en befintlig datauppsättning.

1. På Adobe Experience Platform använder du schemaläsaren för att hitta det utdataschema som du vill aktivera profilen på och klickar på dess namn för att visa dess komposition.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Expandera schemastrukturen och hitta ett lämpligt fält som ska anges som primär identifierare. Klicka på det önskade fältet för att visa dess egenskaper.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Ange fältet som primär identitet genom att aktivera fältegenskapen **Identitet** , **Primär identitet** och sedan välja ett lämpligt **identitetsnamnområde**. Klicka på **Använd** när du har gjort ändringarna.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Klicka på det översta nivåobjektet i schemastrukturen för att visa schemaegenskaperna och aktivera schemat för profilen genom att växla **profilväxeln** . Klicka på **Spara** för att slutföra ändringarna. Den datauppsättning som skapades med det här schemat kan nu aktiveras för profilen.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Använd datauppsättningens webbläsare för att hitta den datauppsättning som du vill aktivera profilen för och klicka på dess namn för att komma åt informationen.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Aktivera datauppsättningen för profilen genom att växla **profilväxeln** i rätt informationskolumn.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

När data hämtas in till en profilaktiverad datauppsättning, hämtas samma data även som profilposter. Nu när ditt schema och din datauppsättning har förberetts kan du generera data i datauppsättningen genom att utföra poängkörningar med en lämplig modell, och fortsätta med den här självstudiekursen för att skapa insikter med hjälp av Segment Builder.

## Skapa segment med segmentverktyget {#create-segments-using-the-segment-builder}

Nu när du har genererat och inhämtat insikter i din profilaktiverade datauppsättning kan du hantera dessa data genom att identifiera deluppsättningar av relaterade element med hjälp av segmentbyggaren. Följ stegen nedan för att skapa egna segment.

1. På Adobe Experience Platform klickar du på fliken **Segment** följt av **Skapa segment** för att komma åt segmentbyggaren.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. I segmentbyggaren ger den vänstra listen tillgång till de centrala byggstenarna i segment: attribut, händelser och befintliga segment. Varje byggsten visas på sin egen flik. Välj den klass som det profilaktiverade schemat omfattar och bläddra sedan efter byggstenarna för ditt segment.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Dra och släpp byggstenar på regelbyggarens arbetsyta, fyll i dem genom att ange jämförande satser.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. När du skapar ett segment kan du förhandsgranska det uppskattade segmentresultatet genom att observera panelen *Segmentegenskaper* .
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Välj en lämplig **sammanfogningsprofil**, ange ett namn och en valfri beskrivning och klicka sedan på **Spara** för att slutföra det nya segmentet.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Nästa steg {#next-steps}

I det här dokumentet gick du igenom de steg som krävs för att aktivera ett schema och en datauppsättning för profil och demonstrerade kortfattat arbetsflödet för att skapa insiktssegment med hjälp av segmentbyggaren. Mer information om segment och segmentbyggaren finns i Översikt över [segmenteringstjänsten](../../segmentation/home.md).