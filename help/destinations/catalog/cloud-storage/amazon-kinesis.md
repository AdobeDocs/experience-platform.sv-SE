---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Amazon Kinesis
seo-title: Amazon Kinesis
description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
seo-description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a78dd4b95896387aa1daa022c9e1d5a6cf978448
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# (Beta) [!DNL Amazon Kinesis] mål

>[!IMPORTANT]
>
>Målet [!DNL Amazon Kinesis] i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

Med tjänsten [!DNL Kinesis Data Streams] från [!DNL Amazon Web Services] kan du samla in och bearbeta stora dataströmmar i realtid.

Du kan skapa en utgående anslutning i realtid till ditt [!DNL Amazon Kinesis]-lagringsutrymme för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Amazon Kinesis] finns i [Amazon-dokumentationen](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Om du vill ansluta till [!DNL Amazon Kinesis] med API-anrop kan du läsa självstudiekursen [API för direktuppspelningsmål](../../api/streaming-destinations.md).
* Om du vill ansluta till [!DNL Amazon Kinesis] med användargränssnittet för plattformen läser du avsnitten nedan.

![Amazon Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Använd fall {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Amazon Kinesis] kan du enkelt mata in segmenteringshändelser med högt värde och associerade profilattribut i dina valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden hamnar i till målet [!DNL Amazon Kinesis] får du den här händelsen i [!DNL Amazon Kinesis]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Anslutningsmål {#connect-destination}

Mer information om hur du ansluter till molnlagringsmål, inklusive de som stöds av [!DNL Amazon], finns i [arbetsflödet för molnlagringsmål ](./workflow.md).

För [!DNL Amazon Kinesis]-mål anger du följande information i arbetsflödet för att skapa mål:

### I autentiseringssteget {#authentication-step}

* **[!DNL Amazon Web Services]åtkomstnyckel och hemlig nyckel**: Generera  [!DNL Amazon Web Services]ett  `access key - secret access key` par som ger plattformsåtkomst till ditt  [!DNL Amazon Kinesis] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Ange vilken  [!DNL Amazon Web Services] region data ska strömmas till.

![Inmatningsfält i kontosteget](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### I konfigurationssteget {#setup-step}

* **Namn**: Ange ett namn för anslutningen till  [!DNL Amazon Kinesis]
* **Beskrivning**: Ange en beskrivning för anslutningen till  [!DNL Amazon Kinesis].
* **ström**: Ange namnet på en befintlig dataström i ditt  [!DNL Amazon Kinesis] konto. Plattformen exporterar data till den här strömmen.

![Inmatningsfält i autentiseringssteget](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md).

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform]-data anges i [!DNL Amazon Kinesis] i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är ECID och e-post.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```



>[!MORELIKETHIS]
>
>* [Anslut till Amazon Kinesis och aktivera data med API-anrop](../../api/streaming-destinations.md)
>* [Azure Event Hubs-mål](./azure-event-hubs.md)
>* [Måltyper och -kategorier](../../destination-types.md)

