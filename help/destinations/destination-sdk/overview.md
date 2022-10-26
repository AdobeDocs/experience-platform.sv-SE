---
description: Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till din slutpunkt eller lagringsplats, baserat på vilka data- och autentiseringsformat du väljer. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK

## Översikt {#destinations-sdk}

Adobe Experience Platform Destination SDK är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster för Experience Platform för att leverera målgrupps- och profildata till din slutpunkt eller lagringsplats, baserat på valfritt data och autentiseringsformat. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar.

I dokumentationen till Destinationen SDK finns instruktioner om hur du kan använda Adobe Experience Platform Destinationen SDK för att konfigurera, testa och släppa en produktanpassad målintegration med Adobe Experience Platform, och få destinationen att bli en del av den ständigt växande målkatalogen. Genom att använda Destination SDK kan du även skapa ett eget, anpassat privat mål för att exportera data som är anpassade efter dina behov.

![Skärmbild från användargränssnittet i Experience Platform som visar destinationskatalogen](./assets/destinations-catalog-overview.png)

## Producerade och anpassade integreringar {#productized-custom-integrations}

>[!IMPORTANT]
>
> Den här funktionen för att skapa privata anpassade destinationer är bara tillgänglig för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder.

Som Destination SDK partner kan du dra nytta av att lägga till din produkterade destination på [Experience Platform-katalog](/help/destinations/catalog/overview.md):
1. Standardisera integrationskonfigurationer mellan kunder med förkonfigurerade parametrar och förenkla konfigurationsupplevelsen för kunderna.
2. Lägg in ett varumärkesprofilerat destinationskort i Experience Platform-katalogen för enklare kundkonfiguration och ökad medvetenhet.
3. Upptäck detta som en produkterad målintegration med Adobe Experience Platform &amp; Adobe Real-time Customer Data Platform.

Som Experience Platform-kund kan du också skapa en egen, anpassad destinationsplats som bäst passar dina aktiveringsbehov.

![Ett översiktsdiagram som visar hur målutvecklare interagerar med Destination SDK och hur Real-Time CDP-kunder drar nytta av produktioner och privata destinationer.](./assets/destination-sdk-visual.png)

## Typer av integreringar som stöds {#supported-integration-types}

Genom Destination SDK stöder Adobe Experience Platform realtidsintegrering med mål som har en REST API-slutpunkt. Realtidsintegreringen med Experience Platform stöder funktioner som:
* Meddelandeomvandling och -aggregering
* Bakfyllning av profil
* Konfigurerbar integrering av metadata för att initiera målgruppsinställningar och dataöverföring
* Konfigurerbar autentisering
* En serie test- och validerings-API:er som du kan använda för att testa och iterera i målkonfigurationerna

Med Destination SDK kan du även konfigurera integreringar för att regelbundet exportera filer till valfri lagringsplats. Realtidsintegreringen med Experience Platform stöder funktioner som:
* Filexport i flera format som stöds (CSV, Parquet, JSON)
* Konfigurerbara filformateringsalternativ som gör att du kan strukturera formatet för de exporterade filerna så att de uppfyller dina krav längre fram i kedjan.

Läs om de tekniska kraven på destinationssidan i [integrationskrav](./integration-prerequisites.md) artikel.

## Få tillgång till Destination SDK {#get-access}

Destinationernas SDK åtkomst varierar beroende på din status som partner eller Experience Platform, Real-Time CDP-kund. Se tabellen nedan för mer information.


| Typ av partner eller kund | Åtkomst till Destination SDK |
---------|----------|
| Independent Software Vendor (ISV) | Gå med i [Adobe Exchange-programmet](https://partners.adobe.com/exchangeprogram/experiencecloud.html) och begär att få en Experience Platform-sandlåda för att få åtkomst till Destination SDK. |
| Systemintegratör | Du måste vara på antingen Guld- eller Platina-nivå i [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html)och du får en Experience Platform-sandlåda och tillgång till Destination SDK. |
| Experience Platform kund på [Real-Time CDP Ultimate-paket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Som standard får du tillgång till sandlådor och Destination SDK i Experience Platform, så att du kan skapa privata mål för din organisation. |

{style=&quot;table-layout:auto&quot;}

## Högnivåprocess {#process}

Hur du konfigurerar ditt mål i Experience Platform beskrivs nedan:

1. Om du är en ISV eller SI läser du informationen om hur du får åtkomst i avsnittet ovan. [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) kunder kan hoppa över det här steget.
2. [Begäran om att etablera en Experience Platform-sandlåda](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) och aktivera målredigeringsbehörigheten.
3. Bygg er integration. Följ anvisningarna i produktdokumentationen för att konfigurera [mål för direktuppspelning](./configure-destination-instructions.md) eller [filbaserade mål](./configure-file-based-destination-instructions.md).
4. Testa integreringen. Följ anvisningarna i produktdokumentationen för att testa [mål för direktuppspelning](./test-destination.md) eller [filbaserade mål](./file-based-destination-testing-overview.md).
5. Om du är en ISV- eller SI-utvecklare [produktionsintegrering](./overview.md#productized-custom-integrations), [skicka in integreringen](./submit-destination.md) för Adobe granskning (standardsvarstiden är fem arbetsdagar).
6. Om du är en ISV eller SI som skapar en produktiverad integrering använder du [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida på Experience League för destinationen.
7. När integreringen godkänts av Adobe visas den i [Experience Platform-katalog](/help/destinations/catalog/overview.md).
8. Om du vill uppdatera integreringen följer du samma process.

## Referens  {#reference}

Adobe rekommenderar att du läser och förstår följande Experience Platform-dokumentation:

* [Översikt över Adobe Experience Platform destinationer](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Grundläggande om XDM-schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Översikt över namnområde för identitet](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
