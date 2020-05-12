---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurera ett dataflöde för en databasanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 415b59fc3fa20c09372549e92571c1b41006e540
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---


# Konfigurera ett dataflöde för en databasanslutning i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med databasanslutningen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat en databaskoppling. En lista med självstudiekurser för att skapa olika databasanslutningar i användargränssnittet finns i [källanslutningsöversikten](../../../home.md).

## Markera data

När du har skapat en databaskoppling visas *[!UICONTROL Select data]* steget och du får ett interaktivt gränssnitt där du kan utforska databashierarkin.

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

Dialogrutan *[!UICONTROL Select dataset]* visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **[!UICONTROL Continue]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Använd en ny datauppsättning

Om du vill importera data till en ny datauppsättning markerar du **[!UICONTROL New dataset]** och anger ett namn och en beskrivning för datauppsättningen i de angivna fälten.

Du kan bifoga ett schemafält genom att skriva ett schemanamn i **[!UICONTROL Select schema]** sökfältet. Du kan också välja listruteikonen för att visa en lista över befintliga scheman. Du kan också välja **[!UICONTROL Advanced search]** att visa befintliga scheman, inklusive deras respektive detaljer.

![](../../../images/tutorials/dataflow/databases/new-dataset.png)

Dialogrutan *[!UICONTROL Select schema] visas. Välj det schema som du vill använda för den nya datauppsättningen och klicka sedan på **[!UICONTROL Done]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda mappningsfunktioner för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om datamappning och mappningsfunktioner finns i självstudiekursen om att [mappa CSV-data till XDM-schemafält](../../../../ingestion/tutorials/map-a-csv-file.md).

När källdata har mappats klickar du på **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/mapping.png)

## Schemalägg körning av inmatning

Steget visas så att du kan konfigurera ett schema för att automatiskt importera valda källdata med de konfigurerade mappningarna. *[!UICONTROL Scheduling]* I följande tabell visas de olika konfigurerbara fälten för schemaläggning:

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Valbara frekvenser är Minute, Hour, Day och Week. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. |
| Starttid | En UTC-tidsstämpel för vilken det allra första intaget sker. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. Om *Backfill* är aktiverat, kommer alla aktuella filer i den angivna sökvägen att kapslas in under det första schemalagda intaget. Om *Backfill* är inaktiverat kapslas endast de filer som läses in mellan den första importkörningen och *starttiden* . Filer som lästs in före *starttiden* importeras inte. |
| Delta-kolumn | Ett alternativ med en filtrerad uppsättning källschemafält av typen, datumet eller tiden. Det här fältet används för att skilja mellan nya och befintliga data. Inkrementella data importeras baserat på tidsstämpeln för den markerade kolumnen. |

Dataflöden är utformade för att automatiskt importera data enligt schema. Om du bara vill importera en gång genom det här arbetsflödet kan du göra det genom att konfigurera **[!UICONTROL Frequency]** till &quot;Dag&quot; och använda ett mycket stort tal för **[!UICONTROL Interval]** fotot, till exempel 10000 eller liknande.

Ange värden för schemat och välj **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule.png)

## Namnge dataflödet

Stegen visas där du måste ange ett namn och en valfri beskrivning för dataflödet. *[!UICONTROL dataflow detail]* Steget visas. Välj **[!UICONTROL Next]** när du är klar.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Granska ditt dataflöde

Steget visas så att du kan granska det nya dataflödet innan det skapas. *[!UICONTROL Review]* Informationen är grupperad i följande kategorier:

- *Anslutning*: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
- *Tilldela datauppsättnings- och kartfält*: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
- *Schemaläggning*: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet kan du klicka **[!UICONTROL Finish]** och vänta tills dataflödet har skapats.

![](../../../images/tutorials/dataflow/databases/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det. Mer information om hur du övervakar dataflöden finns i självstudiekursen om [konton och dataflöden](../monitor.md).

## Nästa steg

I den här självstudiekursen har du skapat ett dataflöde som hämtar in data från en extern databas och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid och datavetenskapen. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Markera fliken på *[!UICONTROL Sources]* arbetsytan **[!UICONTROL Dataflowss]** . Välj sedan det dataflöde som du vill inaktivera.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

Kolumnen *Egenskaper* visas till höger på skärmen, inklusive en **[!UICONTROL Enabled]** växlingsknapp. Markera växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Aktivera inkommande data för profilifyllning

Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid. Mer information om hur du fyller i Real-Customer Profile-data finns i självstudiekursen om [profilpopulationen](../profile.md).