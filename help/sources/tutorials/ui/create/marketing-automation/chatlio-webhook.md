---
title: Skapa en Chatlio-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Chatlio-källanslutning med Adobe Experience Platform-gränssnittet.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Skapa en [!DNL Chatlio] källanslutning i användargränssnittet

>[!NOTE]
>
>The [!DNL Chatlio] källan är i betaversion. Läs [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Chatlio] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Förutsättningar {#prerequisites}

Följande avsnitt innehåller information om krav som måste utföras innan du kan skapa en [!DNL Chatlio] källanslutning.

### Exempel-JSON för att definiera källschemat för [!DNL Chatlio] {#prerequisites-json-schema}

Innan du skapar [!DNL Chatlio] källanslutning, du måste ange ett källschema. Du kan använda JSON nedan.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Skapa ett plattformsschema för [!DNL Chatlio] {#create-platform-schema}

Du måste också se till att du skapar ett plattformsschema som kan användas för källan. Läs självstudiekursen om [skapa ett plattformsschema](../../../../../xdm/schema/composition.md) om du vill ha omfattande anvisningar om hur du skapar ett schema.

![Plattformsgränssnittet visar ett exempelschema för Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Koppla samman [!DNL Chatlio] konto {#connect-account}

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] och se en katalog med källor i Experience Platform.

Använd *[!UICONTROL Categories]* meny för att filtrera källor efter kategori. Du kan också ange ett källnamn i sökfältet för att hitta en viss källa från katalogen.

Gå till [!UICONTROL Marketing automation] för att se [!DNL Chatlio] källkort. Börja genom att välja **[!UICONTROL Add data]**.

![Plattformens gränssnittskatalog med Chatlio-kortet](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Markera data {#select-data}

The **[!UICONTROL Select data]** visas, där du får ett gränssnitt där du kan välja vilka data du vill hämta till plattformen.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** för att överföra en JSON-fil från ditt lokala system. Du kan också dra och släppa den JSON-fil som du vill överföra till [!UICONTROL Drag and drop files] -panelen.

![Steget Lägg till data i källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda [!UICONTROL Search field] för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Dataflödesdetaljer {#dataflow-detail}

The **Dataflödesdetaljer** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mappning {#mapping}

The [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

Mappningarna som anges nedan är obligatoriska och bör konfigureras innan du fortsätter till [!UICONTROL Review] stage.

| Målfält | Beskrivning |
| --- | --- |
| `UUID` | The [!DNL Chatlio] identifierare för händelsen. |

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Granska {#review}

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen till den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** så att dataflödet kan skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Hämta din URL för direktuppspelningsslutpunkt {#get-streaming-endpoint-url}

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform.

För att kunna skapa den URL som används för att konfigurera webbhoten på [!DNL Chatlio] du måste hämta följande:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Så här hämtar du **[!UICONTROL Dataflow ID]** och **[!UICONTROL Streaming endpoint]**, går till [!UICONTROL Dataflow activity] sidan med dataflödet som du just skapade och kopierar informationen från nederkanten av [!UICONTROL Properties] -panelen.

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

När du har hämtat ditt slutpunkts- och dataflödes-ID för direktuppspelning skapar du en URL baserat på följande mönster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. En webbkrok-URL kan till exempel se ut så här: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Konfigurera webkrok i [!DNL Chatlio] {#set-up-webhook}

När webkrok-URL:en har skapats kan du nu konfigurera din webkrok med [!DNL Chatlio] användargränssnitt.

Logga in på [[!DNL Chatlio]](https://chatlio.com/) konto och följ [guiden för installation](https://chatlio.com/docs/setup/) för att skapa en widget.

När en widget har skapats navigerar du till inställningssidan för widgeten för att lägga till din webkros-URL i den widgeten.

![Webbkrokinställningssidan på Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Nästa steg är att välja **[!DNL Behavior]** och lägga till din webkrok-URL i *[!DNL Webhook when a new conversation starts]* fält och andra webbhothändelsefält som du vill prenumerera på.

![Chatlio-gränssnittet visar webbkrokens slutpunktsfält.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Du kan prenumerera på olika evenemang för [!DNL Chatlio] webbkrok. Mer information om de olika händelserna finns i [[!DNL Chatlio] dokumentation för händelser](https://chatlio.com/docs/webhooks/).

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du konfigurerat ett dataflöde för direktuppspelning för att [!DNL Chatlio] data till Experience Platform. Om du vill övervaka de data som importeras läser du i guiden på [övervaka strömmande dataflöden med hjälp av plattformsgränssnitt](../../monitor-streaming.md).

## Ytterligare resurser {#additional-resources}

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL Chatlio] källa.

### Validering {#validation}

För att verifiera att du har konfigurerat källan och [!DNL Chatlio] meddelanden importeras, följ stegen nedan:

* Du kan kontrollera [!DNL Chatlio] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** för att identifiera de händelser som spelas in av [!DNL Chatlio].

![Chatlio UI, skärmbild som visar chatthistorik](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Välj **[!UICONTROL View Dataflows]** bredvid [!DNL Chatlio] kortmenyn i källkatalogen. Nästa, välj **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats för de webbböcker som du har konfigurerat i [!DNL Chatlio].

![Skärmbild av användargränssnittet för plattformen med inkapslade händelser](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Ytterligare information om [!DNL Chatlio], går till [[!DNL Chatlio] dokumentation](https://chatlio.com/docs/) och [Vanliga frågor](https://chatlio.com/pricing/#FAQ).
