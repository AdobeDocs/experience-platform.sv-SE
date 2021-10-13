---
audience: user
user-guide-title: Hjälp om taggar
breadcrumb-title: Taggar
user-guide-description: Lär dig att driftsätta och hantera analyser, marknadsföring och annonstaggar för att ge bättre kundupplevelser.
feature: Tags
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 25%

---


# Taggar {#tags}

* [Översikt över taggar](./home.md)
* Komma igång {#get-started}
   * [Snabbstartguide](./quick-start/quick-start.md)
   * [Implementeringsguider](./quick-start/implementation-guides.md)
* Användargränssnitt för datainsamling {#ui}
   * [Översikt](./ui/managing-resources/overview.md)
   * Tillägg {#extensions}
      * [Översikt](./ui/managing-resources/extensions/overview.md)
      * [Tilläggsuppgraderingar](./ui/managing-resources/extensions/extension-upgrade.md)
   * [Dataelement](./ui/managing-resources/data-elements.md)
   * [Regler](./ui/managing-resources/rules.md)
   * [Anteckningar](./ui/managing-resources/notes.md)
   * [Kopiera resurser](./ui/managing-resources/copying-resources.md)
   * [Jämför resursrevisioner](./ui/managing-resources/compare-resource-revisions.md)
   * [Ta bort resurser](./ui/managing-resources/delete-resources.md)
   * [Ta bort resurser från ett bibliotek](./ui/managing-resources/remove-resources-from-library.md)
* Publicerar {#publish}
   * [Översikt](./ui/publishing/overview.md)
   * [Publiceringsflöde](./ui/publishing/publishing-flow.md)
   * Värdar {#hosts}
      * [Översikt](./ui/publishing/hosts/hosts-overview.md)
      * [Värdar som hanteras av Adobe](./ui/publishing/hosts/managed-by-adobe-host.md)
      * [SFTP-värdar](./ui/publishing/hosts/sftp-host.md)
   * Miljöer {#environments}
      * [Översikt](./ui/publishing/environments.md)
      * [Testa inbäddningskoder med Adobe Experience Platform Debugger](./ui/publishing/embed-code-testing.md)
   * [Bygger](./ui/publishing/builds.md)
   * [Bibliotek](./ui/publishing/libraries.md)
   * [Självvärdande bibliotek](./ui/publishing/hosts/self-hosting-libraries.md)
   * [Publicera om ett bibliotek](./ui/publishing/republish.md)
* Information på klientsidan {#client-side}
   * [Översikt](./ui/client-side/overview.md)
   * [Asynkron distribution](./ui/client-side/asynchronous-deployment.md)
   * [Satellitobjektreferens](./ui/client-side/satellite-object.md)
   * [Distribuera JavaScript-taggar för att hantera kundernas samtycke](./ui/client-side/consent.md)
   * [Stöd för CSP (Content Security Policy)](./ui/client-side/content-security-policy.md)
   * [Stöd för SRI (Subresource Integrity)](./ui/client-side/sri.md)
* Vidarebefordra händelse {#event-forwarding}
   * [Översikt](./ui/event-forwarding/overview.md)
   * [Komma igång](./ui/event-forwarding/getting-started.md)
* Administrering {#admin}
   * [Översikt](./ui/administration/overview.md)
   * [Företag och fastigheter](./ui/administration/companies-and-properties.md)
   * [Användarbehörigheter](./ui/administration/user-permissions.md)
   * [Hantera behörigheter](./ui/administration/manage-permissions.md)
* Tillägg {#extensions}
   * [Översikt](./extensions/overview.md)
   * Adobe-tillägg {#adobe}
      * [Översikt](./extensions/web/overview.md)
      * Adobe Analytics {#analytics}
         * [Översikt](./extensions/web/analytics/overview.md)
         * [Delade moduler](./extensions/web/analytics/shared-modules.md)
         * [Versionsinformation](./extensions/web/analytics/release-notes.md)
      * Adobe Analytics produktsträng {#product-string}
         * [Översikt](./extensions/web/product-string/overview.md)
         * [Versionsinformation](./extensions/web/product-string/release-notes.md)
      * Adobe Audience Manager {#audience-manager}
         * [Översikt](./extensions/web/audience-manager/overview.md)
      * Adobe-klientdatalagret {#client-data-layer}
         * [Översikt](./extensions/web/client-data-layer/overview.md)
         * [Versionsinformation](./extensions/web/client-data-layer/release-notes.md)
      * Adobe ContextHub {#contexthub}
         * [Översikt](./extensions/web/contexthub/overview.md)
      * Adobe Experience Cloud ID-tjänst {#id-service}
         * [Översikt](./extensions/web/id-service/overview.md)
         * [Versionsinformation](./extensions/web/id-service/release-notes.md)
      * Adobe Experience Platform Demo {#platform-demo}
         * [Översikt](./extensions/web/platform-demo/overview.md)
      * Webb-SDK för Adobe Experience Platform {#sdk}
         * [Översikt](./extensions/web/sdk/overview.md)
      * Adobe Experience Platform Cloud Connector {#cloud-connector}
         * [Översikt](./extensions/web/cloud-connector/overview.md)
      * Adobe Experience Manager Asset Insights {#asset-insights}
         * [Översikt](./extensions/web/asset-insights/overview.md)
         * [Versionsinformation](./extensions/web/asset-insights/release-notes.md)
      * Adobe Media Analytics för ljud och video {#media-analytics}
         * [Översikt](./extensions/web/media-analytics/overview.md)
         * [Versionsinformation](./extensions/web/media-analytics/release-notes.md)
      * Adobe Media Analytics (3.x SDK) {#media-analytics-3x}
         * [Översikt](./extensions/web/media-analytics-3x/overview.md)
         * [Versionsinformation](./extensions/web/media-analytics-3x/release-notes.md)
      * Sekretess för Adobe {#privacy}
         * [Översikt](./extensions/web/privacy/overview.md)
      * Adobe Target {#target}
         * [Översikt](./extensions/web/target/overview.md)
         * [Versionsinformation](./extensions/web/target/release-notes.md)
      * Adobe Target v2 {#target-v2}
         * [Översikt](./extensions/web/target-v2/overview.md)
         * [Versionsinformation](./extensions/web/target-v2/release-notes.md)
      * Plugin-program för vanlig analys {#plugins}
         * [Översikt](./extensions/web/plugins/overview.md)
         * [Versionsinformation](./extensions/web/plugins/release-notes.md)
      * Kärna {#core}
         * [Översikt](./extensions/web/core/overview.md)
         * [Vidarebefordran av händelser](./extensions/web/core/event-forwarding.md)
         * [Versionsinformation](./extensions/web/core/release-notes.md)
      * [!DNL Marketo Munchkin] {#marketo}
         * [Översikt](./extensions/web/marketo/overview.md)
         * [Versionsinformation](./extensions/web/marketo/release-notes.md)
      * [!DNL BrightCove] videouppföljning  {#brightcove}
         * [Översikt](./extensions/web/brightcove/overview.md)
         * [Versionsinformation](./extensions/web/brightcove/release-notes.md)
      * [!DNL YouTube] videospårningstillägg  {#youtube}
         * [Översikt](./extensions/web/youtube/overview.md)
         * [Versionsinformation](./extensions/web/youtube/release-notes.md)
   * [Tredjepartstillägg](./extensions/3rd-party-extensions.md)
* Tilläggsutveckling {#extension-dev}
   * [Översikt](./extension-dev/overview.md)
   * [Komma igång](./extension-dev/getting-started.md)
   * [Webbläsare som stöds](./extension-dev/browsers.md)
   * Inlämningsprocess {#submit}
      * [Översikt](./extension-dev/submit/overview.md)
      * [Företagsinställningar](./extension-dev/submit/setup.md)
      * [Bevilja användaråtkomst](./extension-dev/submit/access.md)
      * [Utveckla ett tillägg](./extension-dev/submit/develop.md)
      * [Skapa en börslista](./extension-dev/submit/create-listing.md)
      * [Ladda upp och implementera testning från början till slut](./extension-dev/submit/upload-and-test.md)
      * [Släpp ett tillägg](./extension-dev/submit/release.md)
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
* Reaktor-API {#api}
   * [Översikt](./api/overview.md)
   * [Komma igång](./api/getting-started.md)
   * Slutpunkter {#endpoints}
      * [Företag](./api/endpoints/companies.md)
      * [Egenskaper](./api/endpoints/properties.md)
      * [Dataelement](./api/endpoints/data-elements.md)
      * [Regler](./api/endpoints/rules.md)
      * [Regelkomponenter](./api/endpoints/rule-components.md)
      * [Tilläggspaket](./api/endpoints/extension-packages.md)
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
      * [Sökning](./api/endpoints/search.md)
   * Stödlinjer {#guides}
      * [Delegera beskrivnings-ID](./api/guides/delegate-descriptor-ids.md)
      * [Krypteringsvärden](./api/guides/encrypting-values.md)
      * [Felhantering](./api/guides/error-handling.md)
      * [Filtrera svar](./api/guides/filtering.md)
      * [Sidinisera svar](./api/guides/pagination.md)
      * [Sortera svar](./api/guides/sorting.md)
      * [Relationer](./api/guides/relationships.md)
      * [Sökresurser](./api/guides/search.md)
* [Vanliga frågor och svar ](./faq.md)
* [Uppdateringar om terminologi](./term-updates.md)
* Versionsinformation {#release-notes}
   * [Senaste](./release-notes/current.md)
   * [Versionsinformation 2020](./release-notes/2020.md)
   * [Versionsinformation 2019](./release-notes/2019.md)
   * [Versionsinformation 2018](./release-notes/2018.md)