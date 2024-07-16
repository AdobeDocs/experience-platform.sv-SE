---
keywords: direktuppspelning, Qualtrics-mål
title: Qualtrics Automations
description: Synkronisera upplevelser och användbara kunddata för att låsa upp personalisering i stor skala. Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience iD för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Qualtrics Automations

## Översikt {#overview}

Synkronisera upplevelser och användbara kunddata för att låsa upp personalisering i stor skala.

Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience iD för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Qualtrics-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt genom att logga in på [Customer Success Hub](https://support-portal.qualtrics.com/).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet *Qualtrics Automations* finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1 {#use-case-1}

**Scenario**: Ett företag vill mäta kundnöjdheten över olika digitala kontaktytor, till exempel deras webbplats och mobilapp. De använder Adobe Experience Platform för att starta undersökningar baserade på användarinteraktioner, som att slutföra ett köp eller besöka en viss webbsida.

**Resultat**: Genom att samla in realtidsfeedback kan företaget göra datadrivna förbättringar av sin kundupplevelse, vilket leder till ökad nöjdhet och lojalitet.

### Använd skiftläge 2 {#use-case-2}

**Scenario**: En organisation har som mål att förbättra sin process för nyanställda. De använder Adobe Experience Platform för att samla in feedback från nyanställda genom enkäter. Undersökningar utlöses automatiskt efter en fördefinierad introduktionsperiod.

**Resultat**: Med kontinuerlig feedback kan organisationen anpassa och förbättra introduktionsprocessen, vilket ger bättre engagemang och produktivitet bland nya medarbetare.

## Förhandskrav

Innan du konfigurerar Qualtrics-målet i Adobe Experience Platform måste du kontrollera att följande krav är uppfyllda:

* Du har ett Qualtrics-konto.
* Du har fått den nödvändiga API-token från Qualtrics.

### Hämta en API-token

Nedan beskrivs de steg som krävs för att erhålla en API-token från Qualtrics.

1. Logga in på ditt Qualtrics-konto.
2. Gå till **Kontoinställningar**.
3. Välj **Frågor och svar**.
4. På den här sidan söker du efter avsnittet **API** som innehåller ett **Token**-fält. Detta är API-token och krävs under målkonfigurationen.

## Identiteter som stöds {#supported-identities}

*Qualtrics Automations* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| e-post | E-postadresser med oformaterad text | Endast e-postadresser med oformaterad text stöds av Qualtrics. |
| external_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer eller andra) som används i målet *Qualtrics Automations*. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Som en del av autentiseringen måste du ange ett **användarnamn** och **lösenord**. Användarnamnet är ditt Qualtrics-användarnamn och lösenordet är Qualtrics-kontots API-token. Följ instruktionerna i avsnittet **Krav** ovan för att hämta API-token.

![Autentisering](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL URL]**: Den URL som hittades i [JSON Event](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) som utlöser ditt [arbetsflöde i Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Se skärmbilden nedan för ett exempel.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Målet har ett öppet schema så du kan skicka egenskaper till variabler.

#### Mappningsattribut

Om du vill lägga till ett attribut i mappningen väljer du bara **anpassade attribut** när du lägger till en ny mappning. Du kan ange ett valfritt namn för attributet. Qualtrics uppmuntrar namnkonventionen *camelCase* för attributnamn (se skärmbilden nedan som exempel).

![Anpassat attribut](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Se skärmbilden nedan för ett exempel på möjliga attributmappningar.

![Exempelmappningar](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mappa identiteter

Du måste välja ett identitetsnamnutrymme för det här målet. De två möjliga mappningarna av källfält till målfält är:

| Source Field | Målfält |
|--------------------|-----------------------|
| IdentityMap: Email | Identitet: e-post |
| IdentityMap: ECID | Identitet: external_id |

Se skärmbilden nedan för ett exempel.

![Identitetsnamnområde](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Exporterade data/Validera dataexport {#exported-data}

Som tidigare nämnts använder det här målet ett öppet schema, så alla egenskaper kan skickas till Qualtrics. De data som skickas till Qualtrics följer dock nedanstående struktur:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Om du vill verifiera att data har importerats i SQL går du till arbetsflödet som innehåller din **JSON Event** därifrån och går till **Kör historik** där du bör se hur ditt arbetsflöde fungerar. Varje arbetsflöde har statusen **Slutfört** eller **Misslyckat**. Om du väljer en viss körning visas mer information om den, så att du kan felsöka om du stöter på några problem.

Om det inte finns några synliga körningar i **körningshistorik** innebär det att arbetsflödet inte har utlösts än, vilket kan tyda på ett problem. Kontrollera att arbetsflödet är aktiverat och att **URL** i målet i Adobe Experience Platform är korrekt. Arbetsflödeskörningar sker inte direkt, så du kan behöva vänta en kort stund innan det är klart.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
