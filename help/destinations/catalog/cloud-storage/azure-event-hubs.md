---
keywords: Azure-händelsehubbsmål;azure-händelsehubb;azure-händelsehubb
title: (Beta) !DNL Azure Event Hubs] anslutning
description: Skapa en utgående anslutning i realtid till ditt !DNL Azure Event Hubs]-lagringsutrymme för att strömma data från Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# (Beta) [!DNL Azure Event Hubs] anslutning

## Översikt {#overview}

>[!IMPORTANT]
>
>The [!DNL Azure Event Hubs] målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

[!DNL Azure Event Hubs] är en stor dataströmningsplattform och en tjänst för händelseredigering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Du kan skapa en utgående anslutning i realtid till din [!DNL Azure Event Hubs] lagring för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Azure Event Hubs], se [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Ansluta till [!DNL Azure Event Hubs] programmatiskt, se [API-självstudiekurs för direktuppspelningsmål](../../api/streaming-destinations.md).
* Ansluta till [!DNL Azure Event Hubs] med hjälp av användargränssnittet för plattformen, se avsnitten nedan.

![AWS Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Användningsexempel {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Azure Event Hubs]kan du enkelt mata in segmenteringshändelser med högt värde och tillhörande profilattribut i valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden tillhör [!DNL Azure Event Hubs] mål får du den här händelsen i [!DNL Azure Event Hubs]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut på [målaktiveringsarbetsflöde](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL SAS Key Name]** och **[!UICONTROL SAS Key]**: Fyll i SAS-nyckelns namn och nyckel. Lär dig mer om autentisering av [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i [!DNL Azure Event Hubs] namnutrymme. Läs mer om [!DNL Azure Event Hubs] namnutrymmen i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Name]**: Fyll i ett namn för anslutningen till [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Ange en beskrivning av anslutningen.  Exempel: &quot;Premium tier customers&quot;, &quot;Males interest of kitsnapfing&quot;.
* **[!UICONTROL eventHubName]**: Ange ett namn för strömmen till din [!DNL Azure Event Hubs] mål.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform] datakörningar i [!DNL Azure Event Hubs] i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är ECID och e-post.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
>* [Anslut till Azure Event Hubs och aktivera data med API:t för Flow Service](../../api/streaming-destinations.md)
>* [AWS Kinesis](./amazon-kinesis.md)
>* [Måltyper och -kategorier](../../destination-types.md)

