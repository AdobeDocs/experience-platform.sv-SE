---
title: Medieanslutning
description: Aktivera profiler för riktade medieundersökningar och insamling av feedback för att bättre förstå kundernas behov och förväntningar.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 1%

---


# Medieanslutning

## Översikt {#overview}

Aktivera profiler för riktade medieundersökningar och insamling av feedback för att bättre förstå kundernas behov och förväntningar.

>[!IMPORTANT]
>
>Dokumentationssidan skapades av Medallia-teamet. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på adobe-integrations@medallia.com.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda mediedestinationen finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Använd skiftläge 1

Ett B2B-varumärke vill utvärdera och effektivisera sitt introduktionsprogram. De vill skicka personaliserade enkäter i realtid till kunder som just slutfört introduktionsprocessen.

### Använd skiftläge 2

En återförsäljare vill förstå kundernas preferenser bättre för orderhantering. De vill skicka en kort enfråge-SMS-enkät till kunder som har gjort online- och butiksköp den senaste månaden.

## Förutsättningar {#prerequisites}

Följande information krävs för att upprätta en parallellanslutning:
* **URL för OAuth-tokenslutpunkt**
* **Klient-ID**
* **Klienthemlighet**
* **API Gateway-URL**
* **Importera API-namn**

Samarbeta med ert medieteam för att få fram den här informationen.

## Identiteter som stöds {#supported-identities}

Medallia stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| e-post | E-postadress | Välj e-postmålets identitet när du vill skicka enkäter om e-postinbjudan. När en profil är associerad med flera e-postadresser utlöser MediaMedia inbjudan till endast det första e-postmeddelandet. |
| telefon | Telefonnummer hashas i E.164-format | Välj telefonens målidentitet när du vill skicka SMS-baserade enkäter. Telefonnumret måste vara i E.164-format, som innehåller ett plustecken (+), en internationell landskod, en lokal områdeskod och ett telefonnummer. Till exempel: (+)(landskod)(riktnummer)(telefonnummer). När en profil är associerad med flera telefonnummer kommer Media att utlösa inbjudan endast till det första telefonnumret. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla nykvalificerade medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL OAuth Token Endpoint URL]**: Används vanligtvis i formatet https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Hämta material från ert medieteam.
* **[!UICONTROL Client Secret]**: Hämta material från ert medieteam.

![Bild som visar autentiseringsskärmen för det här målet.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL API Gateway URL]**: Hämta material från ert medieteam. Används vanligtvis i formatet https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Hämta material från ert medieteam. Namnet på API:t för medieimport (kallas även webbfeed) som ska användas i den här anslutningen. Du kan aktivera olika segment till olika import-API:er för att utlösa olika undersökningsprogram.

![Bild som visar skärmen för målinformation för det här målet.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Följande namnutrymmen för målidentitet måste mappas beroende på användningsfallet:
* För e-postbaserade undersökningar **e-post** måste mappas som ett målfält med **Målfält** > **Välj namnområde för identitet** > **e-post**
* För SMS-baserade undersökningar **telefon** måste mappas som ett målfält med **Målfält** > **Välj namnområde för identitet** > **telefon**. Telefonnummer måste vara i E.164-format, som innehåller ett plustecken (+), en landskod, en lokal områdeskod och ett telefonnummer

Vi rekommenderar starkt att du även mappar ytterligare anpassade målattribut för att skapa personaliserade enkäter och lägger till ytterligare information om kunden till enkätposten:

* Personaliserade enkäter riktar sig vanligtvis till kunden efter namn
   * Mappa kundens förnamn till **Målfält** > **Välj anpassade attribut** > **Attributnamn** > **förnamn**
   * Mappa kundens efternamn till **Målfält** > **Välj anpassade attribut** > **Attributnamn** > **efternamn**
* Lägg till mappningar för andra anpassade målattribut efter behov

![Bild som visar en exempelmappning för identiteter och attribut.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Dela med er Media Delivery-grupp exakt **Attributnamn** för varje anpassat målattribut du mappar med **Målfält** > **Välj anpassade attribut** > **Attributnamn**. Du kan ta en skärmbild av mappningssidan och dela den direkt.

## Exporterade data {#exported-data}

När du har aktiverat segmenten på destinationen ska du informera ditt Media Delivery Team, som ska kunna validera exporterade data från Adobe Experience Platform till MediaMedia. Observera att undersökningar endast kan aktiveras inom media efter framgångsrik dataverifiering. Innan detta kommer uppgifterna att exporteras till Medallia, men de kommer inte att utlösa undersökningar till kunderna.

Ett exempel på JSON för exporterade data anges nedan, som använder exempelmappningen från skärmbilden ovan i **Mappa attribut och identiteter** avsnitt:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
