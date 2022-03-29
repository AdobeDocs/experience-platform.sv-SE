---
keywords: Azure-händelsehubbsmål;azure-händelsehubb;azure-händelsehubb
title: (Beta) [!DNL Azure Event Hubs] anslutning
description: Skapa en utgående anslutning i realtid till din [!DNL Azure Event Hubs] lagring för att strömma data från Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: b2ac26589527313ec9f3cf84126e3e23da6c7b83
workflow-type: tm+mt
source-wordcount: '1278'
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

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP-adress tillåtelselista {#ip-address-allowlist}

För att uppfylla kundernas säkerhets- och kompatibilitetskrav tillhandahåller Experience Platform en lista över statiska IP-adresser som du kan tillåtslista för [!DNL Azure Event Hubs] mål. Se [IP-adress tillåtelselista för direktuppspelningsmål](/help/destinations/catalog/streaming/ip-address-allow-list.md) för den fullständiga listan över IP-adresser som ska tillåtslista.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL SAS Key Name]**: Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn.
* **[!UICONTROL SAS Key]**: Den primära nyckeln för namnutrymmet för händelsehubbar. The `sasPolicy` som `sasKey` motsvarar måste ha **hantera** rättigheter som konfigurerats för att händelsehubs-listan ska fyllas i. Lär dig mer om autentisering av [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i [!DNL Azure Event Hubs] namnutrymme. Läs mer om [!DNL Azure Event Hubs] namnutrymmen i [Microsoft-dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Name]**: Fyll i ett namn för anslutningen till [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Ange en beskrivning av anslutningen.  Exempel: &quot;Förstklassiga kunder&quot;,&quot;kunder som är intresserade av att skaffa utrustning&quot;.
* **[!UICONTROL eventHubName]**: Ange ett namn för strömmen till din [!DNL Azure Event Hubs] mål.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Beteende vid export av profiler {#profile-export-behavior}

Experience Platform optimerar exportbeteendet för profiler för [!DNL Azure Event Hubs] mål, om du bara vill exportera data till destinationen när relevanta uppdateringar av en profil har gjorts efter segmentkvalificering eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen bestäms av en ändring av segmentmedlemskapet för minst ett av segmenten som är mappat till målet. Profilen har till exempel kvalificerats för ett av de segment som är mappade till målet eller har avslutat ett av de segment som är mappade till målet.
* Profiluppdateringen bestäms av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för ett av de segment som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen bestäms av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om ett segment som är mappat till målflödet till exempel har hundra medlemmar och fem nya profiler är kvalificerade för segmentet, kommer exporten till målet att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

### Vad avgör en dataexport och vad som ingår i exporten {#what-determines-export-what-is-included}

När det gäller data som exporteras för en viss profil är det viktigt att förstå de två olika begreppen i *vad som avgör dataexport till [!DNL Azure Event Hubs] mål* och *vilka data som inkluderas i exporten*.

| Vad avgör en målexport | Vad som ingår i målexporten |
|---------|----------|
| <ul><li>Kopplade attribut och segment fungerar som referens för en målexport. Det innebär att om ett mappat segment ändrar lägen (från null till realiserad eller från realiserad/befintlig till befintlig) eller om mappade attribut uppdateras, kommer en målexport att startas om.</li><li>Eftersom identiteter inte kan mappas till [!DNL Azure Event Hubs] destinationer, ändringar av en identitet i en viss profil avgör också destinationsexporten.</li><li>En ändring för ett attribut definieras som en uppdatering för attributet, oavsett om det är samma värde eller inte. Det innebär att en överskrivning av ett attribut betraktas som en ändring även om värdet i sig inte har ändrats.</li></ul> | <ul><li>Alla segment (med den senaste medlemskapsstatusen), oavsett om de är mappade i dataflödet eller inte, ingår i `segmentMembership` -objekt.</li><li>Alla identiteter i `identityMap` -objektet ingår också (Experience Platform stöder för närvarande inte identitetsmappning i [!DNL Azure Event Hubs] mål).</li><li>Endast mappade attribut inkluderas i målexporten.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Tänk dig till exempel det här dataflödet som en [!DNL Azure Event Hubs] mål där tre segment är markerade i dataflödet och fyra attribut är mappade till målet.

![Amazon Kinesis måldataflöde](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

En profilexport till målet kan bestämmas av en profil som kvalificerar för eller avslutar en av *tre mappade segment*. I dataexporten kan du dock `segmentMembership` objekt (se [Exporterade data](#exported-data) nedan) kan andra omappade segment visas om den aktuella profilen är medlem i dem. Om en profil kvalificerar sig för kunden med DeLorean Cars-segmentet men även är medlem i &quot;Tillbaka till framtiden&quot;-segmentet för film- och science fiction-fans, kommer dessa två andra segment också att finnas i `segmentMembership` dataexportens objekt, även om dessa inte är mappade i dataflödet.

När det gäller profilattribut kommer alla ändringar av de fyra attribut som mappas ovan att avgöra målexporten och alla de fyra mappade attributen som finns i profilen kommer att finnas i dataexporten.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform] data får plats i [!DNL Azure Event Hubs] mål i JSON-format. Exporten nedan innehåller till exempel en profil som har kvalificerats för ett visst segment, är medlem i ett annat segment och har avslutat ett annat segment. Exporten innehåller också profilattributets förnamn, efternamn, födelsedatum och personlig e-postadress. Identiteterna för den här profilen är ECID och e-post.

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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

