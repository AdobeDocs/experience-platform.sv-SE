---
title: Azure Event Hubs-mål
seo-title: Azure Event Hubs-mål
description: Skapa en utgående anslutning i realtid till din Azure Event Hubs-lagring för att strömma data från Experience Platform.
seo-description: Skapa en utgående anslutning i realtid till din Azure Event Hubs-lagring för att strömma data från Experience Platform.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Azure Event Hubs-mål

## Översikt {#overview}

[!DNL Azure Event Hubs] är en stor dataströmningsplattform och en tjänst för händelseredigering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Du kan skapa en utgående anslutning i realtid till ditt [!DNL Azure Event Hubs] lagringsutrymme för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Azure Event Hubs]finns i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Mer information om hur du ansluter till [!DNL Azure Event Hubs] med API-anrop finns i [självstudiekursen]om mål för direktuppspelning.
* Om du vill ansluta till [!DNL Azure Event Hubs] med hjälp av Adobe Real-time CDP-användargränssnittet läser du avsnitten nedan.

![AWS Kinesis i användargränssnittet](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Användningsexempel {#use-cases}

Genom att använda direktuppspelningsmål som Azure Event Hubs kan du enkelt mata in segmenteringshändelser med högt värde och associerade profilattribut i dina valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden hamnar i till Azure Event Hubs-målet får du den här händelsen i Azure Event Hubs. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsdestinationer, inklusive [!DNL Azure Event Hubs].

Ange följande information i arbetsflödet för att skapa mål för [!DNL Azure Event Hubs] mål:

### I kontosteget {#account-step}

* **[!UICONTROL SAS Key Name]** och **[!UICONTROL SAS Key]**: Fyll i SAS-nyckelns namn och nyckel. Läs om hur du autentiserar [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i [!DNL Azure Event Hubs] namnutrymmet. Läs mer om [!DNL Azure Event Hubs] namnutrymmen i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Indata krävs i autentiseringssteget](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### I autentiseringssteget {#authentication-step}

* **[!UICONTROL Name]**: Ange ett namn för anslutningen till [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Ange en beskrivning av anslutningen.  Exempel: &quot;Premium tier customers&quot;, &quot;Males interest of kitsnapfing&quot;.
* **[!UICONTROL eventHubName]**: Ange ett namn för strömmen till ditt [!DNL Azure Event Hubs] mål.

![Data som krävs i konfigurationssteget](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .


## Exporterade data {#exported-data}

Dina exporterade Experience Platform-data får plats [!DNL Azure Event Hubs] i JSON-format. En händelseström som till exempel innehåller den hashas-e-postidentiteten för en målgrupp som har avslutat ett visst segment kan se ut så här:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* Länka till Azure Event Hubs API, genomgång
>* [AWS Kinesis-mål](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Måltyper och -kategorier](/help/rtcdp/destinations/destination-types.md)