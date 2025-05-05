---
title: RainFocus Attendee-profiler
description: Lär dig hur du använder målkopplingen för RainFocus Attendee-profiler för att synkronisera målgruppsprofiler med den globala profilen för RainFocus Attendee.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 3%

---

# RainFocus Attendee-profiler {#rainfocus-destination}

## Översikt {#overview}

Använd målet [!DNL RainFocus Attendee Profiles] för att strömma kundprofiler från Adobe Experience Platform till plattformen [!DNL RainFocus] för att skapa och uppdatera deltagarprofiler.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL RainFocus]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på `clientcare@rainfocus.com` eller går till RainFocus [Help Center](https://help.rainfocus.com/hc/en-us).

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda RainFocus-målet finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Använd skiftläge 1 {#use-case-1}

Ett stort teknikföretag kommer att öppna registreringen för sin kommande globala export och vill överföra kundprofiler till [!DNL RainFocus] för att effektivisera registreringsprocessen.

### Använd skiftläge 2 {#use-case-2}

Ett varumärke som tillhör finanssektorn kommer att vara värd för en rad marknadsföringsprogram som riktar sig till nya och befintliga kunder. De har ett antal målgruppssegment med målkunder i Adobe Experience Platform. Med målkopplingen [!DNL RainFocus] kan de enkelt skicka profilerna till [!DNL RainFocus] för aktivering.

## Förhandskrav {#prerequisites}

Innan du kan använda målet [!DNL RainFocus] måste du kontrollera att följande krav uppfylls:

* Skapa en [!DNL RainFocus] API-profil med OAuth (Global).
   * Slutpunkten för **Attendee Store** måste vara aktiverad.
   * Ett **klient-ID** och **klienthemlighet** måste genereras.

Du måste också ha en RainFocus **händelsekod** som du vill skicka profiler till.

## Identiteter som stöds {#supported-identities}

[!DNL RainFocus] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Ange autentiseringsinformation för RainFocus-målkopplingen](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**: Fyll i [!DNL Client ID] som tillhandahålls av RainFocus API-profil.
* **[!UICONTROL Client secret]**: Fyll i [!DNL Client Secret] som tillhandahålls av RainFocus API-profil.
* **[!UICONTROL Environment]**: Ange vilken RainFocus-miljö du ansluter till, till exempel `dev`, `prod`.
* **[!UICONTROL Org ID]**: Ange den unika `orgid` för din instans av RainFocus.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Ange anslutningsinformation för RainFocus-målkopplingen](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Event ID]**: Din [!DNL RainFocus]-händelsekodsidentifierare som du vill att profiler skickas till.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Följande namnutrymmen för målidentitet måste mappas beroende på användningsfallet:

* **E-post** måste mappas som ett målfält med **Målfält > Välj identitetsnamnområde > e-post**

![Mappa profil- och identitetsfält](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

Vi rekommenderar att du mappar ytterligare profilfält, eftersom det ser till att deltagarprofilen i [!DNL RainFocus] är fullt ifylld. Följande målfält är tillgängliga från [!DNL RainFocus]:

| Målfält | Beskrivning |
|------------|-------------|
| `address1` | Gatuadressens första rad |
| `address2` | Gatuadressens andra linje (om sådan finns) |
| `city` | Ortsnamn |
| `companyname` | Företagets namn |
| `countryid` | En ISO 3166-1 alpha-2-landskodidentifierare för landet |
| `email` | E-postadressen |
| `firstname` | Personens förnamn |
| `lastname` | Personens efternamn |
| `jobtitle` | Personens befattning |
| `phone` | Telefonnumret |
| `state` | FIPS-regionens alfakod för delstat eller provins |
| `zip` | Postnummer eller postnummer |

{style="table-layout:auto"}

## Exporterade data/Validera dataexport {#exported-data}

När en uppsättning profiler har skickats till [!DNL RainFocus] använder du API-profilloggningen i [!DNL RainFocus] för att validera att profilerna har importerats.

![Visa loggar i API-profilen i RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Verifiera att profiler har importerats](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

* [RainFocus Streaming Source Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/analytics/rainfocus)
