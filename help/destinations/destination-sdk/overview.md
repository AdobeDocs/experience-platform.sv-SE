---
description: Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till din slutpunkt, baserat på valfritt dataformat och autentiseringsformat. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2e2ed880650ad6823b60819e36081540a35ab727
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK

## Översikt {#destinations-sdk}

Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till slutpunkten, baserat på vilka data- och autentiseringsformat du väljer. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.

I dokumentationen till Destinationen SDK finns instruktioner om hur du kan använda Adobe Experience Platform Destinationen SDK för att konfigurera, testa och släppa en produktanpassad målintegration med Adobe Experience Platform, och få destinationen att bli en del av den ständigt växande målkatalogen.

![Översikt över destinationskatalogen](./assets/destinations-catalog-overview.png)

## Producerade och anpassade integreringar {#productized-custom-integrations}

Som Destination SDK partner kan du dra nytta av att lägga till din produkterade destination på [Experience Platform-katalog](/help/destinations/catalog/overview.md):
1. Standardisera integrationskonfigurationer mellan kunder med förkonfigurerade parametrar och förenkla konfigurationsupplevelsen för kunderna.
2. Lägg in ett varumärkesprofilerat destinationskort i Experience Platform-katalogen för enklare kundkonfiguration och ökad medvetenhet.
3. Upptäck detta som en produkterad målintegration med Adobe Experience Platform &amp; Real-time Customer Data Platform.

Som Experience Platform-kund kan du skapa en egen, anpassad destinationsplats som bäst passar dina aktiveringsbehov.

![Destinationens SDK visuella diagram](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Typer av integreringar som stöds {#supported-integration-types}

Genom Destination SDK stöder Adobe Experience Platform realtidsintegrering med mål som har en REST API-slutpunkt. Realtidsintegreringen med Experience Platform stöder funktioner som:
* Meddelandeomvandling och -aggregering
* Bakfyllning av profil
* Konfigurerbar integrering av metadata för att initiera målgruppsinställningar och dataöverföring
* Konfigurerbar autentisering
* En serie test- och validerings-API:er som du kan använda för att testa och iterera i målkonfigurationerna

Läs om de tekniska kraven på destinationssidan i [integrationskrav](./integration-prerequisites.md) artikel.

## Få tillgång till Destination SDK {#get-access}

Destinationernas SDK åtkomst varierar beroende på din status som partner eller Experience Platform, Real-Time CDP-kund. Se tabellen nedan för mer information.


| Typ av partner eller kund | Åtkomst till Destination SDK |
---------|----------|
| Independent Software Vendor (ISV) | Gå med i [Adobe Exchange-programmet](https://partners.adobe.com/exchangeprogram/experiencecloud.html) och begär att få en Experience Platform-sandlåda för att få åtkomst till Destination SDK. |
| Systemintegratör | Du måste vara på antingen Guld- eller Platina-nivå i [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html)och du får en Experience Platform-sandlåda och tillgång till Destination SDK. |
| Experience Platform kund på [Aktiveringspaket](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) eller [Real-Time CDP Ultimate-paket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Som standard får du tillgång till sandlådor och Destination SDK i Experience Platform, så att du kan skapa privata mål för din organisation. |

{style=&quot;table-layout:auto&quot;}

## Högnivåprocess {#process}

Hur du konfigurerar ditt mål i Experience Platform beskrivs nedan:

1. Om du är en ISV eller SI läser du informationen om hur du får åtkomst i avsnittet ovan. [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) kunder kan hoppa över det här steget.
2. [Begäran om att etablera en Experience Platform-sandlåda](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) och aktivera målredigeringsbehörigheten.
3. Bygg er integration. Följ anvisningarna i produktdokumentationen för att konfigurera [mål för direktuppspelning](./configure-destination-instructions.md) eller [filbaserade mål (beta)](./configure-file-based-destination-instructions.md).
4. Testa integreringen. Följ anvisningarna i produktdokumentationen för att testa [mål för direktuppspelning](./test-destination.md) eller [filbaserade mål (beta)](./file-based-destination-testing-overview.md).
5. Om du är en ISV- eller SI-utvecklare [produktionsintegrering](./overview.md#productized-custom-integrations), [skicka in integreringen](./submit-destination.md) för Adobe granskning (standardsvarstiden är fem arbetsdagar).
6. Om du är en ISV eller SI som skapar en produktiverad integrering använder du [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida på Experience League för destinationen.
7. När integreringen godkänts av Adobe visas den i [Experience Platform-katalog](/help/destinations/catalog/overview.md).
8. Om du vill uppdatera integreringen följer du samma process.

## Referens  {#reference}

Adobe rekommenderar att du läser och förstår följande Experience Platform-dokumentation:

* [Översikt över Adobe Experience Platform destinationer](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Grundläggande om XDM-schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Översikt över namnområde för identitet](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
