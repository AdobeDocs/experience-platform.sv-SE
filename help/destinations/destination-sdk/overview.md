---
description: Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till din slutpunkt eller lagringsplats, baserat på vilka data- och autentiseringsformat du väljer. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster för Experience Platform för att leverera målgrupps- och profildata till din slutpunkt eller lagringsplats, baserat på valfritt data och autentiseringsformat. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.

I dokumentationen till Destinationen SDK finns instruktioner om hur du kan använda Adobe Experience Platform Destinationen SDK för att konfigurera, testa och släppa en produktanpassad målintegration med Adobe Experience Platform, och få destinationen att bli en del av den ständigt växande destinationskatalogen. Genom att använda Destination SDK kan du även skapa ett eget, anpassat privat mål för att exportera data som är anpassade efter dina behov.

![Skärmbild från användargränssnittet i Experience Platform som visar målkatalogen.](assets/destinations-catalog-overview.png)

## Snabbstart - utforska viktig information {#quick-start}

Läs igenom dokumentationen på länkarna nedan för att snabbt komma igång med att konfigurera och skicka ditt mål via Destination SDK.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Konfigurationssidor</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Alla konfigurationsalternativ förklaras</a></li>
                <li> Målserverkonfiguration - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">serverspecifikationer</a> och <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">mallange specifikationer</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Kunddatafält och andra målkonfigurationskomponenter</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Mallar och makron</a></li>
            </ul>
        </td>
        <td>
            <p><b>Användarhandböcker</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Integrationsprocess på hög nivå</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Konfigurera ett mål för direktuppspelning</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Konfigurera ett filbaserat mål</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Konfigurera ett mål för att exportera profiler för potentiella kunder</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Skicka mål för publicering</a></li>
            </ul>
        </td>
                <td>
            <p><b>API-referenser</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">API-referens för målserverns slutpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">API-referens för målslutpunkt</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">API-referens för målgruppsmetadata</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">Testa API-referens</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">API-referens för målpublicering</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Konfigurera ett mål för direktuppspelning - kalkylblad</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Konfigurera en guide för direktuppspelningsmål från början till slut</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Förstå dataomvandling via mallar</a> och <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">visa mallfunktioner som stöds</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Förstå policyer för dataaggregering</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Exempel på Live-konfiguration</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Testa strömningsmålet</a></li>
            </ul>
        </td>
        <td>
            <p><b>Konfigurera ett filbaserat mål - kalkylblad</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Konfigurera en filbaserad målguide från början till slut</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Konfigurera filformat för de exporterade filerna</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Exempel på Live-konfiguration för ett Amazon S3-mål</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Batchkonfiguration</a> för filexportschema och filnamn</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Testa ditt filbaserade mål</a></li>
            </ul>
        </td>
        <td>
            <p><b>Annan viktig information</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Hämta nödvändiga autentiseringsuppgifter för att använda API:t</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Krav för integrering</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Destinationens SDK ordlista</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Klassificeringsgränser och återförsöksprincip</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Självbetjäningsmall för att dokumentera destinationen</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Producerade och anpassade integreringar {#productized-custom-integrations}

>[!IMPORTANT]
>
> Den här funktionen för att skapa privata anpassade destinationer är bara tillgänglig för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder.

Som Destination SDK partner kan du dra nytta av att lägga till din produkterade destination på [Experience Platform-katalog](../catalog/overview.md):

1. Standardisera integrationskonfigurationer mellan kunder med förkonfigurerade parametrar och förenkla konfigurationsupplevelsen för kunderna.
2. Lägg in ett varumärkesprofilerat destinationskort i Experience Platform-katalogen för enklare kundkonfiguration och ökad medvetenhet.
3. Upptäck detta som en produkterad målintegration med Adobe Experience Platform &amp; Adobe Real-time Customer Data Platform.

Som Experience Platform-kund kan du också skapa en egen egen, anpassad destination som passar dina aktiveringsbehov.

![Översiktsdiagram som visar hur målutvecklare interagerar med Destination SDK och hur Real-Time CDP-kunder drar nytta av produktioner och privata destinationer.](assets/destination-sdk-visual.png)

## Integrationstyper som stöds {#supported-integration-types}

### Integrering i realtid (direktuppspelning) {#real-time-integrations}

Genom Destination SDK stöder Adobe Experience Platform realtidsintegrering (kallas även direktuppspelning) med mål som har en REST API-slutpunkt. Realtidsintegreringen med Experience Platform stöder funktioner som:

* Meddelandeomvandling och -aggregering
* Bakfyllning av profil
* Konfigurerbar metadataintegrering för att initiera målgruppsinställningar och dataöverföring
* Konfigurerbar autentisering
* En serie test- och validerings-API:er som du kan använda för att testa och iterera i målkonfigurationerna

### Filbaserade integreringar {#file-based-integrations}

Med Destination SDK kan du även konfigurera integreringar för att regelbundet exportera filer till valfri lagringsplats. Den filbaserade integrationen med Experience Platform stöder funktioner som:

* Filexport i flera format som stöds (CSV, Parquet, JSON)
* Konfigurerbara filformateringsalternativ som gör att du kan strukturera formatet för de exporterade filerna så att de uppfyller dina senare krav.

Läs om de tekniska kraven på destinationssidan i [integrationskrav](integration-prerequisites.md) artikel och läsa om alla konfigurationer som stöds i [konfigurationsalternativ](functionality/configuration-options.md) artikel

## Få tillgång till Destination SDK {#get-access}

Destinationernas SDK åtkomst varierar beroende på din status som partner eller Experience Platform, Real-Time CDP-kund. Se tabellen nedan för mer information.

| Typ av partner eller kund | Åtkomst till Destination SDK |
---------|----------|
| Independent Software Vendor (ISV) | Gå med i [Adobe Technology Partner Program](https://partners.adobe.com/technologyprogram/experiencecloud.html) och begär att få en Experience Platform-sandlåda för att få åtkomst till Destination SDK. |
| Systemintegratör | Du måste vara på antingen Guld- eller Platina-nivå i [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html) för att få en Experience Platform-sandlåda etablerad och tillgång till Destination SDK. |
| Experience Platform kund på [Real-Time CDP Ultimate-paket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Som standard får du tillgång till sandlådor och Destination SDK i Experience Platform, så att du kan skapa privata mål för din organisation. |

{style="table-layout:auto"}

## Högnivåprocess {#process}

Hur du konfigurerar ditt mål i Experience Platform beskrivs nedan:

1. Om du är en ISV eller SI läser du [hämta åtkomst](#get-access) information i avsnittet ovan. [Real-Time CDP Ultimate-paket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder kan hoppa över det här steget.
2. [Begäran om att etablera en Experience Platform-sandlåda](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) och aktivera målredigeringsbehörigheten.
3. Bygg er integration. Följ anvisningarna i produktdokumentationen för att konfigurera [mål för direktuppspelning](guides/configure-destination-instructions.md) eller [filbaserade mål](guides/configure-file-based-destination-instructions.md).
4. Testa integreringen. Följ anvisningarna i produktdokumentationen för att testa [mål för direktuppspelning](testing-api/streaming-destinations/streaming-destination-testing-overview.md) eller [filbaserade mål](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Om du är en ISV- eller SI-utvecklare [produktionsintegrering](./overview.md#productized-custom-integrations), [skicka in integreringen](guides/submit-destination.md) för Adobe granskning (standardsvarstiden är fem arbetsdagar).
6. Om du är en ISV eller SI som skapar en produktiverad integrering använder du [självbetjäningsdokumentationsprocess](docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida på Experience League för destinationen.
7. När integreringen godkänts av Adobe visas den i [Experience Platform-katalog](../catalog/overview.md).
8. Om du vill uppdatera integreringen följer du samma process.

## Referens {#reference}

Adobe rekommenderar att du läser och förstår följande Experience Platform-dokumentation:

* [Översikt över Adobe Experience Platform destinationer](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html)
* [Grundläggande om XDM-schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html)
* [Översikt över namnområde för identitet](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)
