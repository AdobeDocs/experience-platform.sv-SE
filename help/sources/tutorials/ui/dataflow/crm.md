---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurera ett dataflöde för en CRM-koppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 55fa2d9ca706f9d80bf5011811ec5939f690ba05

---


# Konfigurera ett dataflöde för en CRM-koppling i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med CRM-basanslutningen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat en CRM-koppling. En lista med självstudiekurser för att skapa olika CRM-anslutningar i användargränssnittet finns i [källanslutningsöversikten](../../../home.md).

## Markera data

När du har skapat CRM-anslutningen visas steget *Välj data* , som ger ett interaktivt gränssnitt där du kan utforska filhierarkin.

* Den vänstra halvan av gränssnittet är en katalogwebbläsare som visar serverns filer och kataloger.
* I den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en kompatibel fil.

Markera den katalog som du vill använda och klicka sedan på **Nästa**.

![select-data](../../../images/tutorials/dataflow/crm/select-data.png)

## Mappa datafält till ett XDM-schema

Steget *Mappning* visas med ett interaktivt gränssnitt för att mappa källdata till en plattformsdatauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

### Använd en befintlig datauppsättning

Om du vill importera data till en befintlig datauppsättning väljer du **Använd befintlig datauppsättning** och klickar sedan på ikonen för datauppsättningen.

![use-existing-dataset](../../../images/tutorials/dataflow/crm/use-existing-dataset.png)

Dialogrutan _Välj datauppsättning_ visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **Fortsätt**.

![select-existing-dataset](../../../images/tutorials/dataflow/crm/select-existing-dataset.png)

### Använd en ny datauppsättning

Om du vill importera data till en ny datauppsättning väljer du **Skapa ny datauppsättning** och anger ett namn och en beskrivning för datauppsättningen i fälten. Klicka sedan på schemaikonen.

![use-new-dataset](../../../images/tutorials/dataflow/crm/use-new-dataset.png)

Dialogrutan _Välj schema_ visas. Välj det schema som du vill använda för den nya datauppsättningen och klicka sedan på **Klar**.

![select-schema](../../../images/tutorials/dataflow/crm/select-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda mappningsfunktioner för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om datamappning och mappningsfunktioner finns i självstudiekursen om att [mappa CSV-data till XDM-schemafält](../../../../ingestion/tutorials/map-a-csv-file.md).

När källdata har mappats klickar du på **Nästa**.

## Schemalägg körning av inmatning

Steget *Schemaläggning* visas, så att du kan konfigurera ett schema så att det automatiskt importerar valda källdata med de konfigurerade mappningarna. I följande tabell visas de olika konfigurerbara fälten för schemaläggning:

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Valbara frekvenser är Minute, Hour, Day och Week. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. |
| Starttid | En UTC-tidsstämpel för vilken det allra första intaget sker. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. Om *Backfill* är aktiverat, kommer alla aktuella filer i den angivna sökvägen att kapslas in under det första schemalagda intaget. Om *Backfill* är inaktiverat kapslas endast de filer som läses in mellan den första importkörningen och *starttiden* . Filer som lästs in före *starttiden* importeras inte. |

Dataflöden är utformade för att automatiskt importera data enligt schema. Om du bara vill importera en gång genom det här arbetsflödet kan du göra det genom att konfigurera **Frekvensen** till &quot;Dag&quot; och använda ett mycket stort värde för **Intervall**, till exempel 10000 eller liknande.

Ange värden för schemat och klicka på **Nästa**.

![schemaläggning](../../../images/tutorials/dataflow/crm/scheduling.png)

## Namnge dataflödet

Steget *Namnflöde* visas där du måste ange ett namn och en valfri beskrivning av dataflödet. Klicka på **Nästa** när du är klar.

![name-dataflow](../../../images/tutorials/dataflow/crm/name-dataflow.png)

## Granska ditt dataflöde

Steget *Granska* visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* *Anslutningsinformation*: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* *Mappningsinformation*: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
* *Schemainformation*: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet klickar du på **Slutför** och anger en tid innan dataflödet skapas.

![recension](../../../images/tutorials/dataflow/crm/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det. Följ stegen nedan för att komma åt dataflödets datauppsättningsövervakare.

På arbetsytan _Källor_ väljer du den CRM-källa som du vill visa under kategorin *CRM* . Välj *Anslut källa* för att starta autentiseringsgränssnittet. Om du vill visa ett befintligt dataflöde väljer du *Befintligt konto* och väljer det konto som du vill komma åt.

![monitor](../../../images/tutorials/dataflow/crm/monitor.png)

Skärmen *Källaktivitet* visas. Klicka på namnet på en datauppsättning vars aktivitet du vill övervaka.

![select-dataflow-dataset](../../../images/tutorials/dataflow/crm/select-dataflow-dataset.png)

Aktivitetsskärmen *för* datauppsättning visas. På den här sidan visas hur många meddelanden som används i form av ett diagram.

![datauppsättningsaktivitet](../../../images/tutorials/dataflow/crm/dataset-activity.png)

Mer information om övervakning av datauppsättningar och förtäring finns i självstudiekursen om [övervakning av dataflöden](../../../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Nästa steg

I den här självstudiekursen har du skapat ett dataflöde för att hämta in data från en CRM och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid och datavetenskapen. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../profile/home.md)
* [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

På *autentiseringsskärmen* markerar du namnet på den basanslutning som är kopplad till det dataflöde som du vill inaktivera.

![](../../../images/tutorials/dataflow/crm/monitor.png)

Sidan _Källaktivitet_ visas. Markera det aktiva dataflödet i listan för att öppna kolumnen *Egenskaper* till höger på skärmen, som innehåller en **aktiverad** alternativknapp. Klicka på växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![disable](../../../images/tutorials/dataflow/crm/disable.png)

### Aktivera inkommande data för profilifyllning

Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid. Mer information om hur du fyller i Real-Customer Profile-data finns i självstudiekursen om [profilpopulationen](../profile.md).