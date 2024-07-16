---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK ordlista
description: Förstå viktig terminologi när du redigerar ett mål med Experience Platform Destination SDK.
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK ordlista

I den här ordlistan finns definitioner av termer som används i Destination SDK. Andra Adobe Experience Platform-termer finns i [Experience Platform-ordlistan](/help/landing/glossary.md).

## A

**Samlingsprincip**: När du konfigurerar hur data ska exporteras till målet för realtidsdirektuppspelning kan du definiera hur profildata ska samlas in innan de skickas till målplattformen. Detta hjälper till att optimera dataleveransen genom att gruppera dataposter baserat på specifika kriterier, minska antalet API-anrop och förbättra den övergripande effektiviteten. Olika profiler kan konfigureras för att uppfylla olika destinationskrav, vilket säkerställer att data paketeras och levereras på det mest effektiva sättet. [Läs mer](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Konfigurering av målgruppsmetadata**: En målgruppsmetadatakonfiguration refererar till den strukturerade konfigurationen och parametrar som definieras i Adobe Experience Platform och som gör det möjligt att skapa, uppdatera och ta bort målgruppssegment i ett angivet mål. Den här konfigurationen använder målgruppsmetadatamallar för att anpassas till specifikationerna för målplattformens marknadsförings-API. Läs mer om [målgruppens metadatakonfiguration](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) och [tillgängliga makron](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Slutpunkt för målkonfiguration**: En slutpunkt för målkonfiguration i Adobe Experience Platform, särskilt API-slutpunkten `/authoring/destinations`, används för att skapa, hämta, uppdatera och ta bort konfigurationer för mål. Dessa konfigurationer definierar hur data från Adobe Experience Platform levereras till olika externa system eller destinationer, som marknadsföringsplattformar, molnlagringstjänster eller andra slutpunkter för databearbetning. Läs mer om [tillgängliga konfigurationsalternativ](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) och se [referensdokumentationen](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Målinstans**: En specifik konfiguration av en målkonfiguration i Adobe Experience Platform, som skapas och hanteras via användargränssnittet i Experience Platform. Den innehåller alla nödvändiga parametrar och autentiseringsuppgifter för att ansluta och skicka data till målet. När du har upprättat anslutningen till målet kan du hämta målinstans-ID:t när du [bläddrar i en anslutning till målet](/help/destinations/ui/destination-details-page.md).

![Gränssnittsbild för att hämta målinstans-ID](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]mall**: En [!DNL Pebble]-mall används för att omforma data som exporteras från Adobe Experience Platform till det format som krävs för målplattformen. Den använder mallspråket [!DNL Pebble], som möjliggör dynamisk dataomvandling via funktioner som `filter`, `for`, `if` och `set`. Adobe Experience Platform innehåller ytterligare anpassade funktioner som `addedSegments` och `removedSegments`. Med hjälp av mallarna kan dataelement som tidsstämplar och målgruppsmedlemskap formateras så att de uppfyller målgruppens specifikationer. Läs mer [här](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) och [här](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privat mål**: Anpassade integreringar som skapats av enskilda Adobe Experience Platform-kunder. Dessa är skräddarsydda för att uppfylla specifika affärsbehov och är bara tillgängliga inom kundens organisation, vilket ger flexibilitet vid konfigurationer för dataexport. Privata destinationer är endast tillgängliga för Real-Time CDP Ultimate-kunder. [Läs mer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Offentligt mål**: En allmänt tillgänglig integrering i Adobe Experience Platform-katalogen. Dessa destinationer är standardiserade, varumärkesprofilerade och förenklar kundkonfigurationen genom att tillhandahålla förkonfigurerade parametrar. De är tillgängliga för alla kunder som använder Adobe Experience Platform. [Läs mer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Självbetjäningsdokumentationsmall**: Självbetjäningsdokumentationsmallen innehåller ett strukturerat format som du kan använda för att dokumentera målet. Det innehåller avsnitt för en översikt, användningsfall, förutsättningar, identiteter, målgrupper, exporttyper och frekvens samt steg för att ansluta till målet, aktivera målgrupper och mappningsattribut. Använd den här mallen för att få omfattande och konsekvent dokumentation, så att kunderna snabbt kan komma igång med att använda destinationen och förstå de tillhandahållna användningsexemplen. Läs mer om [hur du dokumenterar ditt mål](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [hämtar den senaste dokumentationsmallen för självbetjäning](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip) och [visar hur det återges](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Mallspecifikationer och mallstrategier**: Mallspecifikationer är konfigurationer som används för att formatera HTTP-begäranden som skickas från Adobe Experience Platform till ett mål. De omvandlar profilattributfält från XDM-schemat till ett format som stöds av målplattformen. Om du använder ett mallspråk som liknar [!DNL Jinja] tillåter dessa specifikationer dynamiska dataomformningar baserade på specifika regler och indata. [Läs mer](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Testnings-API**: Med testnings-API kan du validera målkonfigurationerna innan du skickar en publiceringsbegäran. Den innehåller verktyg för att generera exempelprofiler och testa dataflödet, så att konfigurationen matchar målets krav. API:t har stöd för både direktuppspelning och filbaserade (batch-baserade) mål, vilket ger ett sätt att simulera data och felsöka potentiella problem i konfigurationsprocessen. Läs mer om testnings-API:t för [direktuppspelning](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) och [filbaserade mål](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Omformningsmall**: En omformningsmall anpassar dataformatet från Adobe XDM-schemat till målets förväntade format. [Läs mer](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
