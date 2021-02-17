---
keywords: Experience Platform;hem;populära ämnen;direktuppspelningsanslutning;skapa direktuppspelningsanslutning;ui guide;självstudiekurs;skapa en direktuppspelningsanslutning;direktuppspelningsproblem;intag;
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med användargränssnittet
topic: tutorial
type: Tutorial
description: Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Skapa en direktuppspelningsanslutning med användargränssnittet

Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Skapa en direktuppspelningsanslutning

När du har loggat in på gränssnittet [!DNL Experience Platform] väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL HTTP API]** under kategorin **[!UICONTROL Streaming]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny HTTP-direktuppspelningskontakt.

![](../../../../images/tutorials/create/http/catalog.png)

Sidan **[!UICONTROL Connect HTTP API account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett kontonamn och en valfri beskrivning på indataformuläret som visas. Du får också möjlighet att ange följande konfigurationsegenskaper:

- **[!UICONTROL Authentication]:** Den här egenskapen avgör om direktuppspelningsanslutningen kräver autentisering eller inte. Autentisering säkerställer att data samlas in från betrodda källor. Om du har att göra med personligt identifierbar information (PII) ska den här egenskapen aktiveras. Som standard är den här egenskapen inaktiverad.
- **[!UICONTROL XDM Schema Compatibility]:** Den här egenskapen anger om den här direktuppspelningsanslutningen ska skicka händelser som är kompatibla med XDM-scheman. Som standard är den här egenskapen aktiverad.

När du är klar väljer du **[!UICONTROL Connect to source]** följt av **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/http/new-account.png)

### Befintligt konto

Om du vill ansluta med befintliga autentiseringsuppgifter markerar du den HTTP API-anslutning som du vill använda och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/http/existing-account.png)

## Markera data

När du har skapat HTTP API-anslutningen visas **[!UICONTROL Select data]**-steget, som ger ett gränssnitt för att välja vilken datauppsättning som ska anslutas. Du kan antingen skapa en ny datauppsättning eller ansluta till en befintlig datauppsättning.

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning väljer du **[!UICONTROL New dataset]**. På formuläret som visas anger du namn, valfri beskrivning och målschema för datauppsättningen. Om du väljer ett profilaktiverat schema kan du välja om datauppsättningen också ska vara profilaktiverad.

![](../../../../images/tutorials/create/http/new-dataset.png)

### Använd en befintlig datauppsättning

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Markera den datauppsättning som du vill använda i formuläret som visas. När du har valt en datauppsättning kan du välja om datauppsättningen ska vara Profil aktiverad.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## Dataflödesdetaljer

**[!UICONTROL Dataflow detail]**-steget visas. På den här sidan kan du ange information för det skapade dataflödet genom att ange ett namn och en valfri beskrivning.

När du har angett information för dataflödet väljer du **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## Granska

**[!UICONTROL Review]**-steget visas, så att du kan granska informationen om dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection]**: Visar kontonamnet, källplattformen och källnamnet.
- **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och det schema som datauppsättningen följer.

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]**.

![](../../../../images/tutorials/create/http/review.png)

## Hämta URL för direktuppspelningsslutpunkt

När anslutningen har skapats visas informationssidan för källor. På den här sidan visas information om din nya anslutning, inklusive tidigare körda dataflöden, ID och URL för direktuppspelningsslutpunkt.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en direktuppspelad HTTP-anslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att få åtkomst till en mängd olika API:er för [!DNL Data Ingestion]. Instruktioner om hur du skapar en direktuppspelningsanslutning i API:t finns i [självstudiekursen om att skapa en direktuppspelningsanslutning](../../../api/create/streaming/http.md).

Om du vill lära dig att strömma data till plattformen kan du läsa självstudiekursen om [data från tidsserierna för direktuppspelning](../../../../../ingestion/tutorials/streaming-time-series-data.md) eller självstudiekursen om [data för direktuppspelningsposter](../../../../../ingestion/tutorials/streaming-record-data.md).
