---
title: Skapa en Pendo-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Pendo-källanslutning med Adobe Experience Platform-gränssnittet.
badge: "Beta"
source-git-commit: 5a199262acd517516b1e5313a25ddff8f1b11959
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Skapa en [!DNL Pendo] källanslutningsdataflöde och i användargränssnittet

>[!NOTE]
>
>The [!DNL Pendo] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Pendo] källanslutning och dataflöde med Adobe Experience Platform användargränssnitt.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Förutsättningar {#prerequisites}

Följande avsnitt innehåller information om krav som måste utföras innan du kan skapa en [!DNL Pendo] källanslutning.

### Exempel-JSON för att definiera källschemat för [!DNL Pendo] {#prerequisites-json-schema}

Innan du skapar en [!DNL Pendo] källanslutning, du måste ange ett källschema. Du kan använda JSON nedan.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Mer information finns i [[!DNL Pendo] guide på webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Skapa ett plattformsschema för [!DNL Pendo] {#create-platform-schema}

Du måste också se till att du först skapar ett plattformsschema som kan användas för källan. Se självstudiekursen om [skapa ett plattformsschema](../../../../../xdm/schema/composition.md) om du vill ha omfattande anvisningar om hur du skapar ett schema.

![Plattformsgränssnittet visar ett exempelschema för Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Koppla samman [!DNL Pendo] konto {#connect-account}

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] och se en katalog med källor i Experience Platform.

Använd *[!UICONTROL Categories]* meny för att filtrera källor efter kategori. Du kan också ange ett källnamn i sökfältet för att hitta en viss källa från katalogen.

Gå till [!UICONTROL Analytics] för att se [!DNL Pendo] källkort. Börja genom att välja **[!UICONTROL Add data]**.

![Plattformsgränssnittets källkatalog med Pendo-kortet.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Markera data {#select-data}

The **[!UICONTROL Select data]** visas, där du får ett gränssnitt där du kan välja vilka data du vill hämta till plattformen.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** för att överföra en JSON-fil från ditt lokala system. Du kan också dra och släppa den JSON-fil som du vill överföra till [!UICONTROL Drag and drop files] -panelen.

![Steget Lägg till data i källarbetsflödet.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda [!UICONTROL Search field] för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Dataflödesdetaljer {#dataflow-detail}

The **Dataflödesdetaljer** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappning {#mapping}

The [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

Mappningarna som anges nedan är obligatoriska och bör konfigureras innan du fortsätter till [!UICONTROL Review] stage.

| Målfält | Beskrivning |
| --- | --- |
| `uniqueId` | The [!DNL Pendo] identifierare för händelsen. |

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Granska {#review}

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** så att dataflödet kan skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Hämta din URL för direktuppspelningsslutpunkt {#get-streaming-endpoint-url}

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform.

För att kunna skapa den URL som används för att konfigurera webbhoten på [!DNL Pendo] du måste hämta följande:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Så här hämtar du **[!UICONTROL Dataflow ID]** och **[!UICONTROL Streaming endpoint]**, går till [!UICONTROL Dataflow activity] sidan med dataflödet som du just skapade och kopierar informationen från nederkanten av [!UICONTROL Properties] -panelen.

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

När du har hämtat ditt slutpunkts- och dataflödes-ID för direktuppspelning skapar du en URL baserat på följande mönster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. En webbkrok-URL kan till exempel se ut så här: ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Konfigurera webkrok i [!DNL Pendo] {#set-up-webhook}

Logga sedan in på ditt konto på [[!DNL Pendo]](https://pendo.io/) och skapa en webkrok. För steg om hur du skapar en webkrok med [!DNL Pendo] användargränssnittet, se [[!DNL Pendo] guide om att skapa webkrok](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Navigera till inställningssidan för [!DNL Pendo] webkrok och ange din webkroks-URL i [!DNL URL] fält.

![Skärmbilden för Pendo-gränssnittet visar webbkrokslutpunktsfältet](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Du kan prenumerera på olika händelsekategorier för att avgöra vilken typ av händelser du vill skicka från din [!DNL Pendo] -instans till plattform. Mer information om de olika händelserna finns i [[!DNL Pendo] dokumentation](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du konfigurerat ett dataflöde för direktuppspelning för att [!DNL Pendo] data till Experience Platform. Om du vill övervaka de data som importeras läser du i guiden på [övervaka strömmande dataflöden med hjälp av plattformsgränssnitt](../../monitor-streaming.md).

## Ytterligare resurser {#additional-resources}

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL Pendo] källa.

### Validering {#validation}

För att verifiera att du har konfigurerat källan och [!DNL Pendo] meddelanden importeras, följ stegen nedan:

* Du kan kontrollera [!DNL Pendo] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** för att identifiera de händelser som spelas in av [!DNL Pendo].

![Pendo UI, skärmbild som visar chatthistorik](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Välj **[!UICONTROL View Dataflows]** bredvid [!DNL Pendo] kortmenyn i källkatalogen. Nästa, välj **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats för de webbböcker som du har konfigurerat i [!DNL Pendo].

![Skärmbild av användargränssnittet för plattformen med inkapslade händelser](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Fel och felsökning {#errors-and-troubleshooting}

När du kontrollerar ett dataflöde kan följande felmeddelande visas: `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Skärmbild för användargränssnittet för plattformen visar ett fel.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Du måste verifiera att *uniqueID* mappningen har konfigurerats. Mer information finns i [Mmpping](#mapping) -avsnitt.

Mer information finns på [[!DNL Pendo] Help Center](https://www.pendo.io/help-center/).