---
keywords: Experience Platform;hem;populära ämnen;konfigurera dataflöde;kundframgångskoppling
solution: Experience Platform
title: Konfigurera ett dataflöde för en anslutning till en källa för lyckade kunder i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en [!DNL Platform] datauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med ditt konto för kundframgångar.
exl-id: d348a7f8-6302-45f1-9961-bab56ad0407e
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Konfigurera ett dataflöde för en anslutning till kundens framgång i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en [!DNL Platform] datauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med ditt konto för kundframgångar.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver dessutom att du redan har skapat ett konto för kundframgångar. En lista med självstudiekurser för att skapa olika kundframgångskopplingar i användargränssnittet finns i [översikt över källanslutningar](../../../home.md).

## Markera data

När du har skapat en kundframgångskontakt kan **[!UICONTROL Select data]** visas med ett interaktivt gränssnitt där du kan utforska din filhierarki.

- Den vänstra halvan av gränssnittet är en katalogwebbläsare som visar serverns filer och kataloger.
- I den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en kompatibel fil.

Du kan använda **[!UICONTROL Search]** överst på sidan för att snabbt identifiera de källdata som du tänker använda.

>[!NOTE]
>
>Sökkällans dataalternativ är tillgängligt för alla tabellbaserade källanslutningar, med undantag för Analytics-, Classifications-, Event Hubs- och Kinesis-anslutningar.

När du har hittat källdata markerar du katalogen och klickar sedan på **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Mappa datafält till ett XDM-schema

The **[!UICONTROL Mapping]** visas med ett interaktivt gränssnitt för att mappa källdata till [!DNL Platform] datauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

### Använd en befintlig datauppsättning

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Use existing dataset]** klickar du sedan på datamängdikonen.

![use-existing-dataset](../../../images/tutorials/dataflow/customer-success/use-existing-dataset.png)

The **[!UICONTROL Select dataset]** visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **[!UICONTROL Continue]**.

![select-existing-dataset](../../../images/tutorials/dataflow/customer-success/select-dataset.png)

### Använd en ny datauppsättning

Om du vill importera data till en ny datauppsättning väljer du **[!UICONTROL Create new dataset]** och ange ett namn och en beskrivning för datauppsättningen i de angivna fälten.

Du kan bifoga ett schemafält genom att ange ett schemanamn i **[!UICONTROL Select schema]** sökfält. Du kan också välja listruteikonen för att visa en lista över befintliga scheman. Du kan också välja **[!UICONTROL Advanced search]** för att få tillgång till skärmen för befintliga scheman, inklusive deras respektive uppgifter.

Under det här steget kan du aktivera datauppsättningen för [!DNL Real-time Customer Profile] och skapa en helhetsbild av ett företags attribut och beteenden. Data från alla aktiverade datauppsättningar inkluderas i [!DNL Profile] och ändringarna tillämpas när du sparar dataflödet.

Växla **[!UICONTROL Profile dataset]** för att aktivera måldatauppsättningen för [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/crm/new-dataset.png)

The **[!UICONTROL Select schema]** visas. Välj det schema som du vill tillämpa på den nya datauppsättningen och klicka sedan på **[!UICONTROL Done]**.

![select-schema](../../../images/tutorials/dataflow/customer-success/select-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../data-prep/ui/mapping.md).

>[!TIP]
>
>Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Välj **[!UICONTROL Preview data]** för att se mappningsresultat på upp till 100 rader med exempeldata från den valda datauppsättningen.

Under förhandsgranskningen prioriteras identitetskolumnen som det första fältet, eftersom det är den nyckelinformation som krävs vid validering av mappningsresultat.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

När källdata har mappats väljer du **[!UICONTROL Close]**.

## Schemalägg körning av inmatning

