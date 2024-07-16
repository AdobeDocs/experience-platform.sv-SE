---
title: Verizon MediaYahoo DataX-anslutning
description: DataX är en aggregerad Verizon Media/Yahoo-infrastruktur som är värd för olika komponenter som gör att Verizon Media/Yahoo kan utbyta data med sina externa partner på ett säkert, automatiserat och skalbart sätt.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# [!DNL Verizon Media/Yahoo DataX]-anslutning

## Översikt {#overview}

[!DNL DataX] är en aggregerad [!DNL Verizon Media/Yahoo]-infrastruktur som är värd för olika komponenter som gör att [!DNL Verizon Media/Yahoo] kan utbyta data med sina externa partner på ett säkert, automatiserat och skalbart sätt.

>[!IMPORTANT]
>
>Den här målanslutnings- och dokumentationssidan skapas och underhålls av [!DNL DataX]-teamet hos [!DNL Verizon Media/Yahoo]. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Förhandskrav {#prerequisites}

**MDM-ID**

Detta är en unik identifierare i [!DNL Yahoo DataX] och det är ett obligatoriskt fält för inställning av dataexport till det här målet. Om du inte känner till det här ID:t kontaktar du kontohanteraren för [!DNL Yahoo DataX].

**Taxonomimetadata**

Taxonomiresursen definierar ett tillägg över basmetadatastrukturen [!DNL DataX]

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Läs mer om [taxonomimetadata](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) i utvecklardokumentationen för [!DNL DataX].

## Hastighetsgränser och skyddsräcken {#rate-limits-guardrails}

>[!IMPORTANT]
>
>När du aktiverar fler än 100 målgrupper till [!DNL Verizon Media/Yahoo DataX] kan du få hastighetsbegränsande fel från målet. När du aktiverar målgrupper till det här målet kan du försöka aktivera färre än 100 målgrupper i ett aktiveringsdataflöde. Om du behöver aktivera fler segment skapar du ett nytt mål för samma konto.

[!DNL DataX] är avgiftsbegränsad enligt kvotgränserna för taxonomi- och målgruppsposter som beskrivs i [DataX-dokumentationen](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Felkod | Felmeddelande | Beskrivning |
|---------|----------|---------|
| 429 För många begäranden | Hastighetsgränsen har överskridits per timme **(gräns: 100)** | Antal begäranden som tillåts i en timme per provider. |

{style="table-layout:auto"}

## Identiteter som stöds {#supported-identities}

[!DNL Verizon Media] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (Email, GAID, IDFA) som används i Verizon Media-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

[!DNL DataX] API:er är tillgängliga för annonsörer som vill rikta sig till en viss målgruppsgrupp som är sparad med e-postadresser i [!DNL Verizon Media] (VMG) kan snabbt skapa en ny målgrupp och skicka den önskade målgruppsgruppen med hjälp av VMG:s API i nära realtid.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

![Yahoo DataX-målkort i plattformsgränssnittet](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL MDM ID]**: Detta är en unik identifierare i [!DNL Yahoo DataX] och det är ett obligatoriskt fält för inställning av dataexport till det här målet. Om du inte känner till det här ID:t kontaktar du kontohanteraren för [!DNL Yahoo DataX].  Med MDM-ID:n kan data begränsas så att de bara kan användas av en viss uppsättning exklusiva användare (till exempel data från första part för annonsörer).

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper till ett mål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till mål.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Mer information finns i [!DNL Yahoo/Verizon Media] [dokumentationen för  [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
