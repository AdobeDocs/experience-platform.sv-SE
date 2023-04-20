---
title: Skapa en anslutning och ett dataflöde för att förminska direktuppspelningen i användargränssnittet
description: Lär dig hur du skapar en Shopify Streaming-källanslutning och ett dataflöde med hjälp av användargränssnittet för plattformen
badge: "Beta"
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för [!DNL Shopify Streaming] data med användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Shopify Streaming] källanslutning och dataflöde med användargränssnittet för plattformen.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

>[!IMPORTANT]
>
>Den här självstudiekursen kräver att du har slutfört nödvändiga inställningar för [!DNL Shopify Streaming] konto. Information om hur du konfigurerar ditt konto finns i [[!DNL Shopify Streaming] översikt](../../../../connectors/ecommerce/shopify-streaming.md).

## Koppla samman [!DNL Shopify Streaming] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **eCommerce** kategori, välj [!DNL Shopify Streaming]och sedan markera **[!UICONTROL Add data]**.

![Katalogen för Experience Platform-källor](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Markera data

The **[!UICONTROL Select data]** visas, där du får ett gränssnitt där du kan välja de data som ska hämtas till plattformen.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** för att överföra en JSON-fil från ditt lokala system. Du kan också dra och släppa den JSON-fil som du vill överföra till [!UICONTROL Drag and drop files] -panelen.

![Steget Lägg till data i källarbetsflödet.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda [!UICONTROL Search field] för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Dataflödesdetaljer

The **Dataflödesdetaljer** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Mappning

The [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du väljer. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Granska

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** så att dataflödet kan skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Hämta din URL för direktuppspelningsslutpunkt

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform.

Gå till [!UICONTROL Dataflow activity] sidan med dataflödet som du just skapade och kopierar slutpunkten från nederkanten av [!UICONTROL Properties] -panelen.

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en källanslutning och ett dataflöde till din [!DNL Shopify Streaming] konto. Instruktioner om hur du ansluter [!DNL Shopify Streaming] med API:t, läs självstudiekursen om [skapa en källanslutning och ett dataflöde för direktuppspelning [!DNL Shopify] data med API:t för Flow Service](../../../api/create/ecommerce/shopify-streaming.md).

