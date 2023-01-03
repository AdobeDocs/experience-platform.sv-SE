---
keywords: Experience Platform;startsida;populära ämnen;meddelanden om dataöverföring;meddelanden;prenumerationshändelser;statushändelser;statushändelser;abonnemang;statusmeddelanden;
solution: Experience Platform
title: Meddelanden om dataöverföring
topic-legacy: overview
description: För att underlätta övervakningen av intagsprocessen kan Adobe Experience Platform prenumerera på en uppsättning händelser som publiceras i varje steg i processen och meddela dig om status för inmatade data och eventuella fel.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Meddelanden om dataöverföring

Processen att samla in data till Adobe Experience Platform består av flera steg. När du har identifierat datafiler som behöver importeras till [!DNL Platform]Intag påbörjas och varje steg sker i följd tills data antingen har importerats eller misslyckats. Intag kan påbörjas med [Adobe Experience Platform Data Ingtion API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) eller med [!DNL Experience Platform] användargränssnitt.

Data läses in i [!DNL Platform] måste gå igenom flera steg för att nå sin destination, [!DNL Data Lake] eller [!DNL Real-Time Customer Profile] datalager. Varje steg innebär att bearbeta data, validera data och sedan lagra data innan de skickas vidare till nästa steg. Beroende på mängden data som hämtas kan detta bli en tidskrävande process och det finns alltid en risk att processen misslyckas på grund av validerings-, semantik- eller bearbetningsfel. Om ett fel uppstår måste dataproblemen åtgärdas och sedan måste hela importen startas om med de korrigerade datafilerna.

För att underlätta övervakningen av intagsprocessen ska [!DNL Experience Platform] gör det möjligt att prenumerera på en uppsättning händelser som publiceras i varje steg i processen och meddela dig om status för inkapslade data och eventuella fel.

## Registrera en webkrok för meddelanden om dataöverföring

För att kunna ta emot meddelanden om dataöverföring måste du använda [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) för att registrera en webkrok i Experience Platform-integreringen.

Följ självstudiekursen på [prenumerera på [!DNL Adobe I/O Event] meddelanden](../../observability/alerts/subscribe.md) för detaljerade steg om hur du uppnår detta.

>[!IMPORTANT]
>
>Se till att du väljer **[!UICONTROL Platform notifications]** som händelseprovider och välj **[!UICONTROL Data ingestion notification]** Evenemangsprenumeration när du uppmanas till det.

## Ta emot meddelanden om dataöverföring

När du har registrerat din webkrok och nya data har importerats kan du börja få händelsemeddelanden. Du kan visa dessa händelser med webbkroken eller genom att välja **[!UICONTROL Debug Tracing]** i projektanmälningsöversikten i Adobe Developer Console.

Följande JSON är ett exempel på en meddelandenyttolast som skulle skickas till din webkrok om en batchöverföringshändelse misslyckades:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
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
| `event.xdm:eventCode` | En statuskod som anger vilken typ av händelse som utlöstes för datauppsättningen. Se [appendix](#event-codes) för specifika värden och definitioner. |

Om du vill visa det fullständiga schemat för händelsemeddelanden kan du läsa [offentlig GitHub-databas](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Nästa steg

När du har registrerat dig [!DNL Platform] meddelanden till ditt projekt kan du visa mottagna händelser från [!UICONTROL Project overview]. Se guiden på [kalkera Adobe I/O-händelser](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) om du vill ha detaljerade anvisningar om hur du spårar händelser.

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du tolkar nyttolaster för meddelanden om dataintrång.

### Tillgängliga statusmeddelandehändelser {#event-codes}

Följande tabell visar vilka statusmeddelanden för dataöverföring som du kan prenumerera på.

| Händelsekod | Plattformstjänst | Status | Händelsebeskrivning |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | En batch har importerats till en datauppsättning i [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fel | Det gick inte att importera en batch till en datauppsättning i [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | En batch har importerats till [!DNL Profile] datalager. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | fel | Det gick inte att hämta en batch till [!DNL Profile] datalager. |
| `ig_load_success` | [!DNL Identity Service] | success | Data lästes in i identitetsdiagrammet. |
| `ig_load_failure` | [!DNL Identity Service] | fel | Det gick inte att läsa in data i identitetsdiagrammet. |

>[!NOTE]
>
>Det finns bara ett händelseämne för alla meddelanden om dataöverföring. Händelsekoden kan användas för att skilja mellan olika statusvärden.
