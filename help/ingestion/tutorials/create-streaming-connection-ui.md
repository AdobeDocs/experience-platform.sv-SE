---
keywords: Experience Platform;hem;populära ämnen;direktuppspelningsanslutning;skapa direktuppspelningsanslutning;ui guide;självstudiekurs;skapa en direktuppspelningsanslutning;direktuppspelningsproblem;intag;
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med användargränssnittet
topic: tutorial
type: Tutorial
description: Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Skapa en direktuppspelningsanslutning med användargränssnittet

Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.

## Komma igång

För att kunna starta direktuppspelning av data till [!DNL Experience Platform] måste du först skapa en direktuppspelad HTTP-anslutning. När du skapar en direktuppspelningsanslutning måste du ange nyckeldetaljer som till exempel källan för direktuppspelningsdata och om du tänker skicka data från en tillförlitlig (autentiserad) eller en otillförlitlig (ej autentiserad) källa eller inte.

När du har registrerat en direktuppspelningsanslutning får du en unik URL som kan användas för att strömma data till [!DNL Platform].

Observera att du måste ha tillgång till Adobe Experience Platform för att kunna slutföra den här guiden. Om du inte har åtkomst till [!DNL Platform] kontaktar du systemadministratören innan du fortsätter.

## Skapa en direktuppspelningsanslutning

När du har loggat in på användargränssnittet för [!DNL Experience Platform] klickar du på **[!UICONTROL Sources]** för att öppna fliken **[!UICONTROL Catalog]**. På den här sidan visas tillgängliga källtyper som enskilda kort, där varje kort innehåller en bubbla som visar antalet dataflöden som har skapats från direktuppspelningsanslutningar till datauppsättningar.

![](../images/streaming-ingestion/ui/click-sources.png)

På sidan **[!UICONTROL Sources]** klickar du på **[!UICONTROL HTTP API]** och sedan på **[!UICONTROL Connect source]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Skärmen **[!UICONTROL Connect to HTTP]** visas. Under **[!UICONTROL Service details]** anger du både namnet och en beskrivning för den nya direktuppspelningsanslutningen.

Under **[!UICONTROL Account Authentication]** väljer du följande konfigurationsegenskaper för din direktuppspelningsanslutning:

- **[!UICONTROL Authentication]:** Om direktuppspelningsanslutningen kräver autentisering eller inte. Autentisering säkerställer att data samlas in från betrodda källor. Vi rekommenderar att detta är aktiverat om det handlar om personligt identifierbar information (PII).
- **[!UICONTROL XDM Schema Compatibility]:** Om den här direktuppspelningsanslutningen skickar händelser som är kompatibla med XDM-scheman eller inte. Som standard är den här egenskapen **på**.

När du har valt konfigurationsegenskaper klickar du på **[!UICONTROL Connect]**. Din HTTP-direktuppspelningsanslutning har skapats och kan nu visas på fliken **[!UICONTROL Browse]** på arbetsytan **[!UICONTROL Sources]**.

![](../images/streaming-ingestion/ui/http-sources-details.png)

På fliken **[!UICONTROL Browse]** kan du klicka på din nyligen skapade Streaming HTTP Connection och visa information om anslutningen.

![](../images/streaming-ingestion/ui/browse-sources.png)

Genom att klicka på hyperlänken för anslutningsnamnet kan du välja vilka data som ska visas genom att konfigurera vilken datauppsättning som ska anslutas genom att klicka på **[!UICONTROL Select data]**.

![](../images/streaming-ingestion/ui/select-data.png)

Du kan antingen [skapa en ny datamängd](#create-a-new-dataset) eller [använda en befintlig datamängd](#use-an-existing-dataset).

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning anger du namn, beskrivning och målschema för datauppsättningen.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

När du infogar all information och klickar på **[!UICONTROL Next]** kan du granska den angivna informationen innan du klickar på **[!UICONTROL Finish]** för att ansluta datauppsättningen till din HTTP-direktuppspelningsanslutning.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Använd en befintlig datauppsättning

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Output dataset name]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

När du har klickat på **[!UICONTROL Next]** kan du granska informationen innan du klickar på **[!UICONTROL Finish]** för att ansluta den valda datauppsättningen till din HTTP-direktuppspelningsanslutning.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en direktuppspelad HTTP-anslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att få åtkomst till en mängd olika API:er för [!DNL Data Ingestion]. Instruktioner om hur du skapar en direktuppspelningsanslutning i API:t finns i [självstudiekursen om att skapa en direktuppspelningsanslutning](../tutorials/create-streaming-connection.md).
