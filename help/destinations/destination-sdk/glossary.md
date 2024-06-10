---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK ordlista
description: Förstå viktig terminologi när du redigerar ett mål med Experience Platform Destination SDK.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# Adobe Experience Platform Destination SDK ordlista

I den här ordlistan finns definitioner av termer som används i Destination SDK. Andra Adobe Experience Platform-termer finns i [Experience Platform ordlista](/help/landing/glossary.md).

## A

**Samlingsprincip**: När du konfigurerar hur data ska exporteras till målet för direktuppspelning i realtid kan du definiera hur profildata ska aggregeras innan de skickas till målplattformen. Detta hjälper till att optimera dataleveransen genom att gruppera dataposter baserat på specifika kriterier, minska antalet API-anrop och förbättra den övergripande effektiviteten. Olika profiler kan konfigureras för att uppfylla olika destinationskrav, vilket säkerställer att data paketeras och levereras på det mest effektiva sättet. [Läs mer](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Konfiguration av målgruppsmetadata**: En målgruppsmetadatakonfiguration avser den strukturerade konfigurationen och de parametrar som definieras i Adobe Experience Platform och som gör det möjligt att skapa, uppdatera och ta bort målgruppssegment i ett visst mål. Den här konfigurationen använder målgruppsmetadatamallar för att anpassas till specifikationerna för målplattformens marknadsförings-API. Läs mer om [konfiguration av målets metadata](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) och [tillgängliga makron](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Slutpunkt för målkonfiguration**: En slutpunkt för målkonfiguration i Adobe Experience Platform, särskilt `/authoring/destinations` API-slutpunkt används för att skapa, hämta, uppdatera och ta bort konfigurationer för mål. Dessa konfigurationer definierar hur data från Adobe Experience Platform levereras till olika externa system eller destinationer, som marknadsföringsplattformar, molnlagringstjänster eller andra slutpunkter för databearbetning. Läs mer om [tillgängliga konfigurationsalternativ](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) och visa [referensdokumentation](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Målinstans**: En specifik konfiguration av en destinationskonfiguration i Adobe Experience Platform som skapas och hanteras via användargränssnittet i Experience Platform. Den innehåller alla nödvändiga parametrar och autentiseringsuppgifter för att ansluta och skicka data till målet. När du har upprättat anslutningen till målet kan du hämta målförekomstens ID när [bläddra genom en anslutning till destinationen](/help/destinations/ui/destination-details-page.md).

![Användargränssnittsbild för att hämta målinstans-ID](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]mall**: A [!DNL Pebble] -mallen används för att omforma data som exporteras från Adobe Experience Platform till det format som krävs för målplattformen. Den använder [!DNL Pebble] mallspråk, som möjliggör dynamisk dataomvandling via funktioner som `filter`, `for`, `if`och `set`. Adobe Experience Platform innehåller andra anpassade funktioner som `addedSegments` och `removedSegments`. Med hjälp av mallarna kan dataelement som tidsstämplar och målgruppsmedlemskap formateras så att de uppfyller målgruppens specifikationer. Läs mer [här](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) och [här](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privat destination**: Anpassade integreringar som skapats av enskilda Adobe Experience Platform-kunder. Dessa är skräddarsydda för att uppfylla specifika affärsbehov och är bara tillgängliga inom kundens organisation, vilket ger flexibilitet vid konfigurationer för dataexport. Privata destinationer är endast tillgängliga för Real-Time CDP Ultimate-kunder. [Läs mer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Offentlig destination**: En allmänt tillgänglig integrering i Adobe Experience Platform-katalogen. Dessa destinationer är standardiserade, varumärkesprofilerade och förenklar kundkonfigurationen genom att tillhandahålla förkonfigurerade parametrar. De är tillgängliga för alla kunder som använder Adobe Experience Platform. [Läs mer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Självbetjäningsdokumentationsmall**: Dokumentationsmallen för självbetjäning innehåller ett strukturerat format som du kan använda för att dokumentera målet. Det innehåller avsnitt för en översikt, användningsfall, förutsättningar, identiteter, målgrupper, exporttyper och frekvens samt steg för att ansluta till målet, aktivera målgrupper och mappningsattribut. Använd den här mallen för att få omfattande och konsekvent dokumentation, så att kunderna snabbt kan komma igång med att använda destinationen och förstå de tillhandahållna användningsexemplen. Läs mer om [dokumentera destinationen](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [ladda ned den senaste självbetjäningsdokumentationsmallen](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip)och [visa hur den renderar](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Mallspecifikationer och mallstrategier**: Mallspecifikationer är konfigurationer som används för att formatera HTTP-begäranden som skickas från Adobe Experience Platform till ett mål. De omvandlar profilattributfält från XDM-schemat till ett format som stöds av målplattformen. Använda ett mallspråk som liknar [!DNL Jinja]möjliggör dessa specifikationer dynamiska dataomvandlingar baserade på specifika regler och indata. [Läs mer](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Testar API**: Med testnings-API kan du validera målkonfigurationerna innan du skickar in en publiceringsbegäran. Den innehåller verktyg för att generera exempelprofiler och testa dataflödet, så att konfigurationen matchar målets krav. API:t har stöd för både direktuppspelning och filbaserade (batch-baserade) mål, vilket ger ett sätt att simulera data och felsöka potentiella problem i konfigurationsprocessen. Läs mer om testnings-API:t för [direktuppspelning](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) och [filbaserade mål](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Omformningsmall**: En omformningsmall anpassar dataformatet från Adobe XDM-schemat till målets förväntade format. [Läs mer](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).