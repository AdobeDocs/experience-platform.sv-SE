---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Amazon Kinesis-anslutning
description: Skapa en utgående anslutning i realtid till din Amazon Kinesis-lagring för att strömma data från Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] anslutning

## Översikt {#overview}

>[!IMPORTANT]
>
> Det här målet är bara tillgängligt för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder.

The [!DNL Kinesis Data Streams] service av [!DNL Amazon Web Services] gör det möjligt att samla in och bearbeta stora dataströmmar i realtid.

Du kan skapa en utgående anslutning i realtid till din [!DNL Amazon Kinesis] lagring för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Amazon Kinesis], se [Amazon-dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Ansluta till [!DNL Amazon Kinesis] programmatiskt, se [API-självstudiekurs för direktuppspelningsmål](../../api/streaming-destinations.md).
* Ansluta till [!DNL Amazon Kinesis] med hjälp av användargränssnittet för plattformen, se avsnitten nedan.

![Amazon Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Användningsfall {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Amazon Kinesis]kan du enkelt mata in segmenteringshändelser med högt värde och tillhörande profilattribut i valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa segmentet som den potentiella kunden tillhör [!DNL Amazon Kinesis] mål får du den här händelsen i [!DNL Amazon Kinesis]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP-adress tillåtelselista {#ip-address-allowlist}

För att uppfylla kundernas säkerhets- och kompatibilitetskrav tillhandahåller Experience Platform en lista över statiska IP-adresser som du kan tillåtslista för [!DNL Amazon Kinesis] mål. Se [IP-adress tillåtelselista för direktuppspelningsmål](/help/destinations/catalog/streaming/ip-address-allow-list.md) för den fullständiga listan över IP-adresser som ska tillåtslista.

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

{style=&quot;table-layout:auto&quot;}

Mer information om hur du styr åtkomst för [!DNL Kinesis] dataströmmar, läs följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). När du ansluter till det här målet måste du ange följande information:

### Autentiseringsinformation {#authentication-information}

Ange fälten nedan och välj **[!UICONTROL Connect to destination]**:

![Bild av gränssnittsskärmen som visar slutförda fält för Amazon Kinesis-autentiseringsinformation](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]åtkomstnyckel och hemlig nyckel**: I [!DNL Amazon Web Services], generera ett `access key - secret access key` två för att ge plattformsåtkomst till din [!DNL Amazon Kinesis] konto. Läs mer i [Amazon Web Services-dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Region]**: Ange vilken [!DNL Amazon Web Services] region som data ska strömmas till.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Inkludera segmentnamn"
>abstract="Växla om du vill att dataexporten ska inkludera namnen på de segment som du exporterar. Visa dokumentationen för ett dataexportexempel där det här alternativet är markerat."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Inkludera tidsstämplar för segment"
>abstract="Växla om du vill att dataexporten ska inkludera UNIX-tidsstämpeln när segmenten skapades och uppdaterades, samt UNIX-tidsstämpeln när segmenten mappades till målet för aktiveringen. Visa dokumentationen för ett dataexportexempel där det här alternativet är markerat."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Bild av gränssnittsskärmen med ifyllda fält för Amazon Kinesis-målinformationen](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn för anslutningen till [!DNL Amazon Kinesis]
* **[!UICONTROL Description]**: Ange en beskrivning för din anslutning till [!DNL Amazon Kinesis].
* **[!UICONTROL Stream]**: Ange namnet på en befintlig dataström i din [!DNL Amazon Kinesis] konto. Plattformen exporterar data till den här strömmen.
* **[!UICONTROL Include Segment Names]**: Växla om du vill att dataexporten ska inkludera namnen på de segment som du exporterar. Ett exempel på en dataexport med det här alternativet markerat finns i [Exporterade data](#exported-data) vidare nedan.
* **[!UICONTROL Include Segment Timestamps]**: Växla om du vill att dataexporten ska inkludera UNIX-tidsstämpeln när segmenten skapades och uppdaterades, samt UNIX-tidsstämpeln när segmenten mappades till målet för aktiveringen. Ett exempel på en dataexport med det här alternativet markerat finns i [Exporterade data](#exported-data) vidare nedan.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Beteende vid export av profiler {#profile-export-behavior}

Experience Platform optimerar exportbeteendet för profiler för [!DNL Amazon Kinesis] mål, om du bara vill exportera data till destinationen när relevanta uppdateringar av en profil har gjorts efter segmentkvalificering eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen bestäms av en ändring av segmentmedlemskapet för minst ett av segmenten som är mappat till målet. Profilen har till exempel kvalificerats för ett av de segment som är mappade till målet eller har avslutat ett av de segment som är mappade till målet.
* Profiluppdateringen bestäms av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för ett av de segment som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen bestäms av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om ett segment som är mappat till målflödet till exempel har hundra medlemmar och fem nya profiler är kvalificerade för segmentet, kommer exporten till målet att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

### Vad avgör en dataexport och vad som ingår i exporten {#what-determines-export-what-is-included}

När det gäller data som exporteras för en viss profil är det viktigt att förstå de två olika begreppen i *vad som avgör dataexport till [!DNL Amazon Kinesis] mål* och *vilka data som inkluderas i exporten*.

| Vad avgör en målexport | Vad som ingår i målexporten |
|---------|----------|
| <ul><li>Kopplade attribut och segment fungerar som referens för en målexport. Det innebär att om ett mappat segment ändrar lägen (från null till realiserad eller från realiserad/befintlig till befintlig) eller om mappade attribut uppdateras, kommer en målexport att startas om.</li><li>Eftersom identiteter inte kan mappas till [!DNL Amazon Kinesis] destinationer, ändringar av en identitet i en viss profil avgör också destinationsexporten.</li><li>En ändring för ett attribut definieras som en uppdatering för attributet, oavsett om det är samma värde eller inte. Det innebär att en överskrivning av ett attribut betraktas som en ändring även om värdet i sig inte har ändrats.</li></ul> | <ul><li>Alla segment (med den senaste medlemskapsstatusen), oavsett om de är mappade i dataflödet eller inte, ingår i `segmentMembership` -objekt.</li><li>Alla identiteter i `identityMap` -objektet ingår också (Experience Platform stöder för närvarande inte identitetsmappning i [!DNL Amazon Kinesis] mål).</li><li>Endast mappade attribut inkluderas i målexporten.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Tänk dig till exempel det här dataflödet som en [!DNL Amazon Kinesis] mål där tre segment är markerade i dataflödet och fyra attribut är mappade till målet.

![Amazon Kinesis måldataflöde](../../assets/catalog/http/profile-export-example-dataflow.png)

En profilexport till målet kan bestämmas av en profil som kvalificerar för eller avslutar en av *tre mappade segment*. I dataexporten kan du dock `segmentMembership` objekt (se [Exporterade data](#exported-data) nedan) kan andra omappade segment visas om den aktuella profilen är medlem i dem. Om en profil kvalificerar sig för kunden med DeLorean Cars-segmentet men även är medlem i &quot;Tillbaka till framtiden&quot;-segmentet för film- och science fiction-fans, kommer dessa två andra segment också att finnas i `segmentMembership` dataexportens objekt, även om dessa inte är mappade i dataflödet.

När det gäller profilattribut kommer alla ändringar av de fyra attribut som mappas ovan att avgöra målexporten och alla de fyra mappade attributen som finns i profilen kommer att finnas i dataexporten.

## Bakgrundsfyllning av historiska data {#historical-data-backfill}

När du lägger till ett nytt segment till ett befintligt mål, eller när du skapar ett nytt mål och mappningssegment till det, exporterar Experience Platform data för historiska segmentkvalificeringar till målet. Profiler som är kvalificerade för segmentet *före* segmentet lades till i målet och exporteras till målet inom ungefär en timme.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform] data får plats i [!DNL Amazon Kinesis] mål i JSON-format. Exporten nedan innehåller till exempel en profil som har kvalificerats för ett visst segment, är medlem i ett annat segment och har avslutat ett annat segment. Exporten innehåller också profilattributets förnamn, efternamn, födelsedatum och personlig e-postadress. Identiteterna för den här profilen är ECID och e-post.

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

Nedan visas ytterligare exempel på exporterade data, beroende på vilka användargränssnittsinställningar du har valt i anslutningsmålflödet för **[!UICONTROL Include Segment Names]** och **[!UICONTROL Include Segment Timestamps]** alternativ:

+++ Exemplet på dataexport nedan innehåller segmentnamn i `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ Exemplet på dataexport nedan innehåller segmenttidsstämplar i `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Begränsningar och återförsöksprincip {#limits-retry-policy}

På 95 % av tiden försöker Experience Platform att erbjuda en genomströmningslatens på mindre än 10 minuter för meddelanden som skickats utan fel med en hastighet på mindre än 10 000 begäranden per sekund för varje dataflöde till en HTTP-destination.

Om det uppstår misslyckade begäranden till HTTP API-målet, lagrar Experience Platform de misslyckade förfrågningarna och försöker skicka dem till slutpunkten två gånger.

>[!MORELIKETHIS]
>
>* [Anslut till Amazon Kinesis och aktivera data med API:t för Flow Service](../../api/streaming-destinations.md)
>* [Azure Event Hubs-mål](./azure-event-hubs.md)
>* [Måltyper och -kategorier](../../destination-types.md)

