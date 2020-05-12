---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurera ett dataflöde för en direktuppspelningskontakt för molnlagring i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: dca1accc16395de72db6d0cc8eac78f07dd05e03
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Konfigurera ett dataflöde för en direktuppspelningskontakt för molnlagring i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med molnlagringsbasen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver dessutom att du redan har skapat en molnlagringskontakt. En lista med självstudiekurser för att skapa olika molnlagringskopplingar i gränssnittet finns i [källanslutningsöversikten](../../../../home.md).

## Markera data

När du har skapat molnlagringskopplingen visas steget *Välj data* , som ger dig ett gränssnitt där du kan välja vilken ström du vill direktuppspela data från.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mappa datafält till ett XDM-schema

Steget *Mappning* visas med ett interaktivt gränssnitt för att mappa källdata till en plattformsdatauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera data till en befintlig datauppsättning väljer du **Använd befintlig datauppsättning** och klickar sedan på ikonen för datauppsättningen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Dialogrutan _Välj datauppsättning_ visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **Fortsätt**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Använd en ny datauppsättning**

Om du vill importera data till en ny datauppsättning väljer du **Skapa ny datauppsättning** och anger ett namn och en beskrivning för datauppsättningen i fälten. Välj sedan det schema som du vill använda i listrutan.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Namnge dataflödet

I *Dataflödets detaljsteg* kan du namnge och ge en kort beskrivning av det nya dataflödet.

Ange värden för dataflödet och klicka på **Nästa**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Granska ditt dataflöde

Steget *Granska* visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- *Källinformation*: Visar källtypen och annan relevant information om källan.
- *Målinformation*: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet klickar du på **Slutför** och anger en tid innan dataflödet skapas.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Övervaka dataflödet

När ditt molnlagringsdataflöde har skapats kan du övervaka de data som hämtas genom det. Mer information om att övervaka datauppsättningar finns i självstudiekursen om [övervakning av dataflöden](../../../../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta in data från en extern molnlagring och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid och datavetenskapen. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Klicka på fliken *Bläddra* på arbetsytan **Källor** . Klicka sedan på namnet på den basanslutning som är associerad med det aktiva dataflöde som du vill inaktivera.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Sidan *Källaktivitet* visas. Markera det aktiva dataflödet i listan för att öppna kolumnen *Egenskaper* till höger på skärmen, som innehåller en **aktiverad** alternativknapp. Klicka på växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Aktivera inkommande data för profilifyllning

Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid. Mer information om hur du fyller i Real-Customer Profile-data finns i självstudiekursen om [profilpopulationen](../../profile.md).
