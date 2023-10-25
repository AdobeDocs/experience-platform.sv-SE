---
keywords: direktuppspelning, Qualtrics-mål
title: Qualtrics Automations
description: Synkronisera upplevelser och användbara kunddata för att låsa upp personalisering i stor skala. Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience iD för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner.
last-substantial-update: 2023-10-25T00:00:00Z
source-git-commit: 57d3e136902201f9ba9bd2f427ebe0f876900671
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Qualtrics Automations

## Översikt {#overview}

Synkronisera upplevelser och användbara kunddata för att låsa upp personalisering i stor skala.

Använd aggregering av flera olika källor med driftsdata i Adobe Experience Platform som indata i Qualtrics Experience iD för att bättre förstå era kunder och möjliggöra riktad utåtriktad marknadsföring för att överbrygga klyftan när det gäller att förstå avsikter, känslor och upplevelsedrivrutiner.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Qualtrics-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt genom att logga in på [Navet för nöjda kunder](https://support-portal.qualtrics.com/).

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda *Qualtrics Automations* mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda denna destination.

### Använd skiftläge 1 {#use-case-1}

**Scenario**: Ett företag vill mäta kundnöjdheten över olika digitala kontaktytor, som webbplatser och mobilappar. De använder Adobe Experience Platform för att starta undersökningar baserade på användarinteraktioner, som att slutföra ett köp eller besöka en viss webbsida.

**Resultat**: Genom att samla in feedback i realtid kan företaget göra datadrivna förbättringar av kundupplevelsen, vilket leder till ökad kundnöjdhet och lojalitet.

### Använd skiftläge 2 {#use-case-2}

**Scenario**: En organisation har som mål att förbättra sin process för nyanställda. De använder Adobe Experience Platform för att samla in feedback från nyanställda genom enkäter. Undersökningar utlöses automatiskt efter en fördefinierad introduktionsperiod.

**Resultat**: Med kontinuerlig feedback kan organisationen anpassa och förbättra introduktionsprocessen, vilket ger bättre engagemang och produktivitet bland nya medarbetare.

## Förutsättningar

Innan du konfigurerar Qualtrics-målet i Adobe Experience Platform måste du kontrollera att följande krav är uppfyllda:

* Du har ett Qualtrics-konto.
* Du har fått den nödvändiga API-token från Qualtrics.

### Hämta en API-token

Nedan beskrivs de steg som krävs för att erhålla en API-token från Qualtrics.

1. Logga in på ditt Qualtrics-konto.
2. Gå till **Kontoinställningar**.
3. Välj **Qualtrics ID:n**.
4. På den här sidan letar du efter **API** -avsnittet innehåller en **Token** fält. Detta är API-token och krävs under målkonfigurationen.

## Identiteter som stöds {#supported-identities}

*Qualtrics Automations* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| e-post | E-postadresser med oformaterad text | Endast e-postadresser med oformaterad text stöds av Qualtrics. |
| external_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i *Qualtrics Automations* mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Som en del av autentiseringen måste du ange en **Användarnamn** och **Lösenord**. Användarnamnet är ditt Qualtrics-användarnamn och lösenordet är Qualtrics-kontots API-token. Följ instruktionerna från **Förutsättningar** ovan.

![Autentisering](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL URL]**: Den URL som finns i [JSON-händelse](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) som triggar [arbetsflöde i Frågor och svar](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Se skärmbilden nedan för ett exempel.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Målet har ett öppet schema så du kan skicka egenskaper till variabler.

#### Mappningsattribut

Om du vill lägga till ett attribut i mappningen väljer du bara **anpassade attribut** när en ny mappning läggs till. Du kan ange ett valfritt namn för attributet. Frågor uppmuntrar *camelCase* namnkonvention för attributnamn (se skärmbilden nedan för ett exempel).

![Eget attribut](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Se skärmbilden nedan för ett exempel på möjliga attributmappningar.

![Exempelmappningar](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mappa identiteter

Du måste välja ett identitetsnamnutrymme för det här målet. De två möjliga mappningarna av källfält till målfält är:

| Källfält | Målfält |
|--------------------|-----------------------|
| IdentityMap: Email | Identitet: e-post |
| IdentityMap: ECID | Identitet: external_id |

Se skärmbilden nedan för ett exempel.

![Namnutrymme för identitet](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

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

Om du vill verifiera att data har importerats i testversionerna går du till arbetsflödet som innehåller dina **JSON-händelse**, därifrån, gå till **Kör historik** där du bör se hur arbetsflödet fungerar. Varje arbetsflöde har statusen **Slutförd** eller **Misslyckades**. Om du väljer en viss körning visas mer information om den, så att du kan felsöka om du stöter på några problem.

Om inga körningar visas i **Kör historik** innebär det att arbetsflödet inte har utlösts än, vilket kan tyda på ett problem. Kontrollera att arbetsflödet är aktiverat och att **URL** i Adobe Experience Platform är korrekt. Arbetsflödeskörningar sker inte direkt, så du kan behöva vänta en kort stund innan det är klart.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
