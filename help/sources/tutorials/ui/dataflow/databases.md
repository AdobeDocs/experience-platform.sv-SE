---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurera ett dataflöde för en databasanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---


# Konfigurera ett dataflöde för en databasanslutning i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med ditt databaskonto.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) System](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat ett databaskonto. En lista med självstudiekurser för att skapa olika databasanslutningar i användargränssnittet finns i [källanslutningsöversikten](../../../home.md).

## Markera data

När du har skapat ditt databaskonto visas **[!UICONTROL Select data]** steget och du får ett interaktivt gränssnitt där du kan utforska databashierarkin.

- Den vänstra halvan av gränssnittet är en webbläsare som visar kontots lista över databaser.
- I den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader med data.

Markera den databas som du vill använda och klicka sedan på **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/add-data.png)

## Mappa datafält till ett XDM-schema

Steget *Mappning* visas med ett interaktivt gränssnitt för att mappa källdata till en plattformsdatauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

### Använd en befintlig datauppsättning

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** och klickar sedan på datamängdikonen .

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

Dialogrutan **[!UICONTROL Select dataset]** visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **[!UICONTROL Continue]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Använd en ny datauppsättning

Om du vill importera data till en ny datauppsättning markerar du **[!UICONTROL New dataset]** och anger ett namn och en beskrivning för datauppsättningen i de angivna fälten.

Du kan bifoga ett schemafält genom att ange ett schemanamn i **[!UICONTROL Select schema]** sökfältet. Du kan också välja listruteikonen för att visa en lista över befintliga scheman. Du kan också välja **[!UICONTROL Advanced search]** att få åtkomst till skärmen med befintliga scheman, inklusive deras respektive detaljer.

![create-new-dataset](../../../images/tutorials/dataflow/all-tabular/new-target-dataset.png)

Dialogrutan **[!UICONTROL Select schema]** visas. Välj det schema som du vill använda för den nya datauppsättningen och klicka sedan på **[!UICONTROL Done]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda mappningsfunktioner för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om datamappning och mappningsfunktioner finns i självstudiekursen om att [mappa CSV-data till XDM-schemafält](../../../../ingestion/tutorials/map-a-csv-file.md).

När källdata har mappats klickar du på **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/all-tabular/mapping-updated.png)

## Schemalägg körning av inmatning

Steget visas så att du kan konfigurera ett schema för att automatiskt importera valda källdata med de konfigurerade mappningarna. **[!UICONTROL Scheduling]** I följande tabell visas de olika konfigurerbara fälten för schemaläggning:

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Valbara frekvenser inkluderar `Once`, `Minute`, `Hour`, `Day`och `Week`. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. |
| Starttid | En UTC-tidsstämpel som anger när det allra första intaget är inställt. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. Om **[!UICONTROL Backfill]** är aktiverat importeras alla aktuella filer i den angivna sökvägen under den första schemalagda importen. Om **[!UICONTROL Backfill]** är inaktiverat importeras endast de filer som är inlästa mellan den första importen och den andra **[!UICONTROL Start time]** . Filer som lästs in tidigare **[!UICONTROL Start time]** kommer inte att importeras. |
| Delta-kolumn | Ett alternativ med en filtrerad uppsättning källschemafält av typen, datumet eller tiden. Det här fältet används för att skilja mellan nya och befintliga data. Inkrementella data importeras baserat på tidsstämpeln för den markerade kolumnen. |

Dataflöden är utformade för att automatiskt importera data enligt schema. Börja med att välja intagsfrekvens. Ange sedan intervallet för att ange perioden mellan två flödeskörningar. Intervallets värde måste vara ett heltal som inte är noll och måste vara större än eller lika med 15.

Om du vill ange starttid för intaget justerar du datumet och tiden som visas i rutan för starttid. Du kan också välja kalenderikonen för att redigera starttidsvärdet. Starttiden måste vara större än eller lika med den aktuella UTC-tiden.

Välj **[!UICONTROL Load incremental data by]** att tilldela deltakolumnen. I det här fältet görs en skillnad mellan nya och befintliga data.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Konfigurera ett dataflöde för engångsbruk

Om du vill ställa in engångsintag väljer du den nedrullningsbara pilen för frekvens och väljer **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** och **[!UICONTROL Backfill]** inte är synliga vid engångsbruk.

När du har angett lämpliga värden för schemat väljer du **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Ange information om dataflöde

Stegen visas så att du kan ange ett namn och en kort beskrivning av det nya dataflödet. **[!UICONTROL Dataflow detail]**

Under den här processen kan du även aktivera **[!UICONTROL Partial ingestion]** och **[!UICONTROL Error diagnostics]**. Aktivering **[!UICONTROL Partial ingestion]** ger möjlighet att importera data som innehåller fel upp till ett visst tröskelvärde. När **[!UICONTROL Partial ingestion]** det är aktiverat drar du i **[!UICONTROL Error threshold %]** reglaget för att justera batchens feltröskel. Du kan också justera tröskelvärdet manuellt genom att markera inmatningsrutan. Mer information finns i översikten över [partiell gruppöverföring](../../../../ingestion/batch-ingestion/partial.md).
Ange värden för dataflödet och välj **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Granska ditt dataflöde

Steget visas så att du kan granska det nya dataflödet innan det skapas. **[!UICONTROL Review]** Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
- **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
- **[!UICONTROL Scheduling]**: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet kan du klicka **[!UICONTROL Finish]** och vänta tills dataflödet har skapats.

![](../../../images/tutorials/dataflow/databases/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen om [övervakning av konton och dataflöden i användargränssnittet](../monitor.md).

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med den **[!UICONTROL Delete]** funktion som finns på **[!UICONTROL Dataflows]** arbetsytan. Mer information om hur du tar bort dataflöden finns i självstudiekursen om hur du [tar bort dataflöden i användargränssnittet](../delete.md).

## Nästa steg

I den här självstudiekursen har du skapat ett dataflöde som hämtar in data från en extern databas och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av [!DNL Platform] tjänster längre fram i kedjan som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [[!DNL Real-time Customer Profile] översikt](../../../../profile/home.md)
- [[!DNL Data Science Workspace] översikt](../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Markera fliken på **[!UICONTROL Sources]** arbetsytan **[!UICONTROL Dataflows]** . Välj sedan det dataflöde som du vill inaktivera.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

Kolumnen visas till höger på skärmen, inklusive en **[!UICONTROL Properties]** **[!UICONTROL Enabled]** växlingsknapp. Markera växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Aktivera inkommande data för [!DNL Profile] populationen

Inkommande data från källkopplingen kan användas för att berika och fylla i dina [!DNL Real-time Customer Profile] data. Mer information om hur du fyller i dina [!DNL Real-time Customer Profile] data finns i självstudiekursen om [profilpopulationen](../profile.md).