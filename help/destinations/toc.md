---
audience: user
user-guide-title: Destinationshandbok
user-guide-description: Aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
description: I det här dokumentet visas innehållsförteckningen för Adobe Experience Platform-destinationer
feature: 'Mål '
source-git-commit: 9c9ea0d9e8247dbc4a1a4078dbdba2ae80ed70ef
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Mål  {#destinations}

* [Översikt över mål](./home.md)
* [Måltyper och -kategorier](./destination-types.md)
* API-självstudiekurser {#api}
   * [Anslut till direktuppspelningsmål och aktivera data med API:t för Flow Service](./api/streaming-destinations.md)
   * [Anslut till e-postmarknadsföringsmål och aktivera data med API:t för Flow Service](./api/email-marketing.md)
* Användargränssnittsguider {#ui}
   * [Arbetsytan Destinationer](./ui/destinations-workspace.md)
   * [Skapa en ny målanslutning](./ui/connect-destination.md)
   * Aktivera målgruppsdata till mål{#activate}
      * [Aktiveringsöversikt](./ui/activation-overview.md)
      * [Aktivera målgruppsdata för att direktuppspela segmentexportmål](./ui/activate-segment-streaming-destinations.md)
      * [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md)
      * [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md)
   * [Visa målinformation](./ui/destination-details-page.md)
   * [Uppdatera destinationskonton](./ui/update-accounts.md)
   * [Redigera aktiveringsflöden](./ui/edit-activation.md)
   * [Ta bort mål](./ui/delete-destinations.md)
   * [Övervaka dataflöden](./ui/monitor-dataflows.md)
* Målkatalog {#catalog}
   * [Översikt över destinationskatalogen](./catalog/overview.md)
   * [ (Alfa) HTTP-anslutning](./catalog/http-destination.md)
   * Adobe mål{#adobe}
      * [Översikt över destinationer i Adobe](./catalog/adobe/overview.md)
      * [(Beta) Marketo Engage-anslutning](./catalog/adobe/marketo-engage.md)
      * [Experience Platform segmentdelning](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * Annonsmål{#advertising}
      * [Översikt över reklamdestinationer](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud-tillägg](./catalog/advertising/adobe-advertising-cloud.md)
      * [Tillägget Awin Advertiser Conversion Tag](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag-tillägg](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads UET-tillägg (Universal Event Tracking)](./catalog/advertising/bing-ads.md)
      * [Filialtillägg](./catalog/advertising/branch.md)
      * [Dubbelklicka på FlöLjus-tillägget (beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel-tillägg](./catalog/advertising/facebook-pixel.md)
      * [Flashtalk OneTag-tillägg](./catalog/advertising/flashtalking.md)
      * [Google Ads-anslutning](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-tillägg](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-anslutning](./catalog/advertising/google-ad-manager.md)
      * [Google Customer Match Connection](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360-anslutning](./catalog/advertising/google-dv360.md)
      * [Google-taggtillägg](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag Extension](./catalog/advertising/linkedin.md)
      * [Microsoft Bing-anslutning](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-tillägg](./catalog/advertising/pinterest-extension.md)
      * [The Trade Desk connection](./catalog/advertising/tradedesk.md)
      * [Tillägget twitter Universal Web Site Tag](./catalog/advertising/twitter-uwt.md)
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
   * Lagringsmål för molnet {#cloud-storage}
      * [Översikt över destinationer för molnlagring](./catalog/cloud-storage/overview.md)
      * [(Beta) Amazon Kinesis-anslutning](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-anslutning](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-anslutning](./catalog/cloud-storage/azure-blob.md)
      * [(Beta) Azure Event Hubs-anslutning](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP-anslutning](./catalog/cloud-storage/sftp.md)
      * [IP-adress tillåtelselista](./catalog/cloud-storage/ip-address-allow-list.md)
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
   * Taggtillägg {#launch-extensions}
      * [Översikt över taggtillägg](./catalog/launch-extensions/overview.md)
   * Destinationer för mobilengagemang {#mobile-engagement}
      * [Översikt över mål för mobilengagemang](./catalog/mobile-engagement/overview.md)
      * [(Beta) Koppling mellan attribut för luftskepp](./catalog/mobile-engagement/airship-attributes.md)
      * [(Beta) Koppling mellan luftfartygets taggar](./catalog/mobile-engagement/airship-tags.md)
      * [(Beta) Braze connection](./catalog/mobile-engagement/braze.md)
   * Destinationer för personalisering {#personalization}
      * [Översikt över destinationer för personalisering](./catalog/personalization/overview.md)
      * [Adobe Target-tillägg](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-tillägg](./catalog/personalization/adobe-target-v2.md)
      * [Beemray-tillägg](./catalog/personalization/beemray.md)
      * [D&amp;B Visitor Intelligence-tillägg](./catalog/personalization/dnb.md)
      * [Experience Cloud ID-tjänsttillägg](./catalog/personalization/adobe-ecid.md)
      * [Gainsight-tillägg](./catalog/personalization/gainsight.md)
      * [KickFire-tillägg](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization-tillägg](./catalog/personalization/marketo-web-personalization.md)
   * Sociala mål{#social}
      * [Översikt över sociala mål](./catalog/social/overview.md)
      * [Adobe Livefyre-tillägg](./catalog/social/adobe-livefyre.md)
      * [Facebook-anslutning](./catalog/social/facebook.md)
      * [linkedIn Matched Auditions connection](./catalog/social/linkedin.md)
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
      * [Medietillägg](./catalog/voice/medallia.md)
      * [Tillägg för URL-inkorg](./catalog/voice/talkurl.md)
* [Frågor och svar](./destinations-faq.md)
* [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)
