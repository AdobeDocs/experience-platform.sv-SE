---
title: Mappa en CSV-fil till ett XDM-schema med hjälp av AI-genererade Recommendations
description: I den här självstudien beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av AI-genererade rekommendationer.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Mappa en CSV-fil till ett XDM-schema med hjälp av AI-genererade rekommendationer

>[!NOTE]
>
>Mer information om allmänt tillgängliga CSV-mappningsfunktioner i Platform finns i dokumentet om [mappa en CSV-fil till ett befintligt schema](./existing-schema.md).

För att kunna importera CSV-data till [!DNL Adobe Experience Platform]måste data mappas till en [!DNL Experience Data Model] (XDM) schema. Du kan välja att mappa till [ett befintligt schema](./existing-schema.md), men om du inte vet exakt vilket schema som ska användas eller hur det ska struktureras kan du i stället använda dynamiska rekommendationer baserade på ML-modeller (Machine Learning) i plattformsgränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.
   * Du måste åtminstone förstå begreppet [beteenden i XDM](../../../xdm/home.md#data-behaviors)så att du kan bestämma om du vill mappa dina data till en [!UICONTROL Profile] klass (postbeteende) eller [!UICONTROL ExperienceEvent] klass (tidsseriebeteende).
* [Batchförtäring](../../batch-ingestion/overview.md): Den metod som [!DNL Platform] importerar data från datafiler som användaren anger.
* [Adobe Experience Platform Data Prep](../../batch-ingestion/overview.md): En uppsättning funktioner som gör att du kan mappa och omvandla inkapslade data så att de överensstämmer med XDM-scheman. Dokumentationen om [Förinställningsfunktioner för data](../../../data-prep/functions.md) är specifikt relevant för schemamappning.

## Ange information om dataflöde

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Sources]** i den vänstra navigeringen. På **[!UICONTROL Catalog]** visa, navigera till **[!UICONTROL Local system]** kategori. Under **[!UICONTROL Local file upload]** väljer du **[!UICONTROL Add data]**.

