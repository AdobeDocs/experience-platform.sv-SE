---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Amazon Kinesis-anslutning
description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: f7f3bc229ddad046dca5ea8d2889942fc9cb2cab
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# (Beta) [!DNL Amazon Kinesis] anslutning

## Översikt {#overview}

>[!IMPORTANT]
>
>The [!DNL Amazon Kinesis] målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

The [!DNL Kinesis Data Streams] service av [!DNL Amazon Web Services] gör det möjligt att samla in och bearbeta stora dataströmmar i realtid.

Du kan skapa en utgående anslutning i realtid till din [!DNL Amazon Kinesis] lagring för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Amazon Kinesis], se [Amazon-dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Ansluta till [!DNL Amazon Kinesis] programmatiskt, se [API-självstudiekurs för direktuppspelningsmål](../../api/streaming-destinations.md).
* Ansluta till [!DNL Amazon Kinesis] med hjälp av användargränssnittet för plattformen, se avsnitten nedan.

![Amazon Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Användningsfall {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Amazon Kinesis]kan du enkelt mata in segmenteringshändelser med högt värde och tillhörande profilattribut i valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden tillhör [!DNL Amazon Kinesis] mål får du den här händelsen i [!DNL Amazon Kinesis]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut på [målaktiveringsarbetsflöde](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Obligatoriskt [!DNL Amazon Kinesis] behörigheter {#required-kinesis-permission}

Ansluta och exportera data till [!DNL Amazon Kinesis] strömmar, Experience Platform behöver behörigheter för följande åtgärder:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Dessa behörigheter är ordnade i [!DNL Kinesis] och kontrolleras av Platform när du har konfigurerat Kinesis-målet i användargränssnittet för plattformen.

I exemplet nedan visas den lägsta åtkomstbehörighet som krävs för att exportera data till en [!DNL Kinesis] mål.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `kinesis:ListStreams` | En åtgärd som listar dataströmmarna i Amazon Kinesis. |
| `kinesis:PutRecord` | En åtgärd som skriver en enskild datapost till en dataström från Kinesis. |
| `kinesis:PutRecords` | En åtgärd som skriver flera dataposter till en dataström från Kinesis i ett enda anrop. |

Mer information om hur du styr åtkomst för [!DNL Kinesis] dataströmmar, läs följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!DNL Amazon Web Services]åtkomstnyckel och hemlig nyckel**: I [!DNL Amazon Web Services], generera ett `access key - secret access key` två för att ge plattformsåtkomst till din [!DNL Amazon Kinesis] konto. Läs mer i [Amazon Web Services-dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Ange vilken [!DNL Amazon Web Services] region som data ska strömmas till.
* **Namn**: Ange ett namn för anslutningen till [!DNL Amazon Kinesis]
* **Beskrivning**: Ange en beskrivning för din anslutning till [!DNL Amazon Kinesis].
* **stream**: Ange namnet på en befintlig dataström i din [!DNL Amazon Kinesis] konto. Plattformen exporterar data till den här strömmen.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Beteende vid export av profiler {#profile-export-behavior}

Experience Platform optimerar beteendet för profilexport till ditt Amazon Kinesis-mål, så att endast data exporteras till ditt mål när relevanta uppdateringar av en profil har gjorts efter att segment kvalificerats eller andra viktiga händelser inträffat. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen utlöstes av en ändring av segmentmedlemskapet för minst ett av segmenten som mappats till målet. Profilen har till exempel kvalificerats för ett av de segment som är mappade till målet eller har avslutat ett av de segment som är mappade till målet.
* Profiluppdateringen utlöstes av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för ett av de segment som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen utlöstes av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om ett segment som är mappat till målflödet till exempel har hundra medlemmar och fem nya profiler är kvalificerade för segmentet, kommer exporten till målet att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform] datakörningar i [!DNL Amazon Kinesis] i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är ECID och e-post.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
>* [Anslut till Amazon Kinesis och aktivera data med API:t för Flow Service](../../api/streaming-destinations.md)
>* [Azure Event Hubs-mål](./azure-event-hubs.md)
>* [Måltyper och -kategorier](../../destination-types.md)

