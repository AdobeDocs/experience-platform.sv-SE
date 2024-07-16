---
keywords: Experience Platform;startsida;populära ämnen;meddelanden om dataöverföring;meddelanden;prenumerationshändelser;statushändelser;statushändelser;abonnemang;statusmeddelanden;
solution: Experience Platform
title: Meddelanden om dataöverföring
description: För att underlätta övervakningen av intagsprocessen kan Adobe Experience Platform prenumerera på en uppsättning händelser som publiceras i varje steg i processen och meddela dig om status för inmatade data och eventuella fel.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Meddelanden om dataöverföring

Processen att samla in data i Adobe Experience Platform består av flera steg. När du har identifierat datafiler som behöver importeras till [!DNL Platform], börjar importen och varje steg sker i följd tills data antingen har importerats eller misslyckats. Inledningsprocessen kan initieras med [Adobe Experience Platform API för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) eller med användargränssnittet [!DNL Experience Platform].

Data som läses in till [!DNL Platform] måste gå igenom flera steg för att nå sitt mål, [!DNL Data Lake] eller datalagret [!DNL Real-Time Customer Profile]. Varje steg innebär att bearbeta data, validera data och sedan lagra data innan de skickas vidare till nästa steg. Beroende på mängden data som hämtas kan detta bli en tidskrävande process och det finns alltid en risk att processen misslyckas på grund av validerings-, semantik- eller bearbetningsfel. Om ett fel uppstår måste dataproblemen åtgärdas och sedan måste hela importen startas om med de korrigerade datafilerna.

För att underlätta övervakningen av inmatningsprocessen kan [!DNL Experience Platform] prenumerera på en uppsättning händelser som publiceras av varje steg i processen och meddela dig om status för inmatade data och eventuella fel.

## Registrera en webkrok för meddelanden om dataöverföring

För att kunna ta emot meddelanden om dataintrång måste du använda [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) för att registrera en webkrok för Experience Platform-integreringen.

Följ självstudiekursen om att [prenumerera på [!DNL Adobe I/O Event] meddelanden](../../observability/alerts/subscribe.md) för mer information om hur du slutför det här.

>[!IMPORTANT]
>
>Under prenumerationsprocessen kontrollerar du att du har valt **[!UICONTROL Platform notifications]** som händelseleverantör och väljer händelseprenumerationen **[!UICONTROL Data ingestion notification]** när du uppmanas till det.

## Ta emot meddelanden om dataöverföring

När du har registrerat din webkrok och nya data har importerats kan du börja få händelsemeddelanden. Dessa händelser kan visas med hjälp av själva webbhoten eller genom att välja fliken **[!UICONTROL Debug Tracing]** i projektets översikt över händelseregistrering i Adobe Developer Console.

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
| `event_id` | Ett unikt, systemgenererat ID för meddelandet. |
| `event` | Ett objekt som innehåller information om händelsen som utlöste meddelandet. |
| `event.xdm:datasetId` | ID:t för den datauppsättning som ingressen gäller för. |
| `event.xdm:eventCode` | En statuskod som anger vilken typ av händelse som utlöstes för datauppsättningen. Se [bilagan](#event-codes) för specifika värden och definitioner. |

Om du vill visa det fullständiga schemat för händelsemeddelanden kan du läsa [GitHub-databasen](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Nästa steg

När du har registrerat [!DNL Platform] meddelanden till ditt projekt kan du visa mottagna händelser från [!UICONTROL Project overview]. Mer information om hur du spårar händelser finns i guiden om [spårning av Adobe I/O-händelser](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md).

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du tolkar nyttolaster för meddelanden om dataintrång.

### Tillgängliga statusmeddelandehändelser {#event-codes}

Följande tabell visar vilka statusmeddelanden för dataöverföring som du kan prenumerera på.

| Händelsekod | Plattformstjänst | Status | Händelsebeskrivning |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | framgång | En batch har importerats till en datauppsättning i [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fel | Det gick inte att kapsla en batch i en datauppsättning i [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | framgång | En batch har importerats till datalagret [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | fel | Det gick inte att importera en batch till datalagret [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | framgång | Data lästes in i identitetsdiagrammet. |
| `ig_load_failure` | [!DNL Identity Service] | fel | Det gick inte att läsa in data i identitetsdiagrammet. |

>[!NOTE]
>
>Det finns bara ett händelseämne för alla meddelanden om dataöverföring. Händelsekoden kan användas för att skilja mellan olika statusvärden.
