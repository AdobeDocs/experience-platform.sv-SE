---
audience: user
user-guide-title: Destinationshandbok
user-guide-description: Aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
description: I det här dokumentet visas innehållsförteckningen för Adobe Experience Platform-destinationer
feature: Destinations
source-git-commit: 69bf43f86ab3369ad0c7febcb69ec41d3bcac8bb
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 1%

---


# Mål  {#destinations}

* [Översikt över mål](./home.md)
* [Måltyper och -kategorier](./destination-types.md)
* API-självstudiekurser {#api}
   * [Anslut till direktuppspelningsmål och aktivera data med API:t för Flow Service](./api/streaming-destinations.md)
   * [Anslut till gruppmolnlagring och e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](./api/connect-activate-batch-destinations.md)
   * [(Beta) Aktivera målgruppssegment till batchmål via ad hoc-aktiverings-API](./api/ad-hoc-activation-api.md)
   * [Uppdatera måldataflöden](./api/update-destination-dataflows.md)
   * [Ta bort destinationskonton](./api/delete-destination-account.md)
   * [Ta bort måldataflöden](./api/delete-destination-dataflow.md)
* Användargränssnittsguider {#ui}
   * [Arbetsytan Destinationer](./ui/destinations-workspace.md)
   * [Skapa en ny målanslutning](./ui/connect-destination.md)
   * Aktivera målgruppsdata för destinationer{#activate}
      * [Aktiveringsöversikt](./ui/activation-overview.md)
      * [Aktivera målgruppsdata för att direktuppspela segmentexportmål](./ui/activate-segment-streaming-destinations.md)
      * [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md)
      * [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md)
      * [Aktivera målgruppsdata för att profilera mål för begäran](./ui/activate-profile-request-destinations.md)
      * [Konfigurera personaliseringsmål för personalisering på samma sida och nästa sida](./ui/configure-personalization-destinations.md)
      * [(Beta) Exportera filer on demand till gruppmål med hjälp av användargränssnittet i Experience Platform](./ui/export-file-now.md)
   * [Visa målinformation](./ui/destination-details-page.md)
   * [Uppdatera destinationskonton](./ui/update-accounts.md)
   * [Ta bort destinationskonton](./ui/delete-destination-account.md)
   * [Redigera aktiveringsdataflöden](./ui/edit-activation.md)
   * [Ta bort mål](./ui/delete-destinations.md)
   * [Övervaka dataflöden](./ui/monitor-dataflows.md)
   * [Prenumerera på aviseringar om destinationer i sitt sammanhang](ui/alerts.md)
* Målkatalog {#catalog}
   * [Översikt över destinationskatalogen](./catalog/overview.md)
   * Adobe destinationer{#adobe}
      * [Översikt över destinationer i Adobe](./catalog/adobe/overview.md)
      * [Marketo Engage](./catalog/adobe/marketo-engage.md)
      * [Experience Platform segmentdelning](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Annonsmål{#advertising}
      * [Översikt över reklamdestinationer](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud-anslutning](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud-tillägg](./catalog/advertising/adobe-advertising-cloud.md)
      * [Tillägget Awin Advertiser Conversion Tag](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag-tillägg](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads UET-tillägg (Universal Event Tracking)](./catalog/advertising/bing-ads.md)
      * [Filialtillägg](./catalog/advertising/branch.md)
      * [(Beta) Kriterieanslutning](./catalog/advertising/criteo.md)
      * [Dubbelklicka på FlöLjus-tillägget (beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel-tillägg](./catalog/advertising/facebook-pixel.md)
      * [Flashtalk OneTag-tillägg](./catalog/advertising/flashtalking.md)
      * [Google Ads-anslutning](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-tillägg](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-anslutning](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Google Ad Manager 360-anslutning](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google Customer Match Connection](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360-anslutning](./catalog/advertising/google-dv360.md)
      * [Google Gtag-tillägg](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag Extension](./catalog/advertising/linkedin.md)
      * [Microsoft Bing-anslutning](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-tillägg](./catalog/advertising/pinterest-extension.md)
      * [Pinterest Customer List Connection](./catalog/advertising/pinterest.md)
      * [(Beta) Snapchat Ads-anslutning](./catalog/advertising/snap-inc.md)
      * [The Trade Desk connection](./catalog/advertising/tradedesk.md)
      * [CRM-anslutningen för Trade Desk](./catalog/advertising/tradedesk-emails.md)
      * [Tillägget twitter Universal Web Site Tag](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX-anslutning](./catalog/advertising/datax.md)
   * Analysmål {#analytics}
      * [Översikt över Analytics-destinationer](./catalog/analytics/overview.md)
      * [Anpassa tillägg för webbplatsspårning](./catalog/analytics/adform.md)
      * [Adobe Analytics-tillägg](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics för ljud- och videotillägg](./catalog/analytics/adobe-video-analytics.md)
      * [Klickbart tillägg](./catalog/analytics/clicktale.md)
      * [Innehållsfyrkantigt tillägg](./catalog/analytics/contentsquare.md)
      * [Decibel-tillägg](./catalog/analytics/decibel.md)
      * [Demandbase-tillägg](./catalog/analytics/demandbase.md)
      * [DialogTech-tillägg](./catalog/analytics/dialogtech.md)
      * [Tillägget Google Global Site Tag](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics-tillägg](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics-tillägg (beta)](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK-tillägg](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA Handler Extension](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS Player Handler Extension](./catalog/analytics/nielsen-videojs.md)
      * [Analysera.ly Analytics-tillägg](./catalog/analytics/parsely.md)
      * [Quantum Metric-tillägg](./catalog/analytics/quantum-metric.md)
      * [SessionCam-tillägg](./catalog/analytics/sessioncam.md)
      * [TMMData-tillägg](./catalog/analytics/tmmdata.md)
      * [Yext Conversion Tracking-tillägg](./catalog/analytics/yext.md)
   * Lagringsmål i molnet {#cloud-storage}
      * [Översikt över destinationer för molnlagring](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis-anslutning](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-anslutning](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-anslutning](./catalog/cloud-storage/azure-blob.md)
      * [Azure Event Hubs-anslutning](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP-anslutning](./catalog/cloud-storage/sftp.md)
      * [IP-adress tillåtelselista för molnlagringsmål](./catalog/cloud-storage/ip-address-allow-list.md)
   * Plattformsmål för datahantering {#data-management}
      * [Översikt över mål för datahanteringsplattformen (DMP)](./catalog/data-management/overview.md)
      * [Audience Manager DIL utökningen](./catalog/data-management/aam-dil-extension.md)
   * E-postmål {#email}
      * [Bizible-tillägg](./catalog/email/bizible.md)
      * [Marketo-tillägg](./catalog/email/marketo.md)
      * [Marketo Munchkin-tillägg](./catalog/email/marketo-munchkin.md)
      * [PebblePost-tillägg](./catalog/email/pebblepost.md)
   * E-postmarknadsföringsmål {#email-marketing}
      * [Översikt över destinationer för e-postmarknadsföring](./catalog/email-marketing/overview.md)
      * [Adobe Campaign-anslutning](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle Eloqua-anslutning](./catalog/email-marketing/oracle-eloqua.md)
      * [Oraclena svarssystemanslutning](./catalog/email-marketing/oracle-responsys.md)
      * [Salesforce Marketing Cloud-anslutning](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [SendGrid-anslutning](./catalog/email-marketing/sendgrid.md)
   * Märkordstillägg {#launch-extensions}
      * [Översikt över taggtillägg](./catalog/launch-extensions/overview.md)
   * Destinationer för mobilengagemang {#mobile-engagement}
      * [Översikt över mål för mobilengagemang](./catalog/mobile-engagement/overview.md)
      * [Luftfartygsattribut](./catalog/mobile-engagement/airship-attributes.md)
      * [Ansluta till luftfartygets taggar](./catalog/mobile-engagement/airship-tags.md)
      * [Braze connection](./catalog/mobile-engagement/braze.md)
   * Destinationer för personalisering {#personalization}
      * [Översikt över destinationer för personalisering](./catalog/personalization/overview.md)
      * [Adobe Target-anslutning](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target-tillägg](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-tillägg](./catalog/personalization/adobe-target-v2.md)
      * [Beemray-tillägg](./catalog/personalization/beemray.md)
      * [Anpassad personaliseringsanslutning](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence-tillägg](./catalog/personalization/dnb.md)
      * [Experience Cloud ID-tjänsttillägg](./catalog/personalization/adobe-ecid.md)
      * [Gainsight-tillägg](./catalog/personalization/gainsight.md)
      * [KickFire-tillägg](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization-tillägg](./catalog/personalization/marketo-web-personalization.md)
   * Sociala destinationer{#social}
      * [Översikt över sociala mål](./catalog/social/overview.md)
      * [Adobe Livefyre-tillägg](./catalog/social/adobe-livefyre.md)
      * [Facebook-anslutning](./catalog/social/facebook.md)
      * [linkedIn Matched Auditions connection](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] anslutning](./catalog/social/twitter.md)
   * Målgrupper för direktuppspelning {#streaming}
      * [HTTP API-anslutning](./catalog/streaming/http-destination.md)
      * [IP-adress tillåtelselista för direktuppspelningsmål](./catalog/streaming/ip-address-allow-list.md)
   * Undersökningsmål {#survey}
      * [Översikt över undersökningsmål](./catalog/survey/overview.md)
      * [Mål för sidtillägg](./catalog/survey/foresee.md)
      * [InMoment-tillägg](./catalog/survey/inmoment.md)
      * [Qualtrics-tillägg för webbplatsfeedback](./catalog/survey/qualtrics.md)
      * [QuestionPro Intercept Surveys extension](./catalog/survey/web-intercept-surveys.md)
   * Voice of the customer destination {#voice}
      * [Översikt över kundens destinationer](./catalog/voice/overview.md)
      * [Bekräfta tillägg för digital feedback](./catalog/voice/confirmit-digital-feedback.md)
      * [Anropa taggtillägg](./catalog/voice/invoca.md)
      * [Medieanslutning](./catalog/voice/medallia-connector.md)
      * [Medietillägg](./catalog/voice/medallia.md)
      * [Tillägg för URL-inkorg](./catalog/voice/talkurl.md)
* Destination SDK {#destination-sdk}
   * [Översikt](./destination-sdk/overview.md)
   * [Krav för integrering](./destination-sdk/integration-prerequisites.md)
   * [Komma igång](./destination-sdk/getting-started.md)
   * Destination SDK {#functionality}
      * [Konfigurationsalternativ](./destination-sdk/configuration-options.md)
      * [Konfiguration för direktuppspelningsmål](./destination-sdk/destination-configuration.md)
      * [(Beta) Filbaserad målkonfiguration](./destination-sdk/file-based-destination-configuration.md)
      * [Serverspecifikationer och mallspecifikationer för direktuppspelningsmål](./destination-sdk/server-and-template-configuration.md)
      * [(Beta) Filbaserade mål, server- och filspecifikationer](./destination-sdk/server-and-file-configuration.md)
      * [Meddelandeformat](./destination-sdk/message-format.md)
      * [Hantering av målgruppsmetadata](./destination-sdk/audience-metadata-management.md)
      * Autentisering {#authentication}
         * [Autentiseringskonfiguration](./destination-sdk/authentication-configuration.md)
         * [OAuth 2-autentisering](./destination-sdk/oauth2-authentication.md)
      * Utvecklarverktyg {#developer-tools}
         * [Skapa och testa en meddelandeomformningsmall](./destination-sdk/create-template.md)
         * [Testa målkonfigurationen](./destination-sdk/test-destination.md)
   * API-åtgärder {#api}
      * [API-referens för Destination SDK (målredigering)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [API-åtgärder för destinationsslutpunkt](./destination-sdk/destination-configuration-api.md)
      * [API-åtgärder för målserverns slutpunkt](./destination-sdk/destination-server-api.md)
      * [API-åtgärder för målgruppsmetadata](./destination-sdk/audience-metadata-api.md)
      * [API-åtgärder för slutpunkt för autentiseringsuppgifter](./destination-sdk/credentials-configuration-api.md)
      * [Publicera API-åtgärder för slutpunkt](./destination-sdk/destination-publish-api.md)
      * Referens för utvecklingsverktyg {#developer-tools-reference}
         * API för testning av direktuppspelningsmål {#streaming-destination-testing-api}
            * [Hämta API-åtgärder för exempelmallar](./destination-sdk/sample-template-api.md)
            * [API-åtgärder för återgivningsmall](./destination-sdk/render-template-api.md)
            * [API-åtgärder för måltestning](./destination-sdk/destination-testing-api.md)
            * [API-åtgärder för generering av exempelprofiler](./destination-sdk/sample-profile-generation-api.md)
         * Filbaserat API för måltestning {#file-based-destination-testing-api}
            * [Översikt över API för filbaserad destinationstestning](./destination-sdk/file-based-destination-testing-overview.md)
            * [Generera exempelprofiler baserat på ett källschema](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Testa ditt filbaserade mål med exempelprofiler](./destination-sdk/file-based-destination-testing-api.md)
            * [Visa detaljerade aktiveringsresultat](./destination-sdk/file-based-destination-results-api.md)
            * [Validera mallsidiga kundfält](./destination-sdk/file-based-render-template-api.md)
   * Stödlinjer {#guides}
      * [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](./destination-sdk/configure-destination-instructions.md)
      * [(Beta) Använd Destination SDK för att konfigurera ett filbaserat mål](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Skicka för granskning av ett mål som skapats i Destination SDK](./destination-sdk/submit-destination.md)
   * Referens {#reference}
      * [Regler för hastighetsbegränsning och återförsök för direktuppspelningsmål](./destination-sdk/rate-limiting-retry-policy.md)
      * [Omformningsfunktioner som stöds](./destination-sdk/supported-functions.md)
   * Dokumentera destinationen {#document-destination}
      * [Dokumentera destinationen i Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Skapa en måldokumentationssida med en textredigerare i den lokala miljön](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Självbetjäningsmall för dokumentation](./destination-sdk/docs-framework/self-service-template.md)
      * [Bästa tillvägagångssätt](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Frågor och svar](./destinations-faq.md)
* [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)
