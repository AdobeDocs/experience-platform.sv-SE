---
title: Konfigurerbara och gemensamma exportinställningar för destinationer
description: Lär dig vilka exportinställningar i destinationer som kan konfigureras på en målnivå och som är fasta och inte kan redigeras.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Konfigurerbara och gemensamma exportinställningar för destinationer

När du tänker på exportbeteendet till destinationer i Experience Platform måste du överväga tre olika nivåer för vilka konfigurationer fungerar.

* På en första nivå är vissa av inställningarna för profilexportbeteende och konfigurationsinställningar gemensamma för alla mål som tillhör en måltyp. De här inställningarna hänvisar till vad som utlöser en målexport och vad som ingår i en export och kan inte redigeras av målutvecklare eller CDP-användare i realtid.
* På en andra nivå kan vissa inställningar anpassas på en målnivå av målutvecklaren när måldestinationer skapas med Destination SDK.
* På en tredje nivå finns det konfigurationsinställningar som kan ställas in av CDP-användare i realtid i aktiveringsarbetsflödena.

![Bild som visar hur vanliga och konfigurerbara exportinställningar för destinationer samverkar](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Den här sidan beskriver eller länkar ut till alla vanliga och konfigurerbara exportinställningar för destinationer på de tre nivåer som beskrivs ovan.

## Gemensamma exportinställningar för olika måltyper {#common-settings-across-destination-types}

Beteendet för destinationsexport är konsekvent för destinationer som tillhör en destinationstyp med avseende på *vad som utlöser en målexport* och *vad som ingår i målexporten*. Destinationsexporter utlöses av meddelanden om att destinationstjänsten tar emot från [tjänst för kundprofil i realtid](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Vad som ingår i målexporten varierar något mellan olika måltyper. Läs mer om [mönster för vanliga exportbeteenden per måltyp](/help/destinations/how-destinations-work/profile-export-behavior.md). Dessa inställningar kan inte redigeras av målutvecklare eller CDP-användare i realtid.

## Anpassningsbara exportinställningar per målutvecklare {#customizable-settings-by-destination-developers}

Målutvecklare kan använda [Destination SDK](/help/destinations/destination-sdk/overview.md) för att skapa anpassade eller producerade (privata eller offentliga) destinationer. Destination SDK ger utvecklare stor flexibilitet att konfigurera destinationer baserat på funktionaliteten i senare led i API-slutpunkterna och filmottagningssystemen. Baserat på de underordnade funktionerna har målutvecklare följande konfigurationsalternativ tillgängliga när de konfigurerar ett mål med Destination SDK:

* Avgör vilka attribut och identiteter som kan exporteras från Experience Platform till målet. Avgör också vilka identiteter som krävs av deras mål för att dataexporten ska lyckas.
* Ange en aggregeringsprincip som bestämmer hur lång tid Experience Platform ska vänta när HTTP-meddelanden som ska skickas till API-integreringar samlas in. Målutvecklare kan konfigurera olika aggregeringstyper för att avgöra hur många profiler som ska inkluderas i utgående HTTP-meddelanden och hur länge Experience Platform ska vänta tills HTTP-meddelandet skickas. Här finns omfattande information om [konfigurationsalternativ för aggregeringsprincip](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) som är tillgängliga för målutvecklare i Destinationens SDK dokumentation.
* Kontrollera om HTTP-meddelandeexport ska innehålla profiler som är kvalificerade för segment, som tas bort från segment eller båda.
* Avgör vilka filnamn och filformateringskonfigurationer som ska vara tillgängliga för användare vid export av filer.

## Inställningar på en dataflödesnivå som kan anpassas av användare {#settings-on-dataflow-level}

Förutom de icke-redigerbara inställningarna som är beroende av måltyp och de inställningar som har konfigurerats av målutvecklaren, finns det vissa exportinställningar som användare kan konfigurera i aktiveringsarbetsflödet. De här inställningarna är relaterade till exportschemat för ett visst dataflöde till ett mål, attribut och identitetsfält som ska exporteras i ett dataflöde eller filformateringsalternativen för exporterade filer.

Vilka inställningar som är tillgängliga för användare vid anslutning till ett mål beror på hur målet konfigurerades av målutvecklaren och vilka inställningar de gjorde tillgängliga för användarna.

Till exempel [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations)kan en målutvecklare konfigurera vilka identiteter som deras mål godkänner och endast de identiteterna visas för användaren i [mappningssteg för aktiveringsarbetsflödet](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), enligt nedan:

![Skärminspelning av identitetsvalet för målfältet i mappningssteget i aktiveringsarbetsflödet. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

På samma sätt gäller för [filbaserade mål](/help/destinations/destination-types.md#file-based)kan målutvecklaren avgöra vilken [filnamnstillägg](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) de vill göra tillgängliga för sina destinationer, eller som [filformateringsalternativ](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) de vill göra tillgängliga och användaren kan välja bland dessa alternativ, vilket visas nedan:

![Skärminspelning av filformateringsalternativet vid anslutning till ett filbaserat mål.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Skärminspelning av alternativet för filnamnstillägg i schemaläggningssteget i aktiveringsarbetsflödet. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Läs mer om de olika alternativen och stegen i aktiveringsarbetsflödet:

* [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Aktivera målgruppsdata för företagsdestinationer](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportera filer on demand till batchmål](/help/destinations/ui/export-file-now.md)
* [(Beta) Exportera datauppsättningar till molnlagringsmål](/help/destinations/ui/export-datasets.md)

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu vilka exportinställningar för mål som är gemensamma för olika måltyper, som kan konfigureras på en enskild målnivå av utvecklare, och vilka inställningar som kan redigeras av användare i aktiveringsarbetsflödet.

Nu kan du läsa mer om [mönster för vanliga exportbeteenden per måltyp](/help/destinations/how-destinations-work/profile-export-behavior.md).

För målutvecklare kan du [komma igång](/help/destinations/destination-sdk/getting-started.md) med Destination SDK. För användare som vill aktivera data kan du ta en titt på alla tillgängliga mål i [katalog](/help/destinations/catalog/overview.md).
