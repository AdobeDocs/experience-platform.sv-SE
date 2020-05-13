---
title: Amazon Kinesis-mål
seo-title: Amazon Kinesis-mål
description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
seo-description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# (Beta) Amazon Kinesis-mål


>[!IMPORTANT]
>
>Målet [!DNL Amazon Kinesis] i Adobe Real-time CDP är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

Med Amazons webbtjänste kan du samla in och bearbeta stora dataströmmar i realtid. [!DNL Kinesis Data Streams]

Du kan skapa en utgående anslutning i realtid till ditt [!DNL Amazon Kinesis] lagringsutrymme för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Amazon Kinesis]finns i [Amazons dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Mer information om hur du ansluter till [!DNL Amazon Kinesis] med API-anrop finns i [självstudiekursen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)om mål för direktuppspelning.
* Om du vill ansluta till [!DNL Amazon Kinesis] med hjälp av Adobe Real-time CDP-användargränssnittet läser du avsnitten nedan.

![Amazon Kinesis i användargränssnittet](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Användningsexempel {#use-cases}

Genom att använda direktuppspelningsmål som Amazon Kinesis kan du enkelt mata in segmenteringshändelser med högt värde och associerade profilattribut i dina valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden hamnar i till Amazon Kinesis-målet får du den här händelsen i Amazon Kinesis. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsdestinationer, inklusive de som stöds av [!DNL Amazon].

Ange följande information i arbetsflödet för att skapa mål för [!DNL Amazon Kinesis] mål:

### I kontosteget {#account-step}

* **Åtkomstnyckel och hemlig nyckel** för Amazon Web Services: Generera [!DNL Amazon Web Services]i stället en åtkomstnyckel - nyckelpar för hemlig åtkomst som ger Adobe CDP-åtkomst i realtid till ditt [!DNL Amazon Kinesis] konto. Läs mer i [Amazons webbtjänstdokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Ange vilken [!DNL Amazon Web Services] region data ska strömmas till.

![Inmatningsfält i kontosteget](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### I autentiseringssteget {#authentication-step}

* **Namn**: Ange ett namn för anslutningen till [!DNL Amazon Kinesis]
* **Beskrivning**: Ange en beskrivning för anslutningen till [!DNL Amazon Kinesis].
* **ström**: Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto. Adobe CDP i realtid exporterar data till den här strömmen.

![Inmatningsfält i autentiseringssteget](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .

## Exporterade data {#exported-data}

Dina exporterade Experience Platform-data får plats [!DNL Amazon Kinesis] i JSON-format. En händelse som innehåller den hashas-e-postidentiteten för en målgrupp som har avslutat ett visst segment kan se ut så här:

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
>* [Anslut till Amazon Kinesis och aktivera data med API-anrop](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Azure Event Hubs-mål](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Måltyper och -kategorier](/help/rtcdp/destinations/destination-types.md)

