---
audience: user
solution: Data Collection
user-guide-title: Datainsamling
breadcrumb-title: Datainsamling
user-guide-description: Lär dig skicka data till Adobe Experience Platform.
feature: Data Collection
role: Developer
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 16%

---


# Datainsamling {#collection}

+ [Översikt](home.md)
+ [Behörigheter](permissions.md)
+ BrightScript {#brightscript}
   + [BrightScript - översikt](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [JavaScript - översikt](js/js-overview.md)
   + [Versionsinformation](js/release-notes.md)
   + Installation {#install}
      + [Installationsöversikt](js/install/overview.md)
      + [Bibliotek](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Anpassad version](js/install/create-custom-build.md)
   + Kommandon {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + konfigurera {#configure}
         + [Översikt](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [kontext](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehideStyle](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Översikt](js/commands/sendevent/overview.md)
         + [data](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personalisering](js/commands/sendevent/personalization.md)
         + [renderDecision](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Kommandosvar](js/commands/command-responses.md)
   + [Övervaka kopplingar](js/monitoring-hooks.md)
   + [Vanliga frågor och svar](js/faq.md)
+ Taggar {#tags}
   + [Översikt](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [företag](tags/company.md)
   + [container](tags/container.md)
   + [cookie](tags/cookie.md)
   + [miljö](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [loggare](tags/logger.md)
   + [bildskärmar](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [spår](tags/track.md)
+ Användningsfall {#use-cases}
   + [Översikt](use-cases/overview.md)
   + [Klienttips](use-cases/client-hints.md)
   + [Klienttillstånd](use-cases/client-state.md)
   + [Samla in e-handelsdata](use-cases/collect-commerce-data.md)
   + [Konfigurera en CSP](use-cases/configuring-a-csp.md)
   + [Felsökning](use-cases/debugging.md)
   + [Borttagning av händelser](use-cases/event-duplication.md)
   + Identitet {#identity}
      + [Översikt](use-cases/identity/id-overview.md)
      + [Enhets-ID:n från första part](use-cases/identity/first-party-device-ids.md)
      + [ID-delning](use-cases/identity/id-sharing.md)
   + [Flera SDK-instanser](use-cases/multiple-instances.md)
   + Personalisering {#personalization}
      + [Översikt](use-cases/personalization/pers-overview.md)
      + [Visa händelser](use-cases/personalization/display-events.md)
      + [Hantera flimmer](use-cases/personalization/manage-flicker.md)
      + [Återge personaliserat innehåll](use-cases/personalization/rendering-personalization-content.md)
      + [Sidhändelser uppifrån och ned](use-cases/personalization/top-bottom-page-events.md)
