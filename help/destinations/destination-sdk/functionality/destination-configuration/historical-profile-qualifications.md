---
description: Lär dig mer om de historiska profilkvalifikationer som stöds av mål som skapats med Destination SDK.
title: Krav på historisk profil
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Krav på historisk profil

Alla destinationer som skapas via Destination SDK har som standard stöd för historiska profilkvalifikationer. Det innebär att när användarna först ställer in ett aktiveringsdataflöde för destinationerna innehåller den första exporten alla målgrupper som någonsin kvalificerat sig för det segmentet.

Detta beteende definieras av parametern `"backfillHistoricalProfileData":true` i målkonfigurationen.

>[!IMPORTANT]
>
>Historiska profilkvalifikationer är aktiverade för alla mål som skapats via Destination SDK och parametern `backfillHistoricalProfileData` är inte användarkonfigurerbar.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Nästa steg {#next-steps}

När du har läst den här artikeln bör du känna till att Experience Platform automatiskt exporterar en historik över alla profiler som någonsin kvalificerats för en aktiverad målgrupp när målgruppen först exporteras till målet. Det här alternativet kan inte konfigureras i Destination SDK eller i användargränssnittet för Experience Platform.

Mer information om de andra målkomponenterna finns i följande artiklar:

* [Kundautentisering](customer-authentication.md)
* [OAuth2-auktorisering](oauth2-authorization.md)
* [Kunddatafält](customer-data-fields.md)
* [Gränssnittsattribut](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](identity-namespace-configuration.md)
* [Mappningskonfigurationer som stöds](supported-mapping-configurations.md)
* [Destinationsleverans](destination-delivery.md)
* [Konfiguration av målgruppsmetadata](audience-metadata-configuration.md)
* [Samlingsprincip](aggregation-policy.md)
* [Batchkonfiguration](batch-configuration.md)
