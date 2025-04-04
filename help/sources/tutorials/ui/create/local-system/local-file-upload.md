---
keywords: Experience Platform;home;populära topics;local system;file upload;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Skapa en lokal filöverföring för Source Connector i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning för det lokala systemet för att överföra lokala filer till Experience Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Skapa en lokal källanslutning för filöverföring i användargränssnittet

I den här självstudiekursen får du hjälp med att skapa en lokal filöverföringsanslutning för att importera lokala filer till Experience Platform med användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Överför lokala filer till Experience Platform

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Local system] väljer du **[!UICONTROL Local file upload]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/local/catalog.png)

### Använd en befintlig datamängd

På sidan [!UICONTROL Dataflow detail] kan du välja om du vill importera dina CSV-data till en befintlig datamängd eller en ny datamängd.

Om du vill importera dina CSV-data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Du kan antingen hämta en befintlig datauppsättning med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga datauppsättningar i listrutan.

Ange ett namn för dataflödet och en valfri beskrivning när du har valt en datauppsättning.

Under den här processen kan du även aktivera [!UICONTROL Error diagnostics] och [!UICONTROL Partial ingestion]. [!UICONTROL Error diagnostics] aktiverar detaljerad generering av felmeddelanden för alla felaktiga poster som inträffar i dataflödet, medan [!UICONTROL Partial ingestion] gör att du kan importera data som innehåller fel, upp till ett visst tröskelvärde som du manuellt anger. Mer information finns i [översikten över partiell gruppöverföring](../../../../../ingestion/batch-ingestion/partial.md).

![befintlig-datamängd](../../../../images/tutorials/create/local/existing-dataset.png)

### Använd en ny datauppsättning

Om du vill importera dina CSV-data till en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger sedan ett namn på utdatauppsättningen och en valfri beskrivning. Välj sedan ett schema att mappa till med alternativet [!UICONTROL Advanced search] eller genom att bläddra igenom listan med befintliga scheman i listrutan.

När du har valt ett schema anger du ett namn för dataflödet och en valfri beskrivning och tillämpar sedan de [!UICONTROL Error diagnostics]- och [!UICONTROL Partial ingestion]-inställningar du vill använda för dataflödet. När du är klar väljer du **[!UICONTROL Next]**.

![ny-datamängd](../../../../images/tutorials/create/local/new-dataset.png)

### Markera data

[!UICONTROL Select data]-steget visas med ett gränssnitt för att överföra dina lokala filer och förhandsgranska deras struktur och innehåll. Välj **[!UICONTROL Choose files]** om du vill överföra en CSV-fil från det lokala systemet. Du kan också dra och släppa den CSV-fil som du vill överföra till panelen [!UICONTROL Drag and drop files].

>[!TIP]
>
>Endast CSV-filer stöds för närvarande av lokal filöverföring. Den största filstorleken för varje fil är 1 GB.

![välj-filer](../../../../images/tutorials/create/local/choose-files.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa filens innehåll och struktur.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Beroende på vilken fil du har kan du välja en kolumnavgränsare, t.ex. tabbar, kommatecken, rör eller en anpassad kolumnavgränsare för källdata. Välj listrutepilen **[!UICONTROL Delimiter]** och välj sedan lämplig avgränsare på menyn.

När du är klar väljer du **[!UICONTROL Next]**.

![delimiter](../../../../images/tutorials/create/local/delimiter.png)

## Mappning

Steg [!UICONTROL Mapping] visas, och du får ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet finns i [Användargränssnittshandboken för dataförberedelser](../../../../../data-prep/ui/mapping.md).

När mappningsuppsättningarna är klara väljer du **[!UICONTROL Finish]** och tillåt en stund för att skapa det nya dataflödet.

![mappning](../../../../images/tutorials/create/local/mapping.png)

## Övervaka datainmatning

När CSV-filen har mappats och skapats kan du övervaka de data som importeras via den via kontrollpanelen. Mer information finns i självstudiekursen [Övervaka källans dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

## Nästa steg

I den här självstudiekursen har du mappat en platt CSV-fil till ett XDM-schema och infogat den i Experience Platform. Dessa data kan nu användas av [!DNL Experience Platform]-tjänster längre fram i kedjan, till exempel [!DNL Real-Time Customer Profile]. Mer information finns i översikten för [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md).
