---
solution: Data Collection
audience: user
user-guide-title: Hjälp med webb-SDK för Adobe Experience Platform
breadcrumb-title: Användarhandbok om webb-SDK
user-guide-description: Interagera med Experience Cloud-tjänsterna via Edge Network.
feature: Web SDK
role: Developer
source-git-commit: 1a6d42fd1319828f5bb5d470f24ea5ee8bed4661
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 19%

---


# Webb-SDK för Adobe Experience Platform {#web-sdk}

* [Web SDK - översikt](home.md)
* [Versionsinformation](release-notes.md)
* Web SDK-installation {#install}
   * [Översikt](install/overview.md)
   * [Installera Web SDK med hjälp av taggtillägget](install/extension.md)
   * [Installera Web SDK med JavaScript-biblioteket](install/library.md)
   * [Installera Web SDK med NPM-paketet](install/npm.md)
* Kommandon {#commands}
   * konfigurera {#configure}
      * [Översikt](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [kontext](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehideStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Översikt](commands/sendevent/overview.md)
      * [data](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personalisering](commands/sendevent/personalization.md)
      * [renderDecision](commands/sendevent/renderdecisions.md)
      * [type](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Konfigurera åsidosättningar av datastream](commands/datastream-overrides.md)
   * [Kommandosvar](commands/command-responses.md)

* Identitet {#identity}
   * [Översikt](identity/overview.md)
   * [Enhets-ID:n från första part](identity/first-party-device-ids.md)
   * [Delning av mobil-till-webb och domänövergripande ID](identity/id-sharing.md)

* Personalisering {#personalization}
   * [Hantera visningshändelser](personalization/display-events.md)
   * [Återge personaliserat innehåll](personalization/rendering-personalization-content.md)
   * [Personalization via hybridimplementering](personalization/hybrid-personalization.md)
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
   * Offer decisioning {#offer-decisioning}
      * [Översikt](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Översikt](personalization/ajo/overview.md)
      * [Programimplementering på en sida](personalization/ajo/web-spa-implementation.md)
      * [Konfigurera stöd för webb-meddelanden i appen i Web SDK](personalization/web-in-app-messaging.md)

* Godkännande {#consent}
   * IAB Transparency och Consent Framework 2.0 {#iab-tcf}
      * [Översikt](consent/iab-tcf/overview.md)
      * [Integrera med taggar](consent/iab-tcf/with-tags.md)
      * [Integrera utan taggar](consent/iab-tcf/without-tags.md)

* Användningsfall {#use-cases}
   * [Översikt](use-cases/overview.md)
   * [Skicka data till Adobe Analytics via Web SDK](use-cases/adobe-analytics.md)
   * [Tips för användaragentklient](use-cases/client-hints.md)
   * [Samla in e-handelsdata](use-cases/collect-commerce-data.md)
   * [Konfigurera en CSP](use-cases/configuring-a-csp.md)
   * [Felsökningsmetoder](use-cases/debugging.md)
   * [Använda flera Web SDK-instanser](use-cases/multiple-instances.md)
   * [Konfigurera händelser för övre och nedre sidor](use-cases/top-bottom-page-events.md)

* [Vanliga frågor](faq.md)
* [Resurser](resources.md)
