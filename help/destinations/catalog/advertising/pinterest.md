---
title: Pinterest Customer List Connection
description: Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 02110e4b4156774c2961803f78ae1c3fc9d6240a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# [!DNL Pinterest Customer List] anslutning

## Översikt {#overview}

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

>[!IMPORTANT]
>
>Det här målet har byggts av Pinterest team. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på https://help.pinterest.com/en/contact.

## Förutsättningar {#prerequisites}

* Användaren måste autentisera med ett Pinterest-konto som har åtkomst till annonskontot som han/hon vill lägga till en målgrupp i. Information om delning av annonseringskonton finns [här](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Användaren skulle behöva åtkomstnivåerna &quot;målgrupp&quot;.
* Information om identitetsformat för kundlista finns [här](https://help.pinterest.com/en/business/article/audience-targeting).

## Identiteter som stöds {#supported-identities}

The [!DNL Pinterest Customer List] målet har stöd för aktivering av de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

I [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) mappa önskade identiteter till målfältet i arbetsflödet för målaktivering *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa *GAID* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa *IDFA* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| E-POST | E-postadresser (klartext eller hashas med SHA256-algoritmen) | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. <br> Mappa *E-post* eller *Email_LC_SHA256* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i Pinterest kundlista. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Pinterest Customer List] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda denna destination.

### Användningsfall 1

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Ad Account ID]**: Ditt Pinterest-annonserings-ID.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Läs mer i [Pinterest Help Center page](https://help.pinterest.com/en/business/article/audience-targeting) om du vill ha mer information.

+++ Visa ändringslogg


| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| November 2023 | Funktioner och dokumentation | Pinterest-målet i Real-Time CDP använder nu API:t för v5-annonsering. |

{style="table-layout:auto"}


+++
