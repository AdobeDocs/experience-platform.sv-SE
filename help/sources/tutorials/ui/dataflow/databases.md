---
keywords: Experience Platform;hem;populära ämnen;databasanslutning
solution: Experience Platform
title: Skapa ett dataflöde med hjälp av en databas-Source i användargränssnittet
type: Tutorial
description: Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du skapar ett dataflöde för en databaskälla med hjälp av plattformsgränssnittet.
exl-id: 9fd8a7ec-bbd8-4890-9860-e6defc6cade3
source-git-commit: f5ac10980e08843f6ed9e892f7e1d4aefc8f0de7
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---

# Skapa ett dataflöde med hjälp av en datakälla i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en datauppsättning i Adobe Experience Platform. I den här självstudiekursen beskrivs hur du skapar ett dataflöde för en databaskälla med hjälp av plattformsgränssnittet.

>[!NOTE]
>
>* Om du vill skapa ett dataflöde måste du redan ha ett autentiserat konto med en datakälla. En lista med självstudiekurser för att skapa olika datakällkonton i användargränssnittet finns i [källöversikten](../../../home.md#database).
>
>* För att Experience Platform ska kunna importera data måste tidszoner för alla tabellbaserade batchkällor konfigureras till UTC. Den enda tidsstämpeln som stöds för [[!DNL Snowflake] source](../../../connectors/databases/snowflake.md) är TIMESTAMP_NTZ med UTC-tid.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../home.md): Med plattformen kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [[!DNL Experience Data Model (XDM)] System](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

## Lägg till data

När du har skapat ditt datakällkonto för databasen visas steget **[!UICONTROL Add data]** som ger dig ett gränssnitt där du kan utforska databaskällkontots tabellhierarki.

* Den vänstra halvan av gränssnittet är en webbläsare som visar en lista över datatabeller som finns i ditt konto. Gränssnittet innehåller också ett sökalternativ som gör att du snabbt kan identifiera de källdata som du tänker använda.
* Den högra halvan av gränssnittet är en förhandsgranskningspanel som gör att du kan förhandsgranska upp till 100 rader med data.

>[!NOTE]
>
>Sökkällans dataalternativ är tillgängligt för alla tabellbaserade källor, förutom Adobe Analytics, [!DNL Amazon Kinesis] och [!DNL Azure Event Hubs].

När du har hittat källdata markerar du tabellen och väljer sedan **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Ange information om dataflöde

På sidan [!UICONTROL Dataflow detail] kan du välja om du vill använda en befintlig datauppsättning eller en ny datauppsättning. Under den här processen kan du även konfigurera inställningar för [!UICONTROL Profile dataset], [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion] och [!UICONTROL Alerts].

![dataflödesdetalj](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Använd en befintlig datamängd

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Du kan antingen hämta en befintlig datauppsättning med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga datauppsättningar i listrutan. När du har valt en datauppsättning anger du ett namn och en beskrivning för dataflödet.

![befintlig-datamängd](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Använd en ny datauppsättning

Om du vill importera till en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger sedan ett namn på utdatauppsättningen och en valfri beskrivning. Välj sedan ett schema att mappa till med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga scheman i listrutan. När du har valt ett schema anger du ett namn och en beskrivning för dataflödet.

![ny-datamängd](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Aktivera [!DNL Profile] och feldiagnostik

Välj sedan alternativet **[!UICONTROL Profile dataset]** för att aktivera datauppsättningen för [!DNL Profile]. På så sätt kan du skapa en helhetsbild av en enhets attribut och beteenden. Data från alla [!DNL Profile]-aktiverade datauppsättningar inkluderas i [!DNL Profile] och ändringarna tillämpas när du sparar dataflödet.

[!UICONTROL Error diagnostics] aktiverar detaljerad generering av felmeddelanden för alla felaktiga poster som inträffar i dataflödet, medan [!UICONTROL Partial ingestion] gör att du kan importera data som innehåller fel, upp till ett visst tröskelvärde som du manuellt anger. Mer information finns i [översikten över partiell gruppöverföring](../../../../ingestion/batch-ingestion/partial.md).

![profil-och-fel](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Aktivera aviseringar

Du kan aktivera varningar för att få meddelanden om status för ditt dataflöde. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på källvarningar med användargränssnittet](../alerts.md).

Välj **[!UICONTROL Next]** när du är klar med informationen om dataflödet.

![varningar](../../../images/tutorials/dataflow/table-based/alerts.png)

## Mappa datafält till ett XDM-schema

Steg [!UICONTROL Mapping] visas, och du får ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../../data-prep/ui/mapping.md).

När källdata har mappats väljer du **[!UICONTROL Next]**.

![mappning](../../../images/tutorials/dataflow/table-based/mapping.png)

## Schemalägg körning av inmatning

Steg [!UICONTROL Scheduling] visas, så att du kan konfigurera ett matningsschema så att det automatiskt importerar valda källdata med de konfigurerade mappningarna. Som standard är schemaläggningen inställd på `Once`. Välj **[!UICONTROL Frequency]** och välj sedan ett alternativ i listrutan om du vill justera din inmatningsfrekvens.

>[!TIP]
>
>Intervall och bakåtfyllnad syns inte vid engångsbruk.

![schemaläggning](../../../images/tutorials/dataflow/table-based/scheduling.png)

Om du ställer in matningsfrekvensen på `Minute`, `Hour`, `Day` eller `Week` måste du ange ett intervall för att skapa en fast tidsram mellan varje intag. En matningsfrekvens som till exempel är inställd på `Day` och ett intervall på `15` innebär att dataflödet är schemalagt att importera data var 15:e dag.

Under det här steget kan du även aktivera **bakgrundsfyllning** och definiera en kolumn för inkrementellt dataintag. Backfill används för att importera historiska data, medan kolumnen som du definierar för inkrementellt intag gör att nya data kan skiljas från befintliga data.

Se tabellen nedan för mer information om schemaläggningskonfigurationer.

| Fält | Beskrivning |
| --- | --- |
| Frekvens | Frekvensen med vilken ett intag sker. Valbara frekvenser är `Once`, `Minute`, `Hour`, `Day` och `Week`. |
| Intervall | Ett heltal som anger intervallet för den valda frekvensen. Intervallets värde måste vara ett heltal som inte är noll och måste vara större än eller lika med 15. |
| Starttid | En UTC-tidsstämpel som anger när det allra första intaget är inställt att ske. Starttiden måste vara större än eller lika med den aktuella UTC-tiden. |
| Backfill | Ett booleskt värde som avgör vilka data som hämtas från början. Om bakåtfyllning är aktiverad, kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. Om underfyllning är inaktiverad importeras endast de filer som läses in mellan den första importkörningen och starttiden. Filer som lästs in före starttiden importeras inte. |
| Läs in inkrementella data med | Ett alternativ med en filtrerad uppsättning källschemafält av typen, datumet eller tiden. Fältet som du väljer för **[!UICONTROL Load incremental data by]** måste ha sina datum- och tidsvärden i UTC-tidszonen för att inkrementella data ska kunna läsas in korrekt. Alla tabellbaserade batchkällor hämtar inkrementella data genom att jämföra ett deltskolumnens tidsstämpelvärde med motsvarande körningsfönster UTC-tid och sedan kopiera data från källan, om nya data hittas i UTC-tidsfönstret. |

![bakgrundsfyllning](../../../images/tutorials/dataflow/table-based/backfill.png)

## Granska ditt dataflöde

Steg **[!UICONTROL Review]** visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer.
* **[!UICONTROL Scheduling]**: Visar den aktiva perioden, frekvensen och intervallet för intag-schemat.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![granskning](../../../images/tutorials/dataflow/table-based/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden i användargränssnittet](../monitor.md).

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen om att [ta bort dataflöden i användargränssnittet](../delete.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde som hämtar data från databaskällan till plattformen. Inkommande data kan nu användas av [!DNL Platform]-tjänster längre fram i kedjan, till exempel [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

* [[!DNL Real-Time Customer Profile] översikt](../../../../profile/home.md)
* [[!DNL Data Science Workspace] översikt](../../../../data-science-workspace/home.md)
