---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurera ett dataflöde för en batchanslutning för molnlagring i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: dca1accc16395de72db6d0cc8eac78f07dd05e03
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---


# Konfigurera ett dataflöde för en batchanslutning för molnlagring i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med molnlagringsbasen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver dessutom att du redan har skapat en molnlagringskontakt. En lista med självstudiekurser för att skapa olika molnlagringskopplingar i gränssnittet finns i [källanslutningsöversikten](../../../../home.md).

### Filformat som stöds

Experience Platform har stöd för följande filformat som kan importeras från externa lagringsplatser:

* Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
* JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

## Markera data

När du har skapat din molnlagringskontakt visas steget *Välj data* , som ger ett interaktivt gränssnitt där du kan utforska din molnlagringshierarki.

* Den vänstra halvan av gränssnittet är en katalogwebbläsare som visar serverns filer och kataloger.
* I den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en kompatibel fil.

Om du klickar på en mapp i listan kan du gå igenom mapphierarkin till djupare mappar. När du har valt en kompatibel fil eller mapp visas listrutan **Välj dataformat** , där du kan välja ett format för att visa data i förhandsvisningsfönstret.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

När förhandsvisningsfönstret har fyllts i kan du klicka på **Nästa** för att överföra alla filer i den valda mappen. Om du vill överföra till en viss fil markerar du filen i listan innan du klickar på **Nästa**.

>[!NOTE] Filformat som stöds är CSV, JSON och Parquet. JSON- och Parquet-filer måste vara XDM-kompatibla.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-next.png)

## Mappa datafält till ett XDM-schema

Steget *Mappning* visas med ett interaktivt gränssnitt för att mappa källdata till en plattformsdatauppsättning. Källfiler som är formaterade i JSON eller Parquet måste vara XDM-kompatibla och kräver inte att du konfigurerar mappningen manuellt. CSV-filer kräver däremot att du uttryckligen konfigurerar mappningen, men låter dig välja vilka källdatafält som ska mappas.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera data till en befintlig datauppsättning väljer du **Använd befintlig datauppsättning** och klickar sedan på ikonen för datauppsättningen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Dialogrutan _Välj datauppsättning_ visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **Fortsätt**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-data.png)

**Använd en ny datauppsättning**

Om du vill importera data till en ny datauppsättning väljer du **Skapa ny datauppsättning** och anger ett namn och en beskrivning för datauppsättningen i fälten. Klicka sedan på schemaikonen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-schema.png)

Dialogrutan _Välj schema_ visas. Välj det schema som du vill använda för den nya datauppsättningen och klicka sedan på **Klar**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Beroende på dina behov kan du välja att mappa fält direkt eller använda mappningsfunktioner för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om datamappning och mappningsfunktioner finns i självstudiekursen om att [mappa CSV-data till XDM-schemafält](../../../../../ingestion/tutorials/map-a-csv-file.md).

När källdata har mappats klickar du på **Nästa**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

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

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling.png)

## Namnge dataflödet

Steget *Namnflöde* visas, så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Ange värden för dataflödet och klicka på **Nästa**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/name-your-dataflow.png)

### Granska ditt dataflöde

Steget *Granska* visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* *Källinformation*: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* *Målinformation*: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.
* *Schemainformation*: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet klickar du på **Slutför** och anger en tid innan dataflödet skapas.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Övervaka dataflödet

När ditt molnlagringsdataflöde har skapats kan du övervaka de data som hämtas genom det. Mer information om att övervaka datauppsättningar finns i självstudiekursen om [övervakning av dataflöden](../../../../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta in data från en extern molnlagring och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid och datavetenskapen. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../../profile/home.md)
* [Översikt över arbetsytan Datavetenskap](../../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Klicka på fliken *Bläddra* på arbetsytan **Källor** . Klicka sedan på namnet på kontot som är associerat med det aktiva dataflödet som du vill inaktivera.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Sidan *Källaktivitet* visas. Markera det aktiva dataflödet i listan för att öppna kolumnen *Egenskaper* till höger på skärmen, som innehåller en **aktiverad** alternativknapp. Klicka på växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Aktivera inkommande data för profilifyllning

Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid. Mer information om hur du fyller i Real-Customer Profile-data finns i självstudiekursen om [profilpopulationen](../../profile.md).
