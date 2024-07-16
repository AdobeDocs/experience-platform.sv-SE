---
title: Medieanslutning
description: Aktivera profiler för riktade medieundersökningar och insamling av feedback för att bättre förstå kundernas behov och förväntningar.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# Medieanslutning

## Översikt {#overview}

Aktivera profiler för riktade medieundersökningar och insamling av feedback för att bättre förstå kundernas behov och förväntningar.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Medallia-teamet. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på adobe-integrations@medallia.com.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda mediedestinationen finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Använd skiftläge 1

Ett B2B-varumärke vill utvärdera och effektivisera sitt introduktionsprogram. De vill skicka personaliserade enkäter i realtid till kunder som just slutfört introduktionsprocessen.

### Använd skiftläge 2

En återförsäljare vill förstå kundernas preferenser bättre för orderhantering. De vill skicka en kort enfråge-SMS-enkät till kunder som har gjort online- och butiksköp den senaste månaden.

## Förhandskrav {#prerequisites}

Följande information krävs för att upprätta en parallellanslutning:
* **URL för OAuth-tokenslutpunkt**
* **Klient-ID**
* **Klienthemlighet**
* **API Gateway-URL**
* **Importera API-namn**

Samarbeta med ert medieteam för att få fram den här informationen.

## Identiteter som stöds {#supported-identities}

Medallia stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| e-post | E-postadress | Välj e-postmålets identitet när du vill skicka enkäter om e-postinbjudan. När en profil är associerad med flera e-postadresser utlöser MediaMedia inbjudan till endast det första e-postmeddelandet. |
| telefon | Telefonnummer hashas i E.164-format | Välj telefonens målidentitet när du vill skicka SMS-baserade enkäter. Telefonnumret måste vara i E.164-format, som innehåller ett plustecken (+), en internationell landskod, en lokal områdeskod och ett telefonnummer. Till exempel: (+)(landskod)(riktnummer)(telefonnummer). När en profil är associerad med flera telefonnummer kommer Media att utlösa inbjudan endast till det första telefonnumret. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla nykvalificerade medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!UICONTROL OAuth Token Endpoint URL]**: Vanligtvis har formatet https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Hämta från ditt team för mediedistribution.
* **[!UICONTROL Client Secret]**: Hämta från ditt team för mediedistribution.

![Bild som visar autentiseringsskärmen för det här målet.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL API Gateway URL]**: Hämta från ditt team för mediedistribution. Används vanligtvis i formatet https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Hämta från ditt team för mediedistribution. Namnet på API:t för medieimport (kallas även webbfeed) som ska användas i den här anslutningen. Du kan aktivera olika målgrupper för olika import-API:er för att starta olika undersökningsprogram.

![Bild som visar målinformationsskärmen för det här målet.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

Följande namnutrymmen för målidentitet måste mappas beroende på användningsfallet:
* För e-postbaserade undersökningar måste **email** mappas som ett målfält med **målfält** > **Välj identitetsnamnutrymme** > **e-post**
* För SMS-baserade enkäter måste **phone** mappas som ett målfält med **målfält** > **Välj identitetsnamnområde** > **telefon**. Telefonnummer måste vara i E.164-format, som innehåller ett plustecken (+), en landskod, en lokal områdeskod och ett telefonnummer

Vi rekommenderar starkt att du även mappar ytterligare anpassade målattribut för att skapa personaliserade enkäter och lägger till ytterligare information om kunden till enkätposten:

* Personaliserade enkäter riktar sig vanligtvis till kunden efter namn
   * Mappa kundens förnamn till **målfält** > **Välj anpassade attribut** > **Attributnamn** > **förnamn**
   * Mappa kundens efternamn till **målfält** > **Välj anpassade attribut** > **attributnamn** > **efternamn**
* Lägg till mappningar för andra anpassade målattribut efter behov

![Bild som visar en exempelmappning för identiteter och attribut.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Dela exakt **Attributnamn** för varje anpassat målattribut som du mappar med hjälp av **målfält** > **Välj anpassade attribut** > **Attributnamn** med Media-leveransteamet. Du kan ta en skärmbild av mappningssidan och dela den direkt.

## Exporterade data {#exported-data}

När du har aktiverat segmenten på destinationen ska du informera ditt Media Delivery Team, som ska kunna validera exporterade data från Adobe Experience Platform till MediaMedia. Observera att enkäter endast kan aktiveras inom media efter lyckad dataverifiering. Före detta exporteras data till Medallia men kommer inte att utlösa undersökningar till kunderna.

Ett exempel-JSON för exporterade data anges nedan, som använder exempelmappningen från skärmbilden ovan i avsnittet **Karteattribut och identiteter**:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