The **[!UICONTROL Scheduling]** visas så att du kan konfigurera ett matningsschema att automatiskt importera valda källdata med de konfigurerade mappningarna. I följande tabell visas de olika konfigurerbara fälten för schemaläggning:

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Valbara frekvenser inkluderar `Once`, `Minute`, `Hour`, `Day`och `Week`. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. |
| Starttid | En UTC-tidsstämpel som anger när det allra första intaget är inställt. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. If **[!UICONTROL Backfill]** är aktiverat kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. If **[!UICONTROL Backfill]** är inaktiverat, kommer endast de filer som läses in mellan den första importkörningen och starttiden att importeras. Filer som lästs in före starttiden importeras inte. |
| Delta-kolumn | Ett alternativ med en filtrerad uppsättning källschemafält av typen, datumet eller tiden. Det här fältet används för att skilja mellan nya och befintliga data. Inkrementella data importeras baserat på tidsstämpeln för den markerade kolumnen. |

Dataflöden är utformade för att automatiskt importera data enligt schema. Börja med att välja intagsfrekvens. Ange sedan intervallet för att ange perioden mellan två flödeskörningar. Intervallets värde måste vara ett heltal som inte är noll och måste vara större än eller lika med 15.

Om du vill ange starttid för intaget justerar du datumet och tiden som visas i rutan för starttid. Du kan också välja kalenderikonen för att redigera starttidsvärdet. Starttiden måste vara större än eller lika med den aktuella UTC-tiden.

Välj **[!UICONTROL Load incremental data by]** för att tilldela deltakolumnen. I det här fältet görs en skillnad mellan nya och befintliga data.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Konfigurera ett dataflöde för engångsbruk

Om du vill ställa in engångsinmatning väljer du den nedrullningsbara frekvenspilen och väljer **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** och **[!UICONTROL Backfill]** inte syns vid engångsbruk.

När du har angett lämpliga värden för schemat väljer du **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Ange information om dataflöde

The **[!UICONTROL Dataflow detail]** visas så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Under den här processen kan du även aktivera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**. Aktivering **[!UICONTROL Partial ingestion]** ger möjlighet att importera data som innehåller fel upp till ett visst tröskelvärde. En gång **[!UICONTROL Partial ingestion]** är aktiverat drar du **[!UICONTROL Error threshold %]** för att justera batchens feltröskel. Du kan också justera tröskelvärdet manuellt genom att markera inmatningsrutan. Mer information finns i [partiell batchingång - översikt](../../../../ingestion/batch-ingestion/partial.md).

Ange värden för dataflödet och välj **[!UICONTROL Next]**.

![dataflödesinformation](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Granska ditt dataflöde

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection details]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
- **[!UICONTROL Mapping details]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
- **[!UICONTROL Schedule details]**: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** så att dataflödet kan skapas.

![recension](../../../images/tutorials/dataflow/customer-success/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen om [övervaka konton och dataflöden i användargränssnittet](../monitor.md).

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med **[!UICONTROL Delete]** finns i **[!UICONTROL Dataflows]** arbetsyta. Mer information om hur du tar bort dataflöden finns i självstudiekursen om [ta bort dataflöden i användargränssnittet](../delete.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde som hämtar in data från en källa där kunderna lyckades och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av underordnade [!DNL Platform] tjänster som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

I **[!UICONTROL Authentication]** markerar du namnet på kontot som är kopplat till det dataflöde som du vill inaktivera.

![](../../../images/tutorials/dataflow/customer-success/monitor.png)

The **[!UICONTROL Source activity]** visas. Välj det aktiva dataflödet i listan för att öppna dess **[!UICONTROL Properties]** kolumn till höger på skärmen som innehåller en **[!UICONTROL Enabled]** växlingsknapp. Klicka på växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![disable](../../../images/tutorials/dataflow/customer-success/disable.png)

### Aktivera inkommande data för [!DNL Profile] population

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-time Customer Profile] data. Mer information om hur du fyller i [!DNL Real-time Customer Profile] data, se självstudiekursen om [Profilpopulation](../profile.md).
