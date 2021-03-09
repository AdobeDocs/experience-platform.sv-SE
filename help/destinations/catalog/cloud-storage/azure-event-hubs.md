---
keywords: Azure-händelsehubbsmål;azure-händelsehubb;azure-händelsehubb
title: (Beta) Azure Event Hubs-anslutning
description: Skapa en utgående anslutning i realtid till din Azure Event Hubs-lagring för att strömma data från Experience Platform.
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# (Beta) [!DNL Azure Event Hubs]-anslutning

>[!IMPORTANT]
>
>Målet [!DNL Azure Event Hubs] i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

[!DNL Azure Event Hubs] är en stor dataströmningsplattform och en tjänst för händelseredigering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Du kan skapa en utgående anslutning i realtid till ditt [!DNL Azure Event Hubs]-lagringsutrymme för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Azure Event Hubs] finns i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Om du vill ansluta till [!DNL Azure Event Hubs] programmatiskt läser du självstudiekursen [API för direktuppspelningsmål](../../api/streaming-destinations.md).
* Om du vill ansluta till [!DNL Azure Event Hubs] med användargränssnittet för plattformen läser du avsnitten nedan.

![AWS Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Använd fall {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Azure Event Hubs] kan du enkelt mata in segmenteringshändelser med högt värde och associerade profilattribut i dina valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden hamnar i till målet [!DNL Azure Event Hubs] får du den här händelsen i [!DNL Azure Event Hubs]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

## Anslutningsmål {#connect-destination}

Se [Arbetsflöde för molnlagringsmål ](./workflow.md)för instruktioner om hur du ansluter till molnlagringsmålen, inklusive [!DNL Azure Event Hubs].

För [!DNL Azure Event Hubs]-mål anger du följande information i arbetsflödet för att skapa mål:

### I autentiseringssteget {#authentication-step}

* **[!UICONTROL SAS Key Name]** och  **[!UICONTROL SAS Key]**: Fyll i SAS-nyckelns namn och nyckel. Läs om hur du autentiserar till [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i  [!DNL Azure Event Hubs] namnutrymmet. Läs mer om [!DNL Azure Event Hubs]-namnutrymmen i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Indata krävs i autentiseringssteget](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

### I konfigurationssteget {#setup-step}

* **[!UICONTROL Name]**: Ange ett namn för anslutningen till  [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Ange en beskrivning av anslutningen.  Exempel: &quot;Premium tier customers&quot;, &quot;Males interest of kitsnapfing&quot;.
* **[!UICONTROL eventHubName]**: Ange ett namn för strömmen till ditt  [!DNL Azure Event Hubs] mål.
* **[!UICONTROL Marketing actions]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns på sidan [Datastyrning i Adobe Experience Platform](../../../data-governance/policies/overview.md). Mer information om de enskilda Adobe-definierade marknadsföringsåtgärderna finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

![Data som krävs i konfigurationssteget](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md).

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform]-data anges i [!DNL Azure Event Hubs] i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är ECID och e-post.

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
>* [Anslut till Azure Event Hubs och aktivera data med API:t för Flow Service](../../api/streaming-destinations.md)
>* [AWS Kinesis-mål](./amazon-kinesis.md)
>* [Måltyper och -kategorier](../../destination-types.md)