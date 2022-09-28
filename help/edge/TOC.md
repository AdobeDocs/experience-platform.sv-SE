---
solution: Data Collection
audience: user
user-guide-title: Hjälp för Adobe Experience Platform Web SDK
breadcrumb-title: Web SDK Guide
user-guide-description: Interagera med Experience Cloud via Edge-nätverket.
feature: Web SDK
source-git-commit: d32d23ca26419c1619033924d776be4f112e619a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 12%

---


# Webb-SDK för Adobe Experience Platform {#edge}

* [SDK för plattform](home.md)
* Grundläggande {#fundamentals}
   * [Användningsexempel som stöds](fundamentals/supported-use-cases.md)
   * [Förutsättningar](fundamentals/prerequisite.md)
   * [Installera SDK](fundamentals/installing-the-sdk.md)
   * [Konfigurera SDK](fundamentals/configuring-the-sdk.md)
   * [Kör kommandon](fundamentals/executing-commands.md)
   * [Spåra händelser](fundamentals/tracking-events.md)
   * [Felsökning](fundamentals/debugging.md)
   * [Konfigurera en CSP](fundamentals/configuring-a-csp.md)
   * [Interagera med flera egenskaper](fundamentals/interacting-with-multiple-properties.md)
   * [Klienttips för användaragent](fundamentals/user-agent-client-hints.md)
* Datastreams {#datastreams}
   * [Översikt](./datastreams/overview.md)
   * [Dataförberedelse för datainsamling](./datastreams/data-prep.md)
* Identitet {#identity}
   * [Översikt](identity/overview.md)
   * [Enhets-ID:n från första part](identity/first-party-device-ids.md)
   * [Delning av mobil-till-webb och domänövergripande ID](identity/id-sharing.md)
* Datainsamling {#data-collection}
   * [Automatiskt insamlad information](data-collection/automatic-information.md)
   * [Spåra länkar](data-collection/track-links.md)
   * [Samla in data om handel och produkter](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Använda Adobe Analytics med Platform Web SDK](data-collection/adobe-analytics/analytics-overview.md)
      * [Mappningsanalysvariabler](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Automatiskt mappade variabler](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Skicka data till Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personalisering {#personalization}
   * [Återge personaliserat innehåll](personalization/rendering-personalization-content.md)
   * [Hantera flimmer](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Översikt](personalization/adobe-target/target-overview.md)
      * [Programimplementering på en sida](personalization/adobe-target/spa-implementation.md)
      * [Åtkomst till svarstoken](personalization/adobe-target/accessing-response-tokens.md)
      * [Använda tredje parts-ID i mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Jämföra biblioteket at.js med Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analyser för målloggning (A4T) {#a4t}
         * [Översikt](personalization/adobe-target/analytics-logging/overview.md)
         * [Loggning på klientsidan](personalization/adobe-target/analytics-logging/client-side.md)
         * [Loggning på serversidan](personalization/adobe-target/analytics-logging/server-side.md)
   * offer decisioning {#offer-decisioning}
      * [Översikt](personalization/offer-decisioning/offer-decisioning-overview.md)
* Godkännande {#consent}
   * [Godkännande](consent/supporting-consent.md)
   * IAB Transparency och Consent Framework 2.0 {#iab-tcf}
      * [Översikt](consent/iab-tcf/overview.md)
      * [Integrera med taggar](consent/iab-tcf/with-launch.md)
      * [Integrera utan taggar](consent/iab-tcf/without-launch.md)
* SDK-taggtillägg för webben {#extension}
   * [Web SDK-tillägg](extension/web-sdk-extension-configuration.md)
   * [Händelsetyper](extension/event-types.md)
   * [Åtgärdstyper](extension/action-types.md)
   * [Dataelementtyper](extension/data-element-types.md)
   * [Åtkomst till ECID](extension/accessing-the-ecid.md)
   * [Versionsinformation för Web SDK-tillägg](extension/web-sdk-ext-release-notes.md)
* [Versionsinformation](release-notes.md)
* [Vanliga frågor](web-sdk-faq.md)
* [Resurser](resources.md)
