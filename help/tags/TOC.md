---
audience: user
user-guide-title: Hjälp med taggar
breadcrumb-title: Taggar
user-guide-description: Lär dig att driftsätta och hantera analyser, marknadsföring och annonstaggar för att förbättra kundupplevelser.
feature: Tags
solution: Data Collection
role: Developer
source-git-commit: 3bd3ef14cd0bd2c079c1c881a70865b067f28341
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 18%

---


# Taggar {#tags}

* [Översikt över taggar](./home.md)
* Komma igång {#get-started}
   * [Snabbstartguide](./quick-start/quick-start.md)
   * [Implementeringsguider](./quick-start/implementation-guides.md)
* Användargränssnittsguider {#ui}
   * [Översikt](./ui/managing-resources/overview.md)
   * Tillägg {#extensions}
      * [Översikt](./ui/managing-resources/extensions/overview.md)
      * [Tillägg - uppgraderingar](./ui/managing-resources/extensions/extension-upgrade.md)
   * [Dataelement](./ui/managing-resources/data-elements.md)
   * [Regler](./ui/managing-resources/rules.md)
   * [Anteckningar](./ui/managing-resources/notes.md)
   * [Kopiera resurser](./ui/managing-resources/copying-resources.md)
   * [Jämför resursrevisioner](./ui/managing-resources/compare-resource-revisions.md)
   * [Ta bort resurser](./ui/managing-resources/delete-resources.md)
   * [Ta bort resurser från ett bibliotek](./ui/managing-resources/remove-resources-from-library.md)
* Publicering {#publish}
   * [Översikt](./ui/publishing/overview.md)
   * [Publiceringsflöde](./ui/publishing/publishing-flow.md)
   * Värdar {#hosts}
      * [Översikt](./ui/publishing/hosts/hosts-overview.md)
      * [Adobe-hanterade värdar](./ui/publishing/hosts/managed-by-adobe-host.md)
      * [SFTP-värdar](./ui/publishing/hosts/sftp-host.md)
   * Miljöer {#environments}
      * [Översikt](./ui/publishing/environments.md)
      * [Testa inbäddningskoder med Adobe Experience Platform Debugger](./ui/publishing/embed-code-testing.md)
   * [Bygger](./ui/publishing/builds.md)
   * [Bibliotek](./ui/publishing/libraries.md)
   * [Självvärdande bibliotek](./ui/publishing/hosts/self-hosting-libraries.md)
   * [Publicera om ett bibliotek](./ui/publishing/republish.md)
   * [Experience Platform-taggar (Kina)](./ui/publishing/premium-cdn.md)
* Information på klientsidan {#client-side}
   * [Översikt](./ui/client-side/overview.md)
   * [Asynkron distribution](./ui/client-side/asynchronous-deployment.md)
   * [Satellitobjektreferens](./ui/client-side/satellite-object.md)
   * [Distribuera JavaScript-taggar för att hantera kundgodkännande](./ui/client-side/consent.md)
   * [Stöd för CSP (Content Security Policy)](./ui/client-side/content-security-policy.md)
   * [Stöd för SRI (Subresource Integrity)](./ui/client-side/sri.md)
   * [Säkerhet för transportlager](./ui/client-side/transport-layer-security.md)
* Vidarebefordran av händelser {#event-forwarding}
   * [Översikt](./ui/event-forwarding/overview.md)
   * [Komma igång](./ui/event-forwarding/getting-started.md)
   * [Konfigurera hemligheter](./ui/event-forwarding/secrets.md)
   * [Övervakning (Beta)](./ui/event-forwarding/monitoring.md)
* Administrering {#admin}
   * [Översikt](./ui/administration/overview.md)
   * [Företag och fastigheter](./ui/administration/companies-and-properties.md)
   * [Användarbehörigheter](./ui/administration/user-permissions.md)
* Tillägg {#extensions}
   * [Översikt](./extensions/overview.md)
   * Taggtillägg (klientsidan) {#client}
      * [Översikt](./extensions/client/overview.md)
      * [Tillgängliga hastighetsmått för webbplats](https://exchange.adobe.com/apps/ec/103053)
      * [Activity Map Customizer](https://exchange.adobe.com/apps/ec/101531)
      * [Uppdatera åtgärdssida](https://exchange.adobe.com/apps/ec/102848)
      * [Anpassa webbplatsspårning](https://exchange.adobe.com/apps/ec/103195)
      * [Adobe Advertising Cloud](https://exchange.adobe.com/apps/ec/100155)
      * Adobe Analytics {#analytics}
         * [Översikt](./extensions/client/analytics/overview.md)
         * [Delade moduler](./extensions/client/analytics/shared-modules.md)
         * [Versionsinformation](./extensions/client/analytics/release-notes.md)
      * [Adobe Analytics &amp; Adobe Target](https://exchange.adobe.com/apps/ec/105363/6sense-for-analytics-and-target)
      * [Adobe Analytics &amp; Microsoft Dynamics](https://exchange.adobe.com/apps/ec/102966)
      * [Adobe Analytics &amp; Salesforce](https://exchange.adobe.com/apps/ec/101530)
      * Adobe Analytics produktsträng {#product-string}
         * [Översikt](./extensions/client/product-string/overview.md)
         * [Versionsinformation](./extensions/client/product-string/release-notes.md)
      * [Adobe Analytics Product String Builder](https://exchange.adobe.com/apps/ec/101461)
      * [Adobe Analytics via Adobe Experience Platform Web SDK](https://exchange.adobe.com/apps/ec/108985/search-discovery-for-adobe-analytics-via-aep-web-sdk)
      * Adobe Audience Manager {#audience-manager}
         * [Översikt](./extensions/client/audience-manager/overview.md)
      * Adobe Client Data Layer {#client-data-layer}
         * [Översikt](./extensions/client/client-data-layer/overview.md)
         * [Versionsinformation](./extensions/client/client-data-layer/release-notes.md)
      * Adobe Content Analytics {#content-analytics}
         * [Översikt](./extensions/client/content-analytics/overview.md)
      * Adobe ContextHub {#contexthub}
         * [Översikt](./extensions/client/contexthub/overview.md)
      * [Adobe Experience Manager Forms](https://exchange.adobe.com/apps/ec/107493)
      * Adobe Experience Cloud ID-tjänst {#id-service}
         * [Översikt](./extensions/client/id-service/overview.md)
         * [Versionsinformation](./extensions/client/id-service/release-notes.md)
      * Adobe Experience Platform Demo {#platform-demo}
         * [Översikt](./extensions/client/platform-demo/overview.md)
      * Webb-SDK för Adobe Experience Platform {#web-sdk}
         * [Översikt](./extensions/client/web-sdk/overview.md)
         * [Konfigurera SDK-taggtillägget för webben](./extensions/client/web-sdk/web-sdk-extension-configuration.md)
         * [Händelsetyper](./extensions/client/web-sdk/event-types.md)
         * [Åtgärdstyper](./extensions/client/web-sdk/action-types.md)
         * [Dataelementtyper](./extensions/client/web-sdk/data-element-types.md)
         * [Åtkomst till ECID](./extensions/client/web-sdk/accessing-the-ecid.md)
         * [SDK-plugins för webben](./extensions/client/web-sdk/web-sdk-plugins.md)
         * [Versionsinformation om SDK-tillägg](./extensions/client/web-sdk/web-sdk-ext-release-notes.md)
         * [Versionsinformation om SDK-plugin-program för webben](./extensions/client/web-sdk/web-sdk-plugins-release-notes.md)
      * Adobe Experience Manager resursinsikter {#asset-insights}
         * [Översikt](./extensions/client/asset-insights/overview.md)
         * [Versionsinformation](./extensions/client/asset-insights/release-notes.md)
      * [Adobe Fonts](https://exchange.adobe.com/apps/ec/101538)
      * Adobe Media Analytics för ljud och video {#media-analytics}
         * [Översikt](./extensions/client/media-analytics/overview.md)
         * [Versionsinformation](./extensions/client/media-analytics/release-notes.md)
      * Adobe Media Analytics (3.x SDK) {#media-analytics-3x}
         * [Översikt](./extensions/client/media-analytics-3x/overview.md)
         * [Versionsinformation](./extensions/client/media-analytics-3x/release-notes.md)
      * Adobe Integritet {#privacy}
         * [Översikt](./extensions/client/privacy/overview.md)
      * [Adobe Report Suite-väljare](https://exchange.adobe.com/apps/ec/100640)
      * Adobe Target {#target}
         * [Översikt](./extensions/client/target/overview.md)
         * [Versionsinformation](./extensions/client/target/release-notes.md)
      * Adobe Target v2 {#target-v2}
         * [Översikt](./extensions/client/target-v2/overview.md)
         * [Versionsinformation](./extensions/client/target-v2/release-notes.md)
      * [Adobe Target Toolkit](https://exchange.adobe.com/apps/ec/100640)
      * [Advertising Cloud](https://exchange.adobe.com/apps/ec/100640)
      * [AEM-resursinsikter](https://exchange.adobe.com/apps/ec/103406)
      * [Airbroms-JS-aviserare](https://exchange.adobe.com/apps/ec/103342)
      * [Amplitud](https://exchange.adobe.com/apps/ec/108010)
      * [Apollo QAX](https://exchange.adobe.com/apps/ec/105068)
      * [Awin Advertiser MasterTag](https://exchange.adobe.com/apps/ec/103176)
      * [Awin-konverteringstagg](https://exchange.adobe.com/apps/ec/103240)
      * [Beemray Human Context](https://exchange.adobe.com/apps/ec/101063)
      * [Bing lägger till universell händelsespårning](https://exchange.adobe.com/apps/ec/100154)
      * [Förgrening](https://exchange.adobe.com/apps/ec/101382)
      * [!DNL BrightCove] videospårning {#brightcove}
         * [Översikt](./extensions/client/brightcove/overview.md)
         * [Versionsinformation](./extensions/client/brightcove/release-notes.md)
      * [CallTrackingMetrics](https://exchange.adobe.com/apps/ec/107695)
      * [Kanal-Source-identifierare](https://exchange.adobe.com/apps/ec/101412)
      * [Cheetah Experiences](https://exchange.adobe.com/apps/ec/102759)
      * [Klickbar](https://exchange.adobe.com/apps/ec/100082)
      * Plugin-program för vanlig analys {#plugins}
         * [Översikt](./extensions/client/plugins/overview.md)
         * [Versionsinformation](./extensions/client/plugins/release-notes.md)
      * [Koncat](https://exchange.adobe.com/apps/ec/104690)
      * [ContentSquare](https://exchange.adobe.com/apps/ec/100364)
      * [Hantering av cookie-samtycke av Usercentrics CMP v2](https://exchange.adobe.com/apps/ec/107037)
      * Core {#core}
         * [Översikt](./extensions/client/core/overview.md)
         * [Versionsinformation](./extensions/client/core/release-notes.md)
      * [Anpassad felsökningsloggare](https://exchange.adobe.com/apps/ec/104698)
      * [Kundigenkänning](https://exchange.adobe.com/apps/ec/100688)
      * [Dataelementassistenten (DEA)](https://exchange.adobe.com/apps/ec/101413)
      * [Datalagerhanteraren](https://exchange.adobe.com/apps/ec/101462)
      * [Decibel](https://exchange.adobe.com/apps/ec/100913)
      * [Demandbase](https://exchange.adobe.com/apps/ec/101605)
      * [Differentiell sekretess](https://exchange.adobe.com/apps/ec/104535)
      * [Dynamiska mediavisare](https://exchange.adobe.com/apps/ec/103048)
      * [EDDL-hjälp](https://exchange.adobe.com/apps/ec/107691)
      * [Flashtalk OneTag](https://exchange.adobe.com/apps/ec/101392)
      * [ForeSee](https://exchange.adobe.com/apps/ec/100164)
      * [Gainsight PX](https://exchange.adobe.com/apps/ec/103343)
      * [Förutsägande av genesys](https://exchange.adobe.com/apps/ec/106148)
      * Google datalager {#google-data-layer}
         * [Översikt](./extensions/client/google-data-layer/overview.md)
         * [Versionsinformation](./extensions/client/google-data-layer/release-notes.md)
      * [Google Global Site Tag (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)
      * [InMoment](https://exchange.adobe.com/apps/ec/100847)
      * [JSON-hjälp](https://exchange.adobe.com/apps/ec/106449)
      * [JW Player Analytics](https://exchange.adobe.com/apps/ec/101523)
      * [KickFire](https://exchange.adobe.com/apps/ec/101621)
      * [Mappningstabell](https://exchange.adobe.com/apps/ec/103136)
      * [!DNL Marketo Munchkin] {#marketo}
         * [Översikt](./extensions/client/marketo/overview.md)
         * [Versionsinformation](./extensions/client/marketo/release-notes.md)
      * [Huvudegenskapshanteraren](https://exchange.adobe.com/apps/ec/102992)
      * [Merkury-tagg](https://exchange.adobe.com/apps/ec/600027/merkury-tag)
      * [!DNL Meta Pixel] {#meta}
         * [Översikt](./extensions/client/meta/overview.md)
      * [Monita](https://exchange.adobe.com/apps/ec/106544)
      * [Nielsen Digital SDK](https://exchange.adobe.com/apps/ec/101361)
      * [OneTrust-hantering för cookies](https://exchange.adobe.com/apps/ec/100340)
      * [Pepperjam](https://exchange.adobe.com/apps/ec/103587)
      * [Persado Connect](https://exchange.adobe.com/apps/ec/103745)
      * [Pinterest Conversion Tracking](https://exchange.adobe.com/apps/ec/100523)
      * [Pixelinläsare](https://exchange.adobe.com/apps/ec/100152)
      * [Frågor och svar om webbplatsen](https://exchange.adobe.com/apps/ec/101569)
      * [Kvantmått](https://exchange.adobe.com/apps/ec/101535)
      * [Lös kortskrift](https://exchange.adobe.com/apps/ec/108352)
      * [Rokt](https://exchange.adobe.com/apps/ec/107591)
      * [SDI-undersökning](https://exchange.adobe.com/apps/ec/102991)
      * [SDI Toolkit](https://exchange.adobe.com/apps/ec/101460)
      * [SessionCam](https://exchange.adobe.com/apps/ec/100517)
      * [Lagringsspanner](https://exchange.adobe.com/apps/ec/102990)
      * [TAGGAR efter loop-Horisont](https://exchange.adobe.com/apps/ec/106092)
      * [Tealium-samling](https://exchange.adobe.com/apps/ec/104217)
      * [Tealium Data Enrichment](https://exchange.adobe.com/apps/ec/104217)
      * [TMMData Foundation-plattform](https://exchange.adobe.com/apps/ec/100148)
      * [TrustArc Cookie Consent Manager](https://exchange.adobe.com/apps/ec/107037)
      * [Vimeo Playback](https://exchange.adobe.com/apps/ec/108937)
      * [Webbsäkra](https://exchange.adobe.com/apps/ec/106769)
      * [XDM-disposition](https://exchange.adobe.com/apps/ec/106062)
      * [ÅttaKonverteringsspårning](https://exchange.adobe.com/apps/ec/103174)
      * [[!DNL Youtube] Uppspelning](https://exchange.adobe.com/apps/ec/104160)
      * [!DNL YouTube] videospårning {#youtube}
         * [Översikt](./extensions/client/youtube/overview.md)
         * [Versionsinformation](./extensions/client/youtube/release-notes.md)
   * Tillägg för vidarebefordran av händelser (på serversidan) {#server}
      * [Översikt](./extensions/server/overview.md)
      * Adobe Experience Platform Cloud Connector {#cloud-connector}
         * [Översikt](./extensions/server/cloud-connector/overview.md)
         * [Versionsinformation](./extensions/server/cloud-connector/release-notes.md)
      * [!DNL Adform] {#adform}
         * [Översikt](./extensions/server/adform/overview.md)
      * [!DNL Amazon] {#amazon}
         * [Översikt](./extensions/server/amazon/overview.md)
      * [!DNL AWS] {#aws}
         * [Översikt](./extensions/server/aws/overview.md)
      * [!DNL Braze] {#braze}
         * [Översikt](./extensions/server/braze/overview.md)
      * [Cloud Connector för Google Analytics](https://exchange.adobe.com/apps/ec/106542)
      * Core {#core}
         * [Översikt](./extensions/server/core/overview.md)
      * [Epsilon-händelse-API](https://exchange.adobe.com/apps/ec/109127)
      * Google Ads Enhanced Conversions {#google-ads-enhanced-conversions}
         * [Översikt](./extensions/server/google-ads-enhanced-conversions/overview.md)
      * Google Cloud Platform {#google-cloud-platform}
         * [Översikt](./extensions/server/google-cloud-platform/overview.md)
      * [!DNL LinkedIn Conversions API] {#linkedin}
         * [Översikt](./extensions/server/linkedin/overview.md)
      * [!DNL Mailchimp] Edge {#mailchimp}
         * [Översikt](./extensions/server/mailchimp/overview.md)
      * [!DNL Meta Conversions API] {#meta}
         * [Översikt](./extensions/server/meta/overview.md)
      * [!DNL Microsoft Azure] {#azure}
         * [Översikt](./extensions/server/azure/overview.md)
      * [!DNL Mixpanel] {#mixpanel}
         * [Översikt](./extensions/server/mixpanel/overview.md)
      * [Pega Customer Decision Hub](https://exchange.adobe.com/apps/ec/107597)
      * [!DNL Pinterest] {#pinterest}
         * [Översikt](./extensions/server/pinterest/overview.md)
      * [!DNL Snapchat] {#snap}
         * [Översikt](./extensions/server/snap/overview.md)
      * [!DNL Snowflake] {#snowflake}
         * [Översikt](./extensions/server/snowflake/overview.md)
      * [!DNL Splunk] {#splunk}
         * [Översikt](./extensions/server/splunk/overview.md)
      * [!DNL Twitter] {#twitter}
         * [Översikt](./extensions/server/twitter/overview.md)
      * Webbhändelse-API för [!DNL Tiktok] {#tiktok}
         * [Översikt](./extensions/server/tiktok/overview.md)
      * [!DNL The Trade Desk] {#thetradedesk}
         * [Översikt](./extensions/server/tradedesk/overview.md)
      * [!DNL Zendesk]-händelse-API {#zendesk}
         * [Översikt](./extensions/server/zendesk/overview.md)
* Tilläggsutveckling {#extension-dev}
   * [Översikt](./extension-dev/overview.md)
   * [Komma igång](./extension-dev/getting-started.md)
   * [Webbläsare som stöds](./extension-dev/browsers.md)
   * Inlämningsprocess {#submit}
      * [Översikt](./extension-dev/submit/overview.md)
      * [Organisationsinställningar](./extension-dev/submit/setup.md)
      * [Bevilja användaråtkomst](./extension-dev/submit/access.md)
      * [Utveckla ett tillägg](./extension-dev/submit/develop.md)
      * [Skapa en börslista](./extension-dev/submit/create-listing.md)
      * [Skapa en ZIP-fil för tilläggspaket](./extension-dev/submit/create-extension-package-zip.md)
      * [Ladda upp och implementera testning från början till slut](./extension-dev/submit/upload-and-test.md)
      * [Frigöra ett tillägg](./extension-dev/submit/release.md)
   * [Tilläggskonfiguration](./extension-dev/configuration.md)
   * [Extension manifest](./extension-dev/manifest.md)
   * Webbtillägg {#web}
      * [Tilläggsflöde](./extension-dev/web/flow.md)
      * [Biblioteksmodulens format](./extension-dev/web/format.md)
      * [Vyer](./extension-dev/web/views.md)
      * [Händelsetyper](./extension-dev/web/event-types.md)
      * [Villkorstyper](./extension-dev/web/condition-types.md)
      * [Åtgärdstyper](./extension-dev/web/action-types.md)
      * [Dataelementtyper](./extension-dev/web/data-element-types.md)
      * [Kärnmoduler](./extension-dev/web/core.md)
      * [Delade moduler](./extension-dev/web/shared.md)
   * Edge-tillägg {#edge}
      * [Tilläggsflöde](./extension-dev/edge/flow.md)
      * [Biblioteksmodulens format](./extension-dev/edge/format.md)
      * [Villkorstyper](./extension-dev/edge/condition-types.md)
      * [Åtgärdstyper](./extension-dev/edge/action-types.md)
      * [Dataelementtyper](./extension-dev/edge/data-element-types.md)
      * [Kontextparameter](./extension-dev/edge/context.md)
   * [Värdar för bibliotek från tredje part](./extension-dev/third-party-libraries.md)
   * [Turbinfri variabel](./extension-dev/turbine.md)
   * [Bakåtkompatibilitetsstandard](./extension-dev/backwards-compatibility.md)
* Reactor API {#api}
   * [Översikt](./api/overview.md)
   * [Autentisera och få åtkomst till Reactor API](./api/getting-started.md)
   * Slutpunkter {#endpoints}
      * [Företag](./api/endpoints/companies.md)
      * [Egenskaper](./api/endpoints/properties.md)
      * [Dataelement](./api/endpoints/data-elements.md)
      * [Regler](./api/endpoints/rules.md)
      * [Regelkomponenter](./api/endpoints/rule-components.md)
      * [Tilläggspaket](./api/endpoints/extension-packages.md)
      * [Användningsbehörighet för tilläggspaket](./api/endpoints/extension-package-usage-authorizations.md)
      * [Tillägg](./api/endpoints/extensions.md)
      * [Bibliotek](./api/endpoints/libraries.md)
      * [Bygger](./api/endpoints/builds.md)
      * [Miljöer](./api/endpoints/environments.md)
      * [Värdar](./api/endpoints/hosts.md)
      * [Appkonfigurationer](./api/endpoints/app-configurations.md)
      * [Granskningshändelser](./api/endpoints/audit-events.md)
      * [Återanrop](./api/endpoints/callbacks.md)
      * [Anteckningar](./api/endpoints/notes.md)
      * [Profil](./api/endpoints/profile.md)
      * [Sök](./api/endpoints/search.md)
      * [Hemligheter](./api/endpoints/secrets.md)
   * Användarhandböcker {#guides}
      * [Delegera beskrivnings-ID:n](./api/guides/delegate-descriptor-ids.md)
      * [Krypteringsvärden](./api/guides/encrypting-values.md)
      * [Felhantering](./api/guides/error-handling.md)
      * [Dela privata tilläggspaket](./api/guides/extension-packages.md)
      * [Filtrera svar](./api/guides/filtering.md)
      * [Sidinisera svar](./api/guides/pagination.md)
      * [Sortera svar](./api/guides/sorting.md)
      * [Relationer](./api/guides/relationships.md)
      * [Sökresurser](./api/guides/search.md)
      * [Hemligheter](./api/guides/secrets.md)
* [Vanliga frågor och svar](./faq.md)
* [Uppdateringar om terminologi](./term-updates.md)
* [Stöd för Internet Explorer 10 och 11 har tagits bort](./ie-deprecation.md)
* [Versionsinformation om Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)

