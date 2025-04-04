---
description: Destinationstjänsten i Adobe Experience Platform använder konfigurationsslutpunkter för flera komponenter som bygger upp målfunktionaliteten. Se hur dessa komponenter tillsammans gör det möjligt för Experience Platform att ansluta till målpartners, skicka anpassade meddelanden och aktivera profildata i hela det digitala ekosystemet.
title: Konfigurationsalternativ i Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Konfigurationsalternativ i Destination SDK

Destinationstjänsten i Adobe Experience Platform använder konfigurationsslutpunkter för flera komponenter som bygger upp målfunktionaliteten.

Tillsammans gör dessa komponenter det möjligt för Experience Platform att ansluta till målplattformar, skicka anpassade meddelanden, exportera anpassade filer och aktivera profildata i hela det digitala ekosystemet.

Bilden nedan visar en översikt på hög nivå över de komponenter som du kan konfigurera via Destination SDK för att skapa ett eget mål. Dessa komponenter beskrivs närmare nedan.

>[!BEGINSHADEBOX]

![Diagram som visar Destination SDK-komponenter, konfigurationsslutpunkter och de åtgärder som stöds av dem.](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## Serverkonfiguration {#server-configuration}

Målserverkonfigurationen kopplar ihop information om serverspecifikationerna och den mall som används av Adobe för att leverera nyttolaster till ditt mål.

Här anger du till exempel vilka API-slutpunkter på din sida som Experience Platform ska ansluta till, samt rubrikerna och formatet för de API-anrop som Experience Platform ska göra.

För filbaserade mål innehåller den här konfigurationen även de filformat och komprimeringsformat som stöds för destinationen. Du kan konfigurera de funktioner som beskrivs nedan via [målserverns slutpunkt](../authoring-api/destination-server/create-destination-server.md).

* [Serverspecifikationer](destination-server/server-specs.md): En konfigurationsmall som innehåller information om lagringsplatsen eller HTTP-slutpunkten dit data skickas.
* [Mallspecifikationer](destination-server/templating-specs.md): I den här mallen kan du definiera hur HTTP API-begäran ska struktureras för slutpunkten, inklusive hur du omformar profilattributfält mellan XDM-schemat och det format som din plattform stöder. Använd den här informationen tillsammans med dokumentationen för [meddelandeformat](destination-server/message-format.md).
* [Meddelandeformat](destination-server/message-format.md): I det här avsnittet beskrivs ingående information om vilka mallspråk, meddelandeformat som stöds och den information som krävs av Adobe för att konfigurera integreringen med din plattform. Använd den här informationen tillsammans med dokumentationen för [mallspecifikationer](destination-server/templating-specs.md).
* [Filspecifikationer](destination-server/file-formatting.md): En konfigurationsmall som innehåller filformatering och komprimeringsalternativ för gruppmålet.

## Målkonfiguration {#destination-configuration}

Den här konfigurationsslutpunkten innehåller grundläggande och avancerad information om målet. Här anger du t.ex. vilka identitetstyper som ditt mål kan hantera, det önskade formatet för exporterade filer (för filbaserade mål) och olika gränssnittsattribut för målkortet i Adobe Experience Platform-användargränssnittet.

I dokumentationen nedan finns mer information om var och en av målkonfigurationskomponenterna. Du kan konfigurera de funktioner som beskrivs nedan via [målslutpunkten](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Konfiguration för kundautentisering](destination-configuration/customer-authentication.md): Välj den autentiseringsmekanism som Experience Platform ska använda för att ansluta till ditt mål. Den här konfigurationen genererar sidan [Konfigurera nytt mål](../../ui/connect-destination.md) i Experience Platform-användargränssnittet, där användare ansluter Experience Platform till de konton de har med ditt mål.
* [OAuth2-auktorisering](destination-configuration/oauth2-authorization.md): Lär dig mer om alla [!DNL OAuth2] autentiseringsflöden som stöds av Destination SDK och få instruktioner om hur du konfigurerar [!DNL OAuth2]-autentisering för ditt mål.
* [Kunddatafält](destination-configuration/customer-data-fields.md): Lär dig hur du skapar indatafält i Experience Platform-gränssnittet som gör att dina användare kan ange olika typer av information som är relevant för att ansluta och exportera data till ditt mål.
* [Gränssnittsattribut](destination-configuration/ui-attributes.md): Lär dig hur du konfigurerar gränssnittsattributen, till exempel dokumentationslänken, målkortskategorin och målanslutningstypen och målfrekvensen, för mål som skapats med Destination SDK.
* [Schemakonfiguration](destination-configuration/schema-configuration.md): Lär dig hur du definierar målschemat som användare kan mappa profilattribut och identiteter till.
* [Namnområdeskonfiguration för identitet](destination-configuration/identity-namespace-configuration.md): Lär dig hur du konfigurerar identiteter som stöds av ditt mål. Den här konfigurationen fyller i målidentiteterna i [mappningssteget](../../ui/activate-segment-streaming-destinations.md#mapping) i Experience Platform-användargränssnittet, där användare mappar identiteter och attribut från sina XDM-scheman till schemat i målet.
* [Målleverans](destination-configuration/destination-delivery.md): Lär dig hur du konfigurerar exakt vart exporterade data ska skickas och vilken autentiseringsregel som används på den plats där data ska landas.
* [Konfigurering av målgruppsmetadata](destination-configuration/audience-metadata-configuration.md): Lär dig hur målgruppsmetadata som målgruppsnamn eller ID:n ska delas mellan Experience Platform och ditt mål.
* [Aggregeringsprincip](destination-configuration/aggregation-policy.md): Lär dig hur du ställer in en aggregeringsprincip för att avgöra hur HTTP-begäranden till ditt mål ska grupperas och grupperas.
* [Gruppkonfiguration](destination-configuration/batch-configuration.md): Ange olika inställningar för filnamngivning och exportschemaläggning som är tillgängliga för användare vid anslutning till målet i Experience Platform-användargränssnittet.
* [Historisk profilkvalificering](destination-configuration/historical-profile-qualifications.md): Lär dig mer om de historiska profilkvalificeringar som stöds av mål som skapats med Destination SDK.

## Konfiguration av målgruppsmetadata {#audience-metadata-configuration}

Med den här komponenten kan du konfigurera hur målgrupper skapas, uppdateras eller tas bort programmatiskt i ditt mål. För filbaserade mål gör det möjligt att konfigurera ett meddelande så snart filerna har levererats till ditt mål. Du kan konfigurera den här funktionen via [målgruppsmallens slutpunkt](../metadata-api/create-audience-template.md).

## Nästa steg {#next-steps}

Genom att läsa den här artikeln får du nu en allmän översikt över funktionerna i Destination SDK och vilka sidor som ska läsas för mer information om specifika konfigurationer. Därefter kan du läsa guiderna som innehåller alla steg som krävs för att [konfigurera en direktuppspelning](../guides/configure-destination-instructions.md) eller ett [filbaserat mål](../guides/configure-file-based-destination-instructions.md) med Destination SDK.
