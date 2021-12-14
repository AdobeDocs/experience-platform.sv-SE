---
title: Verizon MediaYahoo DataX-anslutning
description: DataX är en aggregerad Verizon Media/Yahoo-infrastruktur som är värd för olika komponenter som gör att Verizon Media/Yahoo kan utbyta data med sina externa partner på ett säkert, automatiserat och skalbart sätt.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---

# Verizon Media/Yahoo DataX-anslutning

## Översikt {#overview}

DataX är en aggregerad Verizon Media/Yahoo-infrastruktur som är värd för olika komponenter som gör att Verizon Media/Yahoo kan utbyta data med sina externa partner på ett säkert, automatiserat och skalbart sätt.

>[!IMPORTANT]
>
>Dokumentationssidan skapades av Verizon Media/Yahoos DataX-team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Förutsättningar {#prerequisites}

**MDM-ID**

Detta är en unik identifierare i Yahoo DataX och det är ett obligatoriskt fält för inställning av dataexport till det här målet. Om du inte känner till det här ID:t kontaktar du kontohanteraren för Yahoo Data X.

**Hastighetsgräns**

DataX är avgiftsbegränsat för de kvotgränser för taxonomi- och målgruppsposter som anges i [DataX-dokumentation](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Felkod | Felmeddelande | Beskrivning |
|---------|----------|---------|
| 429 För många begäranden | Hastighetsgränsen har överskridits per timme **(Gräns: 100)** | Antal begäranden som tillåts i en timme per provider. |

{style=&quot;table-layout:auto&quot;}

**Taxonomimetadata**

Taxonomiresursen definierar ett tillägg över basdatax-metadatastrukturen

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

Läs mer om [Taxonomimetadata](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) i DataX-utvecklardokumentationen.

## Identiteter som stöds {#supported-identities}

Verizon Media stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) med de identifierare (e-post) som används i Verizon Media-målet.

## Användningsexempel {#use-cases}

DataX-API:er är tillgängliga för annonsörer som vill rikta sig till en viss målgruppsgrupp som är avstämd från e-postadresser i Verizon Media (VMG) kan snabbt skapa ett nytt segment och skicka den önskade målgruppsgruppen med hjälp av VMG:s API i nära realtid.

## Anslut till mål {#connect}

![Yahoo DataX-målkort i plattformsgränssnitt](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL MDM ID]**: Detta är en unik identifierare i Yahoo DataX och det är ett obligatoriskt fält för inställning av dataexport till det här målet. Om du inte känner till det här ID:t kontaktar du kontohanteraren för Yahoo Data X.  Med MDM-ID:n kan data begränsas så att de bara kan användas av en viss uppsättning exklusiva användare (till exempel data från första part för annonsörer).

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment till ett mål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur målgruppssegment aktiveras för destinationer.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Mer information finns i Yahoo/Verizon Media [dokumentation om DataX](https://developer.verizonmedia.com/datax/guide/).
