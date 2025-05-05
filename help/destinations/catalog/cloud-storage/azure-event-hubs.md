---
keywords: Azure-händelsehubbsmål;azure-händelsehubb;azure-händelsehubb
title: Azure Event Hubs-anslutning
description: Skapa en utgående anslutning i realtid till ditt [!DNL Azure Event Hubs] lagringsutrymme för att strömma data från Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 0%

---

# [!DNL Azure Event Hubs]-anslutning

## Översikt {#overview}

>[!IMPORTANT]
>
> Det här målet är bara tillgängligt för [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform.html)-kunder.

[!DNL Azure Event Hubs] är en stor dataströmningsplattform och en tjänst för händelseinmatning. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Du kan skapa en utgående anslutning i realtid till ditt [!DNL Azure Event Hubs]-lagringsutrymme för att strömma data från Adobe Experience Platform.

* Mer information om [!DNL Azure Event Hubs] finns i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Om du vill ansluta till [!DNL Azure Event Hubs] programmatiskt läser du [API-självstudiekursen för direktuppspelningsmål](../../api/streaming-destinations.md).
* Om du vill ansluta till [!DNL Azure Event Hubs] med Experience Platform användargränssnitt läser du avsnitten nedan.

![AWS Kinesis i användargränssnittet](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Användningsfall {#use-cases}

Genom att använda direktuppspelningsmål som [!DNL Azure Event Hubs] kan du enkelt mata in segmenteringshändelser med högt värde och associerade profilattribut i dina valfria system.

En potentiell kund har till exempel laddat ned ett vitt papper som kvalificerar dem till ett segment med&quot;hög benägenhet att konvertera&quot;. Genom att mappa målgruppen som den potentiella kunden hamnar i till målet [!DNL Azure Event Hubs] får du den här händelsen i [!DNL Azure Event Hubs]. Där kan ni använda en&quot;do-it-self&quot;-strategi och beskriva affärslogiken utöver evenemanget, som ni tror fungerar bäst med företagets IT-system.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP-adress tillåtelselista {#ip-address-allowlist}

För att uppfylla kundernas säkerhets- och kompatibilitetskrav tillhandahåller Experience Platform en lista över statiska IP-adresser som du kan tillåtslista för målet [!DNL Azure Event Hubs]. Se [IP-adressen tillåtelselista för direktuppspelningsmål](/help/destinations/catalog/streaming/ip-address-allow-list.md) för en fullständig lista över IP-adresser som ska tillåtslista.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). När du ansluter till det här målet måste du ange följande information:

### Autentiseringsinformation {#authentication-information}

#### Standardautentisering {#standard-authentication}

![Bild av gränssnittsskärmen som visar slutförda fält för Azure Event Hubs-standardautentiseringsinformation](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Om du väljer typen **[!UICONTROL Standard authentication]** för att ansluta till HTTP-slutpunkten anger du fälten nedan och väljer **[!UICONTROL Connect to destination]**:

* **[!UICONTROL SAS Key Name]**: Namnet på auktoriseringsregeln, som också kallas för SAS-nyckelnamn.
* **[!UICONTROL SAS Key]**: Den primära nyckeln för händelsehubbarnas namnområde. `sasPolicy` som `sasKey` motsvarar måste ha **manage**-rättigheter konfigurerade för att händelsehubbslistan ska kunna fyllas i. Läs om hur du autentiserar till [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i namnutrymmet [!DNL Azure Event Hubs]. Läs mer om [!DNL Azure Event Hubs] namnutrymmen i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### SAS-autentisering (Shared Access Signature) {#sas-authentication}

![Bild av gränssnittsskärmen som visar slutförda fält för Azure Event Hubs-standardautentiseringsinformation](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Om du väljer typen **[!UICONTROL Standard authentication]** för att ansluta till HTTP-slutpunkten anger du fälten nedan och väljer **[!UICONTROL Connect to destination]**:

* **[!UICONTROL SAS Key Name]**: Namnet på auktoriseringsregeln, som också kallas för SAS-nyckelnamn.
* **[!UICONTROL SAS Key]**: Den primära nyckeln för händelsehubbarnas namnområde. `sasPolicy` som `sasKey` motsvarar måste ha **manage**-rättigheter konfigurerade för att händelsehubbslistan ska kunna fyllas i. Läs om hur du autentiserar till [!DNL Azure Event Hubs] med SAS-nycklar i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Fyll i namnutrymmet [!DNL Azure Event Hubs]. Läs mer om [!DNL Azure Event Hubs] namnutrymmen i [Microsoft-dokumentationen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Event Hub Name]**: Fyll i ditt [!DNL Azure Event Hub]-namn. Läs mer om [!DNL Azure Event Hubs]-namn i [Microsoft-dokumentationen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Inkludera segmentnamn"
>abstract="Växla om du vill att dataexporten ska inkludera namnen på de målgrupper som du exporterar. Visa dokumentationen för ett dataexportexempel där det här alternativet är markerat."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Inkludera tidsstämplar för segment"
>abstract="Växla om du vill att dataexporten ska inkludera UNIX-tidsstämpeln när målgrupperna skapades och uppdaterades, samt UNIX-tidsstämpeln när målgrupperna mappades till målet för aktiveringen. Visa dokumentationen för ett dataexportexempel där det här alternativet är markerat."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Bild av gränssnittsskärmen som visar slutförda fält för Azure Event Hubs-målinformation](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn för anslutningen till [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Ange en beskrivning av anslutningen.  Exempel:&quot;Premium tier customers&quot;,&quot;Customers interest of kitResfing&quot;.
* **[!UICONTROL eventHubName]**: Ange ett namn för dataströmmen till ditt [!DNL Azure Event Hubs]-mål.
* **[!UICONTROL Include Segment Names]**: Växla om du vill att dataexporten ska inkludera namnen på de målgrupper som du exporterar. Ett exempel på en dataexport med det här alternativet markerat finns i avsnittet [Exporterade data](#exported-data) längre fram.
* **[!UICONTROL Include Segment Timestamps]**: Växla om du vill att dataexporten ska inkludera UNIX-tidsstämpeln när målgrupperna skapades och uppdaterades, samt UNIX-tidsstämpeln när målgrupperna mappades till målet för aktiveringen. Ett exempel på en dataexport med det här alternativet markerat finns i avsnittet [Exporterade data](#exported-data) längre fram.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* [Principutvärdering av samtycke](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) stöds för närvarande inte i exporter till Azure Event Hubs-målet. [Läs mer](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Se [Aktivera målgruppsdata för att direktuppspela profilexportmål](../../ui/activate-streaming-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Beteende vid export av profiler {#profile-export-behavior}

Experience Platform optimerar beteendet för profilexport till ditt [!DNL Azure Event Hubs]-mål, så att endast data exporteras till ditt mål när relevanta uppdateringar av en profil har gjorts efter målgruppsklassificering eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen bestäms av en ändring av målgruppsmedlemskap för minst en av målgrupperna som är mappad till målet. Profilen har till exempel kvalificerats för en av de målgrupper som är mappade till målet eller har avslutat en av de målgrupper som är mappade till målet.
* Profiluppdateringen bestäms av en ändring i [identitetskartan](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för en av de målgrupper som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen bestäms av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om en målgrupp som mappats till målflödet till exempel har hundra medlemmar och fem nya profiler kvalificerar sig för segmentet, kommer exporten till målplatsen att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

### Vad avgör en dataexport och vad som ingår i exporten {#what-determines-export-what-is-included}

När det gäller data som exporteras för en viss profil är det viktigt att förstå de två olika begreppen *vad som avgör en dataexport till ditt [!DNL Azure Event Hubs] mål* och *vilka data som inkluderas i exporten*.

| Vad avgör en målexport | Vad som ingår i målexporten |
|---------|----------|
| <ul><li>Kopplade attribut och målgrupper fungerar som referens för en målexport. Det innebär att om någon mappad publik ändrar tillstånd (från `null` till `realized` eller från `realized` till `exiting`) eller om några mappade attribut uppdateras, kommer en målexport att startas.</li><li>Eftersom identiteter för närvarande inte kan mappas till [!DNL Azure Event Hubs] mål, bestämmer ändringar i en viss profil även destinationsexporter.</li><li>En ändring för ett attribut definieras som en uppdatering för attributet, oavsett om det är samma värde eller inte. Det innebär att en överskrivning av ett attribut betraktas som en ändring även om värdet i sig inte har ändrats.</li></ul> | <ul><li>Objektet `segmentMembership` innehåller målgruppen som är mappad i aktiveringsdataflödet, för vilket profilens status har ändrats efter en kvalificerings- eller målgruppsavslutningshändelse. Observera att andra omappade målgrupper för vilka profilen är kvalificerad kan ingå i målexporten, om dessa målgrupper tillhör samma [sammanfogningsprincip](/help/profile/merge-policies/overview.md) som målgruppen som är mappad i aktiveringsdataflödet. </li><li>Alla identiteter i objektet `identityMap` ingår också (Experience Platform stöder för närvarande inte identitetsmappning i målet [!DNL Azure Event Hubs]).</li><li>Endast de mappade attributen inkluderas i målexporten.</li></ul> |

{style="table-layout:fixed"}

Ta till exempel det här dataflödet som ett [!DNL Azure Event Hubs]-mål där tre målgrupper har valts i dataflödet och fyra attribut har mappats till målet.

![Amazon Kinesis-måldataflöde](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

En profilexport till målet kan bestämmas av en profil som kvalificerar för eller avslutar ett av de *tre mappade segmenten*. I dataexporten, i objektet `segmentMembership` (se avsnittet [ Exporterade data ](#exported-data) nedan), kan andra omappade målgrupper visas om den aktuella profilen är medlem av dem och om dessa delar samma sammanfogningsprincip som målgruppen som utlöste exporten. Om en profil kvalificerar sig för **kunden med DeLorean Cars**-målgruppen men även är medlem i segmenten **Bevakade&quot;Tillbaka till framtiden&quot;** och **Science fiction fans** kommer dessa två målgrupper också att finnas i `segmentMembership`-objektet för dataexporten, även om de inte mappas i dataflödet, om de har samma sammanslagning policy med segmentet **Customer with DeLorean Cars** .

När det gäller profilattribut kommer alla ändringar av de fyra attribut som mappas ovan att avgöra målexporten och alla de fyra mappade attributen som finns i profilen kommer att finnas i dataexporten.

## Bakgrundsfyllning av historiska data {#historical-data-backfill}

När du lägger till en ny målgrupp till ett befintligt mål, eller när du skapar ett nytt mål och mappar målgrupper till det, exporterar Experience Platform data om målgruppens historiska kvalifikationer till målet. Profiler som är kvalificerade för målgruppen *innan* målgruppen lades till i målet exporteras till målet inom ungefär en timme.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform]-data får plats i ditt [!DNL Azure Event Hubs]-mål i JSON-format. Exporten nedan innehåller till exempel en profil som har kvalificerats för ett visst segment, är medlem i ett annat segment och har avslutat ett annat segment. Exporten innehåller också profilattributets förnamn, efternamn, födelsedatum och personlig e-postadress. Identiteterna för den här profilen är ECID och e-post.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Nedan visas ytterligare exempel på exporterade data, beroende på vilka UI-inställningar du har valt i anslutningsmålflödet för alternativen **[!UICONTROL Include Segment Names]** och **[!UICONTROL Include Segment Timestamps]**:

+++ Exemplet på dataexport nedan innehåller publiknamn i avsnittet `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ Exemplet på dataexport nedan innehåller målgruppstidsstämplar i avsnittet `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

På 95 % av tiden försöker Experience Platform erbjuda en genomströmningslatens på mindre än 10 minuter för meddelanden som skickats utan fel med en hastighet på mindre än 10 000 begäranden per sekund för varje dataflöde till en HTTP-destination.

Om det uppstår misslyckade begäranden till HTTP API-målet, lagrar Experience Platform de misslyckade förfrågningarna och försöker skicka dem till slutpunkten två gånger.

>[!MORELIKETHIS]
>
>* [Anslut till Azure Event Hubs och aktivera data med API:t för Flow Service ](../../api/streaming-destinations.md)
>* [AWS Kinesis-mål](./amazon-kinesis.md)
>* [Måltyper och -kategorier](../../destination-types.md)