![The [!UICONTROL Sources] katalog i plattformens användargränssnitt, med [!UICONTROL Add data] under [!UICONTROL Local file upload] markeras.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

The **[!UICONTROL Map CSV XDM schema]** arbetsflödet visas, med början på **[!UICONTROL Dataflow detail]** steg.

Välj **[!UICONTROL Create a new schema using ML recommendations]**, vilket medför att nya kontroller visas. Välj lämplig klass för de CSV-data som du vill mappa ([!UICONTROL Profile] eller [!UICONTROL ExperienceEvent]). Du kan också använda listrutan för att välja den bransch som är relevant för ditt företag, eller lämna den tom om de angivna kategorierna inte gäller för dig. Om din organisation är verksam under [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md) modell, välj **[!UICONTROL B2B data]** kryssrutan.

![The [!UICONTROL Dataflow detail] med alternativet för ML-rekommendation markerat. [!UICONTROL Profile] är markerat för klassen och [!UICONTROL Telecommunications] väljs för branschen](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Här anger du ett namn för schemat som ska skapas från CSV-data och ett namn för den utdatauppsättning som ska innehålla data som hämtas under det schemat.

Du kan även konfigurera följande ytterligare funktioner för dataflödet innan du fortsätter:

| Indatanamn | Beskrivning |
| --- | --- |
| [!UICONTROL Description] | En beskrivning av dataflödet. |
| [!UICONTROL Error diagnostics] | När det här alternativet är aktiverat genereras felmeddelanden för nyligen kapslade batchar, som kan visas när motsvarande batch hämtas i [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Partial ingestion] | När det här alternativet är aktiverat importeras giltiga poster för nya batchdata inom ett angivet feltröskelvärde. Med det här tröskelvärdet kan du konfigurera procentandelen godtagbara fel innan hela gruppen misslyckas. |
| [!UICONTROL Dataflow details] | Ange ett namn och en valfri beskrivning av dataflödet som hämtar CSV-data till plattformen. Dataflödet tilldelas automatiskt ett standardnamn när arbetsflödet startas. Det är valfritt att ändra namnet. |
| [!UICONTROL Alerts] | Välj i en lista över [varningar i produkten](../../../observability/alerts/overview.md) som du vill få information om dataflödets status när det har initierats. |

{style="table-layout:auto"}

När du har konfigurerat dataflödet väljer du **[!UICONTROL Next]**.

![The [!UICONTROL Dataflow detail] -avsnittet har slutförts.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Markera data

På **[!UICONTROL Select data]** använder du den vänstra kolumnen för att överföra din CSV-fil. Du kan välja **[!UICONTROL Choose files]** om du vill öppna en dialogruta för filutforskaren där du kan välja filen från, eller så kan du dra och släppa filen direkt i kolumnen.

![The [!UICONTROL Choose files] och dra-och-släpp-områden som är markerade i [!UICONTROL Select data] steg.](../../images/tutorials/map-csv-recommendations/upload-files.png)

När du har överfört filen visas ett exempeldataavsnitt som visar de första tio raderna i de mottagna data så att du kan kontrollera att de har överförts korrekt. Välj **[!UICONTROL Next]** för att fortsätta.

![Exempeldatarader fylls i på arbetsytan](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Konfigurera schemamappningar

ML-modellerna körs för att generera ett nytt schema baserat på dataflödeskonfigurationen och den överförda CSV-filen. När processen är klar [!UICONTROL Mapping] fylls i för att visa mappningarna för varje enskilt fält tillsammans med den fullt navigerbara vyn av den genererade schemastrukturen.

![The [!UICONTROL Mapping] i användargränssnittet, där alla mappade CSV-fält och den resulterande schemastrukturen visas.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Här kan du välja att [redigera fältkopplingar](#edit-mappings) eller [ändra de fältgrupper som de är kopplade till](#edit-schema) efter era behov. När du är nöjd väljer du **[!UICONTROL Finish]** för att slutföra mappningen och initiera dataflödet som du konfigurerade tidigare. CSV-data hämtas in till systemet och fyller i en datauppsättning som baseras på den genererade schemastrukturen, klar att användas av plattformstjänster längre fram i kedjan.

![The [!UICONTROL Finish] när du markerar knappen, slutför CSV-mappningsprocessen.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Redigera fältkopplingar {#edit-mappings}

Använd förhandsgranskningen av fältmappningen för att redigera befintliga mappningar eller ta bort dem helt. Mer information om hur du hanterar en mappningsuppsättning i användargränssnittet finns i [Användargränssnittshandbok för datapersonmappning](../../../data-prep/ui/mapping.md#mapping-interface).

### Redigera fältgrupper {#edit-field-groups}

CSV-fälten mappas automatiskt till befintliga XDM-fältgrupper med hjälp av ML-modeller. Om du vill ändra fältgruppen för ett visst CSV-fält väljer du **[!UICONTROL Edit]** bredvid schematrädet.

![The [!UICONTROL Edit] knappen markeras bredvid schematrädet.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

En dialogruta visas där du kan redigera visningsnamn, datatyp och fältgrupp för alla fält i mappningen. Markera redigeringsikonen (![Ikonen Redigera](../../images/tutorials/map-csv-recommendations/edit-icon.png)) bredvid ett källfält för att redigera informationen i den högra kolumnen innan du väljer **[!UICONTROL Apply]**.

![Den rekommenderade fältgruppen för ett källfält som ändras.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

När du är klar med justeringen av schemarekommendationerna för källfälten väljer du **[!UICONTROL Save]** för att tillämpa ändringarna.

## Nästa steg

I den här guiden beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av AI-genererade rekommendationer, så att du kan överföra data till plattformen genom batchingång.

Anvisningar om hur du mappar en CSV-fil till ett befintligt schema finns i [befintligt arbetsflöde för schemamappning](./existing-schema.md). Mer information om att strömma data till plattformen i realtid via färdiga källanslutningar finns i [källöversikt](../../../sources/home.md).
