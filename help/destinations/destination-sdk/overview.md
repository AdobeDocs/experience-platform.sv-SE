---
description: Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till slutpunkten, baserat på valfritt data och autentiseringsformat. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK

## Översikt {#destinations-sdk}

Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till slutpunkten, baserat på vilka data- och autentiseringsformat du väljer. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.

I dokumentationen för mål-SDK finns anvisningar om hur du använder Adobe Experience Platform SDK för destinationer för att konfigurera, testa och frisläppa en produkterad målintegrering med Adobe Experience Platform, och om du vill att destinationen ska ingå i den ständigt växande målkatalogen.

![Översikt över destinationskatalogen](./assets/destinations-catalog-overview.png)

## Producerade och anpassade integreringar {#productized-custom-integrations}

Som SDK-målpartner kan du dra nytta av att lägga till det producerade målet i [Experience Platform-katalogen](/help/destinations/catalog/overview.md):
1. Standardisera integrationskonfigurationer mellan kunder med förkonfigurerade parametrar och förenkla konfigurationsupplevelsen för kunderna.
2. Lägg in ett varumärkesprofilerat destinationskort i Experience Platform-katalogen för enklare kundkonfiguration och ökad medvetenhet.
3. Bli en produktionsintegrerad målserver med Adobe Experience Platform &amp; Customer Data Platform i realtid.

Som Experience Platform-kund kan du skapa en egen, anpassad destinationsplats som bäst passar dina aktiveringsbehov.

![SDK-målets visuella diagram](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Typer av integreringar som stöds {#supported-integration-types}

Genom mål-SDK stöder Adobe Experience Platform realtidsintegreringar med mål som har en REST API-slutpunkt. Realtidsintegreringen med Experience Platform stöder funktioner som:
* Meddelandeomvandling och -aggregering
* Bakfyllning av profil
* Konfigurerbar integrering av metadata för att initiera målgruppsinställningar och dataöverföring
* Konfigurerbar autentisering
* En serie test- och validerings-API:er som du kan använda för att testa och iterera i målkonfigurationerna

Läs om de tekniska kraven på målsidan i [integrationskraven](./integration-prerequisites.md)-artikeln.


## Få åtkomst till mål-SDK {#get-access}

SDK-målåtkomsten varierar beroende på din status som partner eller Experience Platform-kund. Se tabellen nedan för mer information.


| Typ av partner eller kund | Åtkomst till mål-SDK |
---------|----------|
| Independent Software Vendor (ISV) | Gå med i [Adobe Exchange-programmet](https://partners.adobe.com/exchangeprogram/experiencecloud.html) och begär att få en Experience Platform-sandlåda för åtkomst till mål-SDK. |
| Systemintegratör | Du måste vara på antingen Guld- eller Platina-nivå i [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html), och du får en Experience Platform-sandlåda och tillgång till mål-SDK. |
| Experience Platform kund i aktiveringspaketet | Som standard får du åtkomst till sandlådor i Experience Platform och mål-SDK. |
| Experience Platform kund i CDP-paketet i realtid | Du har inte åtkomst till mål-SDK, men du har tillgång till alla produktioner som konfigurerats av andra företag med SDK för mål och som publicerats i olika Experience Platform-organisationer. |

{style=&quot;table-layout:auto&quot;}

## Högnivåprocess {#process}

Hur du konfigurerar ditt mål i Experience Platform beskrivs nedan:

1. Om du är en ISV eller SI läser du informationen om hur du får åtkomst i avsnittet ovan. [Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activationcustomers kan hoppa över det här steget.
2. [Begär att en ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) sandlåda för Experience Platform ska etableras och att målredigeringsbehörigheten ska aktiveras.
3. [Bygg ](./configure-destination-instructions.md) integreringen i produktdokumentationen.
4. [Testa ](./test-destination.md) integreringen i produktdokumentationen.
5. [Skicka in ](./destination-publish-api.md) integreringen för granskning från Adobe (standardsvarstiden är 5 arbetsdagar).
6. Om du är en ISV- eller SI-leverantör och skapar en [produktiserad integrering](./overview.md#productized-custom-integrations) använder du [självbetjäningsdokumentationsprocessen](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida på Experience League för destinationen.
7. När den har godkänts av Adobe visas din integrering i [Experience Platform-katalogen](/help/destinations/catalog/overview.md).
8. Om du vill uppdatera integreringen följer du samma process.

## Referens  {#reference}

Adobe rekommenderar att du läser och förstår följande Experience Platform-dokumentation:

* [Översikt över Adobe Experience Platform destinationer](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Grundläggande om XDM-schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Översikt över namnområde för identitet](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
