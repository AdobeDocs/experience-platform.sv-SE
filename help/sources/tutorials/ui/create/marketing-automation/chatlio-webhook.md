---
title: Skapa en Chatlio Source Connection i användargränssnittet
description: Lär dig hur du skapar en Chatlio-källanslutning med Adobe Experience Platform-gränssnittet.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Skapa en [!DNL Chatlio]-källanslutning i användargränssnittet

>[!NOTE]
>
>Källan [!DNL Chatlio] är i betaversion. Läs [källöversikten](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

I den här självstudien beskrivs hur du skapar en [!DNL Chatlio]-källanslutning med Adobe Experience Platform-användargränssnittet.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Förhandskrav {#prerequisites}

Följande avsnitt innehåller information om krav som måste slutföras innan du kan skapa en [!DNL Chatlio]-källanslutning.

### Exempel-JSON för att definiera källschemat för [!DNL Chatlio] {#prerequisites-json-schema}

Innan du skapar en [!DNL Chatlio]-källanslutning måste du ange ett källschema. Du kan använda JSON nedan.

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

### Skapa ett Experience Platform-schema för [!DNL Chatlio] {#create-platform-schema}

Du måste också se till att du skapar ett Experience Platform-schema som du kan använda för källan. I självstudiekursen [Skapa ett Experience Platform-schema](../../../../../xdm/schema/composition.md) finns omfattande anvisningar om hur du skapar ett schema.

![Experience Platform-gränssnittet visar ett exempelschema för Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Anslut ditt [!DNL Chatlio]-konto {#connect-account}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources] och visa en katalog med tillgängliga källor i Experience Platform.

Använd menyn *[!UICONTROL Categories]* för att filtrera källor efter kategori. Du kan också ange ett källnamn i sökfältet för att hitta en viss källa från katalogen.

Gå till kategorin [!UICONTROL Marketing automation] om du vill se källkortet [!DNL Chatlio]. Börja genom att välja **[!UICONTROL Add data]**.

![Experience Platform UI-katalog med Chatlio-kort](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Markera data {#select-data}

**[!UICONTROL Select data]**-steget visas med ett gränssnitt där du kan välja vilka data du vill hämta till Experience Platform.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** om du vill överföra en JSON-fil från det lokala systemet. Du kan också dra och släppa den JSON-fil som du vill överföra till panelen [!UICONTROL Drag and drop files].

![Stegen för att lägga till data i källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda verktyget [!UICONTROL Search field] för att komma åt specifika objekt från schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Dataflödesdetaljer {#dataflow-detail}

**Dataflödesdetaljsteget** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet, samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mappning {#mapping}

Steg [!UICONTROL Mapping] visas, och du får ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Experience Platform ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../../../data-prep/ui/mapping.md).

Mappningarna som anges nedan är obligatoriska och bör konfigureras innan du fortsätter till [!UICONTROL Review]-steget.

| Målfält | Beskrivning |
| --- | --- |
| `UUID` | Identifieraren [!DNL Chatlio] för händelsen. |

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Granska {#review}

Steg **[!UICONTROL Review]** visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilka data som källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Hämta din URL för direktuppspelningsslutpunkt {#get-streaming-endpoint-url}

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten kommer att användas för att prenumerera på din webkrok så att strömningskällan kan kommunicera med Experience Platform.

För att kunna skapa den URL som används för att konfigurera webkroken på [!DNL Chatlio] måste du hämta följande:

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Om du vill hämta **[!UICONTROL Dataflow ID]** och **[!UICONTROL Streaming endpoint]** går du till sidan [!UICONTROL Dataflow activity] i det dataflöde som du just skapade och kopierar informationen längst ned på panelen [!UICONTROL Properties].

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

När du har hämtat ditt ID för direktuppspelningsslutpunkt och dataflöde ska du skapa en URL som baseras på följande mönster: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. En webbkrok-URL kan till exempel se ut så här: ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Konfigurera webkrok i [!DNL Chatlio] {#set-up-webhook}

När din webkroks-URL har skapats kan du nu konfigurera din webkrok med användargränssnittet [!DNL Chatlio].

Logga in på ditt [[!DNL Chatlio]](https://chatlio.com/)-konto och följ [guiden för konfiguration och installation](https://chatlio.com/docs/setup/) för att skapa en widget.

När en widget har skapats navigerar du till inställningssidan för widgeten för att lägga till din webkros-URL i den widgeten.

![Sidan med webkrosinställningar på Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Välj sedan fliken **[!DNL Behavior]** och lägg till din webkrok-URL i fältet *[!DNL Webhook when a new conversation starts]* och andra webkrokikhändelsefält som du vill prenumerera på.

![Chatlio-gränssnittet visar webbkrokens slutpunktsfält.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Du kan prenumerera på olika händelser för din [!DNL Chatlio]-webkrok. Mer information om de olika händelserna finns i [[!DNL Chatlio] händelsedokumentationen](https://chatlio.com/docs/webhooks/).

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du konfigurerat ett dataflöde för direktuppspelning för att överföra dina [!DNL Chatlio]-data till Experience Platform. Om du vill övervaka data som importeras läser du i guiden [Övervaka dataflöden för direktuppspelning med Experience Platform-gränssnittet](../../monitor-streaming.md).

## Ytterligare resurser {#additional-resources}

Avsnitten nedan innehåller ytterligare resurser som du kan referera till när du använder källan [!DNL Chatlio].

### Validering {#validation}

Följ stegen nedan för att verifiera att du har konfigurerat källan och att [!DNL Chatlio] meddelanden importeras korrekt:

* Du kan kontrollera sidan [!DNL Chatlio] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** för att identifiera de händelser som spelas in av [!DNL Chatlio].

![Chatlio UI-skärmbild som visar chatthistorik](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* I Experience Platform-gränssnittet väljer du **[!UICONTROL View Dataflows]** bredvid kortmenyn [!DNL Chatlio] i källkatalogen. Välj sedan **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats för de webbböcker som du har konfigurerat i [!DNL Chatlio].

![Experience Platform-användargränssnitt, skärmbild som visar kapslade händelser](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Mer information om [!DNL Chatlio] finns i [[!DNL Chatlio] dokumentationen](https://chatlio.com/docs/) och [Vanliga frågor ](https://chatlio.com/pricing/#FAQ).
