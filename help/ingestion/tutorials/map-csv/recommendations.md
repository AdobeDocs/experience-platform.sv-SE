---
title: Mappa en CSV-fil till ett XDM-schema med AI-genererade rekommendationer
description: I den här självstudien beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av AI-genererade rekommendationer.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 0%

---

# Mappa en CSV-fil till ett XDM-schema med AI-genererade rekommendationer

>[!NOTE]
>
>Mer information om allmänt tillgängliga CSV-mappningsfunktioner i Experience Platform finns i dokumentet om [mappning av en CSV-fil till ett befintligt schema](./existing-schema.md).

För att kunna importera CSV-data till [!DNL Adobe Experience Platform] måste data mappas till ett [!DNL Experience Data Model] (XDM)-schema. Du kan mappa till [ett befintligt schema](./existing-schema.md), men om du inte vet exakt vilket schema som ska användas eller hur det ska struktureras kan du i stället använda dynamiska rekommendationer baserade på ML-modeller (Machine Learning) i Experience Platform-gränssnittet.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Experience Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * Du måste åtminstone förstå begreppet [beteenden i XDM](../../../xdm/home.md#data-behaviors), så att du kan bestämma om du ska mappa dina data till en [!UICONTROL Profile]-klass (postbeteende) eller [!UICONTROL ExperienceEvent]-klass (tidsseriebeteende).
* [Gruppinmatning](../../batch-ingestion/overview.md): Den metod som [!DNL Experience Platform] använder för att importera data från användartillhandahållna datafiler.
* [Adobe Experience Platform Data Prep](../../batch-ingestion/overview.md): En serie funktioner som gör att du kan mappa och omvandla inlästa data så att de överensstämmer med XDM-scheman. Dokumentationen för [dataprep-funktioner](../../../data-prep/functions.md) är särskilt relevant för schemamappning.

## Ange information om dataflöde

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen. Navigera till kategorin **[!UICONTROL Local system]** i vyn **[!UICONTROL Catalog]**. Välj **[!UICONTROL Add data]** under **[!UICONTROL Local file upload]**.

![Katalogen [!UICONTROL Sources] i Experience Platform-gränssnittet med [!UICONTROL Add data] under [!UICONTROL Local file upload] markerad.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

Arbetsflödet **[!UICONTROL Map CSV XDM schema]** visas med början i steget **[!UICONTROL Dataflow detail]**.

Välj **[!UICONTROL Create a new schema using ML recommendations]**, vilket gör att nya kontroller visas. Välj lämplig klass för de CSV-data som du vill mappa ([!UICONTROL Profile] eller [!UICONTROL ExperienceEvent]). Du kan också använda listrutan för att välja den bransch som är relevant för ditt företag, eller lämna den tom om de angivna kategorierna inte gäller för dig. Om din organisation arbetar under en [business-to-business-modell (B2B)](../../../xdm/tutorials/relationship-b2b.md) markerar du kryssrutan **[!UICONTROL B2B data]** .

![Steget [!UICONTROL Dataflow detail] med alternativet för ML-rekommendation markerat. [!UICONTROL Profile] väljs för klassen och [!UICONTROL Telecommunications] väljs för branschen ](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Här anger du ett namn för schemat som ska skapas från CSV-data och ett namn för den utdatauppsättning som ska innehålla data som hämtas under det schemat.

Du kan även konfigurera följande ytterligare funktioner för dataflödet innan du fortsätter:

| Indatanamn | Beskrivning |
| --- | --- |
| [!UICONTROL Description] | En beskrivning av dataflödet. |
| [!UICONTROL Error diagnostics] | När det här alternativet är aktiverat genereras felmeddelanden för nyligen kapslade batchar, som kan visas när motsvarande batch hämtas i [API](../../batch-ingestion/api-overview.md) . |
| [!UICONTROL Partial ingestion] | När det här alternativet är aktiverat importeras giltiga poster för nya batchdata inom ett angivet feltröskelvärde. Med det här tröskelvärdet kan du konfigurera procentandelen godtagbara fel innan hela batchen misslyckas. |
| [!UICONTROL Dataflow details] | Ange ett namn och en valfri beskrivning av dataflödet som hämtar CSV-data till Experience Platform. Dataflödet tilldelas automatiskt ett standardnamn när arbetsflödet startas. Det är valfritt att ändra namnet. |
| [!UICONTROL Alerts] | Välj i en lista över [varningar i produkten](../../../observability/alerts/overview.md) som du vill ta emot om dataflödets status när det har initierats. |

{style="table-layout:auto"}

Välj **[!UICONTROL Next]** när du är klar med konfigurationen av dataflödet.

![Avsnittet [!UICONTROL Dataflow detail] har slutförts.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Markera data

I steget **[!UICONTROL Select data]** använder du den vänstra kolumnen för att överföra din CSV-fil. Du kan välja **[!UICONTROL Choose files]** om du vill öppna en dialogruta för filutforskaren och välja filen från. Du kan också dra och släppa filen direkt i kolumnen.

![Knappen [!UICONTROL Choose files] och dra och släpp-området är markerat i [!UICONTROL Select data]-steget.](../../images/tutorials/map-csv-recommendations/upload-files.png)

När du har överfört filen visas ett exempeldataavsnitt som visar de första tio raderna i de mottagna data så att du kan kontrollera att de har överförts korrekt. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Exempeldatarader fylls i på arbetsytan](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Konfigurera schemamappningar

ML-modellerna körs för att generera ett nytt schema baserat på dataflödeskonfigurationen och den överförda CSV-filen. När processen är klar fylls steget [!UICONTROL Mapping] i så att mappningarna för varje enskilt fält visas bredvid den fullt navigerbara vyn för den genererade schemastrukturen.

![Steget [!UICONTROL Mapping] i användargränssnittet, med alla mappade CSV-fält och den resulterande schemastrukturen.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>Du kan filtrera alla fält i schemat baserat på en rad olika villkor under arbetsflödet för att mappa fält från källa till mål. Standardbeteendet är att alla mappade fält visas. Om du vill ändra de fält som visas markerar du filterikonen bredvid sökinmatningsfältet och väljer ett alternativ i listrutan.<br> ![Mappningssteget för arbetsflödet för att skapa CSV-schema till XDM-schema med filterikonen och listrutemenyn markerade.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "Mappningssteget för arbetsflödet för CSV-till-XDM-schemat med filterikonen och listrutan markerad."){width="100" zoomable="yes"}

Härifrån kan du [redigera fältmappningarna](#edit-mappings) eller [ändra de fältgrupper som de är kopplade till](#edit-schema) efter dina behov. När du är nöjd väljer du **[!UICONTROL Finish]** för att slutföra mappningen och initiera dataflödet som du konfigurerade tidigare. CSV-data hämtas in till systemet och fyller i en datauppsättning som baseras på den genererade schemastrukturen, klar att användas av Experience Platform-tjänster längre fram i kedjan.

![Knappen [!UICONTROL Finish] markeras och CSV-mappningsprocessen slutförs.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Redigera fältkopplingar {#edit-mappings}

Använd förhandsgranskningen av fältmappningen för att redigera befintliga mappningar eller ta bort dem helt. Mer information om hur du hanterar en mappningsuppsättning i användargränssnittet finns i [Användargränssnittshandboken för datapersonmappning](../../../data-prep/ui/mapping.md#mapping-interface).

### Redigera fältgrupper {#edit-field-groups}

CSV-fälten mappas automatiskt till befintliga XDM-fältgrupper med hjälp av ML-modeller. Om du vill ändra fältgruppen för ett visst CSV-fält väljer du **[!UICONTROL Edit]** bredvid schematrädet.

![Knappen [!UICONTROL Edit] markeras bredvid schematrädet.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

En dialogruta visas där du kan redigera visningsnamn, datatyp och fältgrupp för alla fält i mappningen. Markera redigeringsikonen (![redigeringsikonen](/help/images/icons/edit.png)) bredvid ett källfält om du vill redigera informationen i den högra kolumnen innan du väljer **[!UICONTROL Apply]**.

![Den rekommenderade fältgruppen för ett källfält ändras.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

När du är klar med justeringen av schemarekommendationerna för dina källfält väljer du **[!UICONTROL Save]** för att tillämpa ändringarna.

## Nästa steg

I den här guiden beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av AI-genererade rekommendationer, så att du kan överföra data till Experience Platform via batchingång.

Anvisningar om hur du mappar en CSV-fil till ett befintligt schema finns i det [befintliga arbetsflödet för schemamappning](./existing-schema.md). Mer information om direktuppspelning av data till Experience Platform i realtid via färdiga källanslutningar finns i [Källöversikt](../../../sources/home.md).

Du kan också använda HTML-algoritmer (Machine Learning) för att **generera ett schema från CSV-exempeldata**. Det här arbetsflödet skapar automatiskt ett nytt schema baserat på CSV-filens struktur och innehåll. Det nya schemat matchar dataformatet så att du sparar tid och får större exakthet när du definierar struktur, fält och datatyper för stora komplexa datauppsättningar. Mer information om det här arbetsflödet finns i guiden [Skapa ML-stödda scheman](../../../xdm/ui/ml-assisted-schema-creation.md).
