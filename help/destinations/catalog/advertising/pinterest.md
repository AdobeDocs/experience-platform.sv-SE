---
title: Pinterest Customer List Connection
description: Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# [!DNL Pinterest Customer List] anslutning

## Översikt {#overview}

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

>[!IMPORTANT]
>
>Detta mål har skapats av Pinterest team. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på https://help.pinterest.com/en/contact.

## Förutsättningar {#prerequisites}

* Användaren måste autentisera med ett Pinterest-konto som har åtkomst till annonskontot som han/hon vill lägga till en målgrupp i. Information om delning av annonseringskonton finns [här](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Användaren skulle behöva åtkomstnivåerna &quot;målgrupp&quot;.
* Information om identitetsformat för kundlista finns [här](https://help.pinterest.com/en/business/article/audience-targeting).

## Identiteter som stöds {#supported-identities}

The [!DNL Pinterest Customer List] målet har stöd för aktivering av de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

I [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) mappa önskade identiteter till målfältet i arbetsflödet för målaktivering *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa *GAID* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa *IDFA* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| E-POST | E-postadresser (klartext eller hashas med SHA256-algoritmen) | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. <br> Mappa *E-post* eller *Email_LC_SHA256* källans ID-namnområde till målidentitetsfältet *pinterest_målgrupp*. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i Pinterest kundlista. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Användningsexempel {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Pinterest Customer List] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Användningsfall 1

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Advertiser ID]**: Ditt Pinterest-annonserings-ID.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Se [Pinterest Help Center page](https://help.pinterest.com/en/business/article/audience-targeting) för ytterligare information.
