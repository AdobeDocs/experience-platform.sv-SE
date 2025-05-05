---
keywords: Reklam; villkor.
title: Kriterieanslutning
description: Criteo ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personanpassade för att nå kunder med rätt annons, vid rätt tidpunkt.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 10%

---

# Kriterieanslutning

## Översikt {#overview}

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Criteo. Om du har frågor eller uppdateringsfrågor kontaktar du Villkor direkt [här](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo ger betrodd och slagkraftig annonsering för att ge alla konsumenter bättre upplevelser över det öppna internet. Med världens största datauppsättning för e-handel och AI av allra högsta klass ser Criteo till att alla kontaktytor under hela kundresan är personanpassade för att nå kunder med rätt annons, vid rätt tidpunkt.

## Förhandskrav {#prerequisites}

* Du måste ha ett administratörsanvändarkonto på [Criteo Management Center](https://marketing.criteo.com).
* Du behöver ditt Criteo Advertiser ID (fråga din Criteo-kontakt om du inte har detta ID).
* Du måste ange [!DNL GUM caller ID] om du vill använda [!DNL GUM ID] som identifierare.

## Begränsningar {#limitations}

* Kriteriet accepterar endast [!DNL SHA-256]-hash-kodade och oformaterade e-postmeddelanden (som ska omformas till [!DNL SHA-256] innan de skickas). Skicka inga PII-filer (personligt ID-nummer, till exempel namn på enskilda personer eller telefonnummer).
* Kunden måste ange minst en identifierare för villkoret. Den prioriterar [!DNL GUM ID] som identifierare framför hashas-e-post eftersom den bidrar till bättre matchningsfrekvens.

![Förhandskrav](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identiteter som stöds {#supported-identities}

Kriteriet stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv-SE#getting-started).

| Målidentitet | Beskrivning | Överväganden |
| --- | --- | --- |
| `email_sha256` | E-postadresser som hashas med SHA-256-algoritmen | Både oformaterad text och SHA-256-hashed-e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut ska du markera alternativet [!UICONTROL Apply transformation] så att Experience Platform automatiskt hash-kodar data vid aktiveringen. |
| `gum_id` | Identifierare för cookie-filen [!DNL GUM] | [!DNL GUM IDs] tillåter klienter att upprätthålla en korrespondens mellan användaridentifieringssystemet och Criteos användaridentifiering ([!DNL UID]). Om identifierartypen är `gum_id` måste även ytterligare en parameter, [!DNL GUM Caller ID], tas med. Kontakta ditt kundkontoteam för att få information om rätt [!DNL GUM Caller ID] eller om du vill ha mer information om den här [!DNL GUM ID]-synkroniseringen, om det behövs. |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| --- | --- | --- |
| Exporttyp | Målgruppsexport | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i målet [!DNL Criteo]. |
| Exportfrekvens | Direktuppspelning | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](../../destination-types.md#streaming-destinations). |

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur du använder målet [!DNL Criteo] finns det några mål som Adobe Experience Platform-kunder kan uppnå med [!DNL Criteo]:

### Användningsfall 1: Hämta trafik

Visa upp er verksamhet med relevanta produkterbjudanden och flexibla kreatörer. Med intelligenta produktrekommendationer kommer era annonser automatiskt att innehålla de produkter som mest troligt kommer att utlösa besök och engagemang. Med flexibel målinriktning kan ni bygga målgrupper utifrån Criteos uppsättning av e-handelsdata eller från era egna listor över potentiella kunder och Adobe CDP-segment.

### Använd fall 2: Öka konverteringen av webbplatser

När besökarna lämnar er webbplats bör du påminna dem om vad de missar med återannonser som ökar konverteringsgraden genom att visa specialerbjudanden och hyperrelevanta erbjudanden, vart de än går. Koppla samman er Adobe CDP-målgrupp för att återengagera befintliga kunder eller inrikta er på kunder som liknar era mest lojala kunder.

## Anslut till villkor {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Autentisera till villkor

Så här ansluter du:

1. Logga in på Adobe Experience Platform och anslut till målet för villkoret.

   ![Logga in](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Du omdirigeras till Villkor för att godkänna anslutningen. Du kan först behöva logga in med dina autentiseringsuppgifter:

   ![Kriterieinloggning](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Kriterieinloggning](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Kriterieinloggning](../../assets/catalog/advertising/criteo/log-in-3.png)


### Anslutningsparametrar {#connection-parameters}

Fyll i följande anslutningsparametrar när du har autentiserat till målet.

![Anslutningsparametrar](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Fält | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| Namn | Ett namn som hjälper dig att identifiera det här målet i framtiden. Det namn du väljer här blir namnet [!DNL Audience] i Criteo Management Center och kan inte ändras i ett senare skede. | Ja |
| Beskrivning | En beskrivning som hjälper dig att identifiera det här målet i framtiden. | Nej |
| Annonsörs-ID | ID för er organisations Criteo Advertiser. Kontakta er kontoansvarige för ditt kriterium för att få denna information. | Ja |
| Villkor [!DNL GUM caller ID] | [!DNL GUM Caller ID] i din organisation. Kontakta ditt kundkontoteam för att få information om rätt [!DNL GUM Caller ID] eller om du vill ha mer information om den här [!DNL GUM]-synkroniseringen, om det behövs. | Ja, när [!DNL GUM ID] anges som en identifierare |

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate-segments}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Du kan se de exporterade målgrupperna i [Criteo Management Center](https://marketing.criteo.com/audience-manager/dashboard).

Innehållet i begäran om att lägga till en användarprofil som tas emot av anslutningen [!DNL Criteo] ser ut ungefär så här:

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

Innehållet i borttagningen av användarprofilen som togs emot av anslutningen [!DNL Criteo] ser ut ungefär så här:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
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

Alla Adobe Experience Platform-destinationer följer dataanvändningsprinciper när data hanteras. Mer information om hur Adobe Experience Platform använder datastyrning finns i [Översikt över datastyrning](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=sv-SE).

## Ytterligare resurser

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Kriterieutvecklarportal](https://developers.criteo.com)
