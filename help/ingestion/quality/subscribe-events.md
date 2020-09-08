---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Prenumerera på dataöverföringshändelser
topic: overview
translation-type: tm+mt
source-git-commit: 80a1694f11cd2f38347989731ab7c56c2c198090
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---


# Meddelanden om dataöverföring

Processen att samla in data till Adobe Experience Platform består av flera steg. När du har identifierat datafiler som behöver importeras [!DNL Platform]till, påbörjas intagsprocessen och varje steg görs i följd tills data antingen har importerats eller misslyckats. Injektionsprocessen kan initieras med [Adobe Experience Platform API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) för datainmatning eller med [!DNL Experience Platform] användargränssnittet.

Data som läses in till [!DNL Platform] måste gå igenom flera steg för att nå målet, [!DNL Data Lake] eller [!DNL Real-time Customer Profile] datalagret. Varje steg innebär att bearbeta data, validera data och sedan lagra data innan de skickas vidare till nästa steg. Beroende på mängden data som hämtas kan detta bli en tidskrävande process och det finns alltid en risk att processen misslyckas på grund av validerings-, semantik- eller bearbetningsfel. Om ett fel uppstår måste dataproblemen åtgärdas och sedan måste hela importen startas om med de korrigerade datafilerna.

För att underlätta övervakningen av intagsprocessen är det möjligt att prenumerera på en uppsättning händelser som publiceras i varje steg i processen och meddela dig om statusen för inmatade data och eventuella fel. [!DNL Experience Platform]

## Registrera en webkrok för meddelanden om dataöverföring

För att kunna ta emot meddelanden om dataintrång måste du använda [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) för att registrera en webkrok för integreringen med Experience Platform.

Följ självstudiekursen om [att prenumerera på [!DNL Adobe I/O Event] meddelanden](../../observability/notifications/subscribe.md) för mer information om hur du gör detta.

>[!IMPORTANT]
>
>Under prenumerationsprocessen kontrollerar du att du väljer **[!UICONTROL Platform notifications]** händelseleverantör och väljer **[!UICONTROL Data ingestion notification]** händelseprenumeration när du uppmanas till det.

## Ta emot meddelanden om dataöverföring

När du har registrerat din webkrok och nya data har importerats kan du börja få händelsemeddelanden. Dessa händelser kan visas med webbhollen eller genom att du väljer **[!UICONTROL Debug Tracing]** fliken i projektregistreringsöversikten i Adobe Developer Console.

Följande JSON är ett exempel på en meddelandenyttolast som skulle skickas till din webkrok om en batchöverföringshändelse misslyckades:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `event_id` | Ett unikt systemgenererat ID för meddelandet. |
| `event` | Ett objekt som innehåller information om händelsen som utlöste meddelandet. |
| `event.xdm:datasetId` | ID:t för den datauppsättning som ingetthändelsen gäller för. |
| `event.xdm:eventCode` | En statuskod som anger vilken typ av händelse som utlöstes för datauppsättningen. Specifika värden och definitioner finns i [bilagan](#event-codes) . |

Se den [offentliga GitHub-databasen](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)för att se det fullständiga schemat för händelsemeddelanden.

## Nästa steg

När du har registrerat [!DNL Platform] meddelanden i projektet kan du visa mottagna händelser från [!UICONTROL Project overview]. Mer information om hur du spårar händelser finns i guiden om [spårning av Adobe I/O-händelser](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) .

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du tolkar nyttolaster för meddelanden om dataintrång.

### Tillgängliga statusmeddelandehändelser {#event-codes}

Följande tabell visar vilka statusmeddelanden för dataöverföring som du kan prenumerera på.

| Händelsekod | Plattformstjänst | Status | Händelsebeskrivning |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | framgång | En batch har importerats till en datauppsättning i [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fel | Det gick inte att importera en batch till en datauppsättning i [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | framgång | En batch har importerats till [!DNL Profile] datalagret. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | fel | Det gick inte att importera en batch till [!DNL Profile] datalagret. |
| `ig_load_success` | [!DNL Identity Service] | framgång | Data lästes in i identitetsdiagrammet. |
| `ig_load_failure` | [!DNL Identity Service] | fel | Det gick inte att läsa in data i identitetsdiagrammet. |

>[!NOTE]
>
>Det finns bara ett händelseämne för alla meddelanden om dataöverföring. Händelsekoden kan användas för att skilja mellan olika statusvärden.