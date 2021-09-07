---
title: Pinterest Customer List Connection
description: Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.
source-git-commit: dc7e43a16923cb17a39a8ddb4ba114c0e9c0cc39
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 1%

---


# Pinterest Customer List Connection

## Översikt {#overview}

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

>[!IMPORTANT]
>
>Detta mål har skapats av Pinterest team. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på https://help.pinterest.com/en/contact.

## Förutsättningar {#prerequisites}

* Användaren måste autentisera med ett Pinterest-konto som har åtkomst till annonskontot som han/hon vill lägga till en målgrupp i. Information om delning av annonseringskonton finns [här](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Användaren skulle behöva åtkomstnivåerna &quot;målgrupp&quot;.
* Information om identitetsformat för kundlista finns [här](https://help.pinterest.com/en/business/article/audience-targeting).


## Identiteter som stöds {#supported-identities}

Pinterest kundlista har stöd för aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

I [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) för arbetsflödet för målaktivering mappar du önskade identiteter till målfältet *pinterest_publik*. Identiteter särskiljs och löses vid datainhämtning till Pinterest.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Mappa *GAID*-källidentitetens namnområde till målidentitetsfältet *pinterest_audiens*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| IDFA | Apple ID för annonsörer | Mappa *IDFA*-källidentitetsnamnutrymmet till målidentitetsfältet *pinterest_audiens*. Identiteter särskiljs och löses vid datainhämtning till Pinterest. |
| E-POST | E-postadresser (klartext eller hashas med SHA256-algoritmen) | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. <br> Mappa  ** källidentitetsfältet  *Email_LC_SHA256* till målidentitetsfältet  *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller annat) som används i Pinterest kundlista.

## Användningsexempel {#use-cases}

För att ni bättre ska förstå hur och när ni ska använda Pinterest kundlista är det här några exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.


### Användningsfall 1

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

## Anslut till mål {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).



### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Ditt Pinterest-konto-ID.

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att direktuppspela segmentets exportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Mer information finns på [Pinterest Help Center-sidan](https://help.pinterest.com/en/business/article/audience-targeting).