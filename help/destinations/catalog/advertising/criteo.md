---
keywords: Reklam. villkor,
title: Kriterieanslutning
description: Kriteriet ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personaliserade för att nå kunder med rätt annons vid rätt tidpunkt.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# (Beta) Kriterieanslutning

## Översikt {#overview}

>[!IMPORTANT]
>
>Den här dokumentationssidan har skapats av Criteo. Detta är för närvarande en betaprodukt och funktionaliteten kan komma att ändras. Kontakta Criteo direkt om du har frågor eller uppdateringsfrågor [här](mailto:criteoTechnicalPartnerships@criteo.com).

Kriteriet ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personaliserade för att nå kunder med rätt annons vid rätt tidpunkt.

## Förutsättningar {#prerequisites}

* Du måste ha ett administratörsanvändarkonto aktiverat [Criteo Management Center](https://marketing.criteo.com).
* Du behöver ditt Criteo Advertiser ID (fråga din Criteo-kontakt om du inte har detta ID).
* Du måste ange [!DNL GUM caller ID]om du vill använda [!DNL GUM ID] som identifierare.

## Begränsningar {#limitations}

* Kriteriet stöder för närvarande inte borttagning av användare från målgrupper.
* Endast tävlingens villkor godkänns [!DNL SHA-256]-hashed och normal text emails (att omvandlas till [!DNL SHA-256] före sändning). Skicka inga PII-filer (personligt ID-nummer, till exempel namn på enskilda personer eller telefonnummer).
* Kunden måste ange minst en identifierare för villkoret. Det prioriterar [!DNL GUM ID] som identifierare över hashad e-post eftersom det ger bättre matchningsfrekvens.

![Förutsättningar](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identiteter som stöds {#supported-identities}

Kriteriet stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Målidentitet | Beskrivning | Överväganden |
| --- | --- | --- |
| `email_sha256` | E-postadresser som hash-kodats med SHA-256-algoritmen | Både oformaterad text och SHA-256-hashed-e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du [!UICONTROL Apply transformation] om du vill att Platform automatiskt ska hash-koda data vid aktiveringen. |
| `gum_id` | Kriterium [!DNL GUM] cookie-identifierare | [!DNL GUM IDs] tillåta klienterna att upprätthålla en korrespondens mellan sina system för användaridentifiering och Criteos användaridentifiering ([!DNL UID]). Om identifierartypen är `GUM`, en extra parameter, [!DNL GUM Caller ID]måste också ingå. Kontakta er kontogrupp för att få reda på vad som är lämpligt [!DNL GUM Caller ID] eller om du vill ha mer information om detta `GUM` synkronisera, om det behövs. |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| --- | --- | --- |
| Exporttyp | Segmentexport | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i [!DNL Criteo] mål. |
| Exportfrekvens | Direktuppspelning | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](../../destination-types.md#streaming-destinations). |

## Användningsfall {#use-cases}

För att du bättre ska förstå hur du använder [!DNL Criteo] mål, här är några mål som Adobe Experience Platform-kunder kan uppnå med [!DNL Criteo]:

### Använd fall 1: Hämta trafik

Visa upp er verksamhet med relevanta produkterbjudanden och flexibla kreatörer. Med intelligenta produktrekommendationer kommer era annonser automatiskt att innehålla de produkter som mest troligt kommer att utlösa besök och engagemang. Flexibel målinriktning gör att ni kan bygga målgrupper utifrån Criteos uppsättning av e-handelsdata eller från era egna listor över potentiella kunder och CDP-segment för Adobe.

### Användningsfall 2: Öka konverteringsgraden för webbplatser

När besökarna lämnar er webbplats bör du påminna dem om vad de missar med återannonser som ökar konverteringsgraden genom att visa specialerbjudanden och hyperrelevanta erbjudanden, vart de än går. Koppla samman era CDP-segment i Adobe för att återengagera befintliga kunder eller inrikta er på konsumenter som liknar era mest lojala kunder.

## Anslut till villkor {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Autentisera till villkor

Så här ansluter du:

1. Logga in på Adobe Experience Platform och anslut till målet för villkoret.

   ![Logga in](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Du omdirigeras till Villkor för att godkänna anslutningen. Du kan först behöva logga in med dina autentiseringsuppgifter:

   ![Inloggningsvillkor](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Inloggningsvillkor](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Inloggningsvillkor](../../assets/catalog/advertising/criteo/log-in-3.png)


### Anslutningsparametrar {#connection-parameters}

Fyll i följande anslutningsparametrar när du har autentiserat till målet.

![Anslutningsparametrar](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Fält | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| Namn | Ett namn som hjälper dig att identifiera det här målet i framtiden. Namnet du väljer här är [!DNL Audience] namnet i Criteo Management Center och kan inte ändras i ett senare skede. | Ja |
| Beskrivning | En beskrivning som hjälper dig att identifiera det här målet i framtiden. | Nej |
| API-version | Version av rit-API. Välj Förhandsgranska. | Ja |
| Annonsörs-ID | ID för er organisations Criteo Advertiser. Kontakta er kontoansvarige för ditt kriterium för att få denna information. | Ja |
| Kriterium [!DNL GUM caller ID] | [!DNL GUM Caller ID] för er organisation. Kontakta er kontogrupp för att få reda på vad som är lämpligt [!DNL GUM Caller ID] eller om du vill ha mer information om detta [!DNL GUM] synkronisera, om det behövs. | Ja, när [!DNL GUM ID] anges som en identifierare |

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate-segments}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Du kan se de exporterade segmenten i [Centrum för kravhantering](https://marketing.criteo.com/audience-manager/dashboard).

Begärandeinstansen som mottogs av [!DNL Criteo] ser anslutningen ut ungefär så här:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Dataanvändning och styrning {#data-usage}

Alla Adobe Experience Platform-destinationer följer dataanvändningsprinciper när data hanteras. Mer information om hur Adobe Experience Platform använder datastyrning finns i [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Ytterligare resurser

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Criteo Developer Portal](https://developers.criteo.com)
