---
title: Självbetjäningsmall // Ersätt med namnet på destinationen
description: Använd den här mallen för att skapa offentlig dokumentation för destinationen i Adobe Experience Platform-katalogen. // Ersätt med stycket i avsnittet Översikt
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Din målanslutning {#your-destination}

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från den här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Please ignore all instances of UICONTROL on this page. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat den.*

>[!IMPORTANT]
>
>* Fyll i alla avsnitt i den här mallen i den ordning som de beskrivs i mallen.
>* Den här mallen uppdateras sällan baserat på feedback från partner. Innan du börjar skapa dokumentation för ditt mål måste du kontrollera att du har hämtat den [senaste versionen av mallen](../assets/docs-framework/yourdestination-template.zip).

## Översikt {#overview}

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Inkludera en länk till din produktdokumentationsstartsida för ytterligare läsning.*

>[!IMPORTANT]
>
>Den här målanslutnings- och dokumentationssidan skapas och underhålls av *YourDestination* -teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk eller e-postadress där du kan komma åt uppdateringar, till exempel `support@YourDestination.com`.*

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda *YourDestination* -målet finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1 {#use-case-1}

*För plattformar för mobilmeddelanden:*

*En uthyrnings- och försäljningsplattform vill skicka mobilmeddelanden till kundernas Android- och iOS-enheter för att tala om för dem att det finns 100 uppdaterade listor i det område där de tidigare sökte efter en uthyrning.*

### Använd skiftläge 2 {#use-case-2}

*För plattformar för sociala nätverk:*

*Ett atletiskt klädmärke vill nå befintliga kunder via sina konton för sociala medier. Det klädvarumärket kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till YourDestination för att visa annonser i sina kunders sociala medieflöden.*

## Förhandskrav {#prerequisites}

*Lägg till information i det här avsnittet om allt som kunderna behöver känna till innan de börjar konfigurera målet i Adobe Experience Platform användargränssnitt. Det här kan vara om:*

* *måste läggas till i en tillåtelselista*
* *krav för e-posthashning*
* *kontoinformation på din sida*
* *Så här hämtar du en API-nyckel för att ansluta till din plattform*

*Du kan länka ut till relevant dokumentation om det skulle vara användbart för kunderna.*

## Identiteter som stöds {#supported-identities}

*Lägg till information i det här avsnittet om de identiteter som stöds av ditt mål. Vi har förfyllt tabellen med några standardvärden. Ta bort de värden som inte gäller för ditt mål och/eller lägg till värden som inte är förifyllda.*

*Din destination* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Läs följande dokument på [ECID](/help/identity-service/features/ecid.md) om du vill ha mer information. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

*Lägg till information i det här avsnittet om de målgrupper som stöds av ditt mål. Vi har förfyllt tabellen med några standardvärden. Använd tecknen `✓` och `X` för att ange om målgruppstypen stöds av det här målet.*

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

*Behåll endast de rader som motsvarar ditt mål i tabellen. Du bör ha en rad för typen Exportera och en rad för Exportfrekvens. Ta bort de värden som inte gäller för ditt mål.*

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i målet *YourDestination*. |
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporttyp | **[!UICONTROL Dataset export]** | Du exporterar rådatamängder som inte är grupperade eller strukturerade efter målgruppsintressen eller kvalifikationer. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

*Lägg till de fält som kunderna måste fylla i när de autentiserar till ditt mål. Dessa fält är målspecifika och beror på din konfiguration i Destination SDK. Målets fält kanske inte är samma som de som anges nedan. Ta även med en skärmbild som liknar den exempelbild som visas nedan.*

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Exempelbild som visar hur du autentiserar till målet](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Bearer token]**: Fyll i bearer-token för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

*Lägg till de fält som kunderna måste fylla i när de konfigurerar ett nytt mål. Dessa fält är målspecifika och beror på din konfiguration i Destination SDK. Målets fält kanske inte är samma som de som anges nedan. Ta även med en skärmbild som liknar den exempelbild som visas nedan.*

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Exempelbild som visar hur du fyller i information för ditt mål](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Ditt *YourDestination*-konto-ID.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

*Ta bort det som är lämpligt - Om du dokumenterar ett nytt direktuppspelningsmål ska du behålla det första stycket nedan. Om du dokumenterar ett nytt filbaserat mål ska du behålla det andra stycket. Om du dokumenterar ett mål som exporterar datauppsättningar ska du behålla det tredje stycket.*

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

Läs [(Beta) Exportera datauppsättningar](/help/destinations/ui/export-datasets.md) om du vill ha omfattande instruktioner om hur du exporterar datauppsättningar till det här målet.

### Mappa attribut och identiteter {#map}

*Lägg till information om mappningar som stöds mellan käll- och målfält i mappningssteget i aktiveringsarbetsflödet. Målet kan ha stöd för export av profilattribut, identitetsnamnutrymmen eller båda. Vissa fält kan vara obligatoriska. Målattribut kan vara fördefinierade eller anpassade. Utmana viktiga kavattar och använd exempel, helst med skärmbilder. Två exempel på målsidor som du kan använda som referens är:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Media](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Exporterade data/Validera dataexport {#exported-data}

*Lägg till ett stycke om hur data exporteras till ditt mål. Detta hjälper kunden att se till att de är korrekt integrerade med er destination. Du kan t.ex. ange ett exempel på JSON som den nedan. Eller så kan du tillhandahålla skärmbilder och information från målgränssnittet som visar hur kunderna förväntar sig att målgrupperna ska fylla i på målplattformen.*

```
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
        "status": "realized"
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

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

*Du kan tillhandahålla ytterligare länkar till din produktdokumentation eller andra resurser som du anser vara viktiga för att kunden ska lyckas.*
