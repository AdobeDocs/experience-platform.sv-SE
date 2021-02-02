---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Prenumerera på Privacy Service Events
topic: privacy events
description: Lär dig hur du prenumererar på Privacy Service-händelser med en förkonfigurerad webkrok.
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---


# Prenumerera på [!DNL Privacy Service Events]

[!DNL Privacy Service Events] är meddelanden från Adobe Experience Platform  [!DNL Privacy Service]som utnyttjar Adobe I/O Events som skickas till en konfigurerad webkrok för att underlätta automatisering av jobbförfrågningar. De minskar eller eliminerar behovet av att avfråga API:t [!DNL Privacy Service] för att kontrollera om ett jobb är färdigt eller om en viss milstolpe i ett arbetsflöde har nåtts.

Det finns för närvarande fyra typer av meddelanden som rör livscykeln för sekretessjobben:

| Typ | Beskrivning |
| --- | --- |
| Jobbet har slutförts | Alla [!DNL Experience Cloud]-program har rapporterat tillbaka och jobbens övergripande eller globala status har markerats som slutförd. |
| Jobbfel | Ett eller flera program rapporterade ett fel när begäran bearbetades. |
| Produkten är klar | Ett av de program som är associerade med det här jobbet har slutfört sitt arbete. |
| Produktfel | Ett av programmen rapporterade ett fel när begäran bearbetades. |

Det här dokumentet innehåller steg för hur du konfigurerar en händelseregistrering för [!DNL Privacy Service]-meddelanden och hur du tolkar meddelandenyttolaster.

## Komma igång

Läs igenom följande Privacy Service-dokumentation innan du startar den här självstudiekursen:

* [Översikt över Privacy Servicen](./home.md)
* [Utvecklarhandbok för Privacy Service API](./api/getting-started.md)

## Registrera en webkrok på [!DNL Privacy Service Events]

För att kunna ta emot [!DNL Privacy Service Events] måste du använda Adobe Developer Console för att registrera en webkrok för din [!DNL Privacy Service]-integrering.

Följ självstudiekursen om [att prenumerera på [!DNL I/O Event] meddelanden](../observability/notifications/subscribe.md) för detaljerade steg om hur du gör detta. Se till att du väljer **[!UICONTROL Privacy Service Events]** som händelseleverantör för att komma åt händelserna ovan.

## Ta emot [!DNL Privacy Service Event] meddelanden

När du har registrerat webkrok- och sekretessjobben kan du börja få händelsemeddelanden. Du kan visa dessa händelser med hjälp av själva webbkroken eller genom att välja fliken **[!UICONTROL Debug Tracing]** i projektets översikt över händelseregistrering i Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Följande JSON är ett exempel på en [!DNL Privacy Service Event]-meddelandenyttolast som skickas till din webkrok när något av programmen som är kopplat till ett sekretessjobb har slutfört sitt arbete:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Ett unikt systemgenererat ID för meddelandet. |
| `type` | Den typ av meddelande som skickas, vilket ger kontext till informationen som anges i `data`. Möjliga värden är: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | En tidsstämpel som anger när händelsen inträffade. |
| `data.value` | Innehåller ytterligare information om vad som utlöste meddelandet: <ul><li>`jobId`: ID för det sekretessjobb som utlöste meddelandet.</li><li>`message`: Ett meddelande om jobbets specifika status. För `productcomplete`- eller `producterror`-meddelanden anger det här fältet Experience Cloud-programmet i fråga.</li></ul> |

## Nästa steg

I det här dokumentet beskrivs hur du registrerar Privacy Service Events för en konfigurerad webkrok och hur du tolkar meddelandenyttolaster. Mer information om hur du spårar sekretessjobb med användargränssnittet finns i [användarhandboken för Privacy Servicen](./ui/user-guide.md).