---
keywords: Experience Platform;hem;populära ämnen;molnlagringskontakt;molnlagring
solution: Experience Platform
title: Konfigurera ett dataflöde för en anslutning för Cloud Storage Streaming i användargränssnittet
topic: overview
type: Tutorial
description: Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en plattformsdatauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med molnlagringsbasen.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---


# Konfigurera ett dataflöde för en direktuppspelningsanslutning för molnlagring i användargränssnittet

Ett dataflöde är en schemalagd aktivitet som hämtar och importerar data från en källa till en [!DNL Platform]-datauppsättning. I den här självstudiekursen beskrivs hur du konfigurerar ett nytt dataflöde med molnlagringsbasen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver dessutom att du redan har skapat en molnlagringskontakt. En lista med självstudiekurser för att skapa olika molnlagringskopplingar i användargränssnittet finns i [översikten över källanslutningar](../../../../home.md).

## Markera data

När du har skapat molnlagringskopplingen visas steget *Markera data*, som ger ett gränssnitt där du kan välja vilken ström du vill direktuppspela data från.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mappa datafält till ett XDM-schema

Steget **[!UICONTROL Mapping]** visas med ett interaktivt gränssnitt för att mappa källdata till en [!DNL Platform]-datauppsättning.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Use existing dataset]** och klickar sedan på datauppsättningsikonen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Dialogrutan **[!UICONTROL Select dataset]** visas. Hitta den datauppsättning du vill använda, markera den och klicka sedan på **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Använd en ny datauppsättning**

Om du vill importera data till en ny datauppsättning väljer du **[!UICONTROL Create new dataset]** och anger ett namn och en beskrivning för datauppsättningen i de angivna fälten. Välj sedan det schema som du vill använda i listrutan.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Namnge dataflödet

Steget **[!UICONTROL Dataflow detail]** visas så att du kan namnge och ge en kort beskrivning av det nya dataflödet.

Ange värden för dataflödet och klicka på **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Granska ditt dataflöde

**[!UICONTROL Review]**-steget visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Source details]**: Visar källtypen och annan relevant information om källan.
- **[!UICONTROL Target details]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** och ger dig tid att skapa dataflödet.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Övervaka och ta bort dataflödet

När ditt molnlagringsdataflöde har skapats kan du övervaka de data som hämtas genom det. Mer information om att övervaka och ta bort dataflöden finns i självstudiekursen om [övervakning av dataflöden](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta in data från en extern molnlagring och fått insikter om att övervaka datauppsättningar. Inkommande data kan nu användas av underordnade [!DNL Platform]-tjänster som [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [[!DNL Real-time Customer Profile] översikt](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] översikt](../../../../../data-science-workspace/home.md)

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med källkopplingar.

### Inaktivera ett dataflöde

När ett dataflöde skapas blir det omedelbart aktivt och importerar data enligt det schema som det gavs. Du kan när som helst inaktivera ett aktivt dataflöde genom att följa instruktionerna nedan.

Klicka på fliken **[!UICONTROL Browse]** på arbetsytan **[!UICONTROL Sources]**. Klicka sedan på namnet på anslutningen som är kopplad till det aktiva dataflöde som du vill inaktivera.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Sidan **[!UICONTROL Source activity]** visas. Markera det aktiva dataflödet i listan för att öppna kolumnen **[!UICONTROL Properties]** till höger på skärmen, som innehåller en alternativknapp för **[!UICONTROL Enabled]**. Klicka på växlingsknappen för att inaktivera dataflödet. Samma växlingsknapp kan användas för att återaktivera ett dataflöde efter att det har inaktiverats.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Aktivera inkommande data för [!DNL Profile]-populationen

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-time Customer Profile]-data. Mer information om hur du fyller i dina [!DNL Real-time Customer Profile]-data finns i självstudiekursen om [profilpopulationen](../../profile.md).
