---
keywords: reklamdestinationer;destinationer;plattformsdestinationer
title: Översikt över reklamdestinationer
seo-title: Advertising destinations overview
description: Koppla Adobe Experience Platform till en annonsplattform från tredje part (t.ex. DSP, annonsnätverk, SSP) och dela pseudonyma målgrupper med dessa plattformar.
seo-description: Connect Adobe Experience Platform to a 3rd-party advertising platform (e.g. DSP, ad network, SSP) and share pseudonymous audiences to these platforms.
exl-id: 072743a4-fc62-4a61-92ec-8f9640a47ab2
source-git-commit: 74b3c6f24486d8b18750932f1268f0da7f5fa034
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Översikt över reklamdestinationer {#advertising-destinations}

## Översikt {#overview}

Koppla Adobe Experience Platform till annonsplattformar från tredje part, t.ex. DSP (Demand-Side Plattforms) (DSP), DSP (Supply-Side Plattformar) och annonsnätverk, och dela pseudonyma målgrupper med dessa plattformar.

När ni ansluter till en annonsdestination skickas era målgrupper som ID:n till målplattformen, där de mappas till ett ID som är känt av målplattformen.

## Annonsdestinationer som stöds {#supported-destinations}

För närvarande stöder Experience Platform de reklamdestinationer som anges nedan.

Information om skillnaden mellan anslutningar och tillägg finns i [Anslutningar](../../destination-types.md#connections) på sidan Måltyper och -kategorier.

### Anslutningar

* [(Beta) Kriterieanslutning](criteo.md)
* [Google Display &amp; Video 360-anslutning](google-dv360.md)
* [Google Ads-anslutning](google-ads-destination.md)
* [Google Ad Manager-anslutning](google-ad-manager.md)
* [(Beta) Google Ad Manager 360-anslutning](google-ad-manager-360-connection.md)
* [Google Customer Match Connection](google-customer-match.md)
* [Microsoft Bing-anslutning](bing.md)
* [Pinterest Customer List Connection](pinterest.md)
* [The Trade Desk connection](tradedesk.md)
* [Yahoo/Verizon DataX](datax.md)

### Tillägg

* [Adobe Advertising Cloud-tillägg](adobe-advertising-cloud.md)
* [Tillägget Awin Advertising Conversion Tag](awin-conversiontag.md)
* [Awin Advertising Mastertag-tillägg](awin-mastertag.md)
* [Bing Ads Universal Event Tracking-tillägg](bing-ads.md)
* [Filialtillägg](branch.md)
* [Dubbelklicka på FlowLight-tillägg](doubleclick-floodlight.md)
* [Facebook Pixel-tillägg](facebook-pixel.md)
* [Flashtalk OneTag-tillägg](flashtalking.md)
* [Google Ads-tillägg](google-ads-extension.md)
* [Google Gtag-tillägg](gtag-advertising.md)
* [linkedIn Insight Tag Extension](linkedin.md)
* [Pinterest Conversion Tracking-tillägg](pinterest-extension.md)
* [Tillägget twitter Universal Web Site Tag](twitter-uwt.md)

## Anslut till ett nytt annonsmål {#connect-destination}

Om du vill skicka segment till reklamdestinationer för era kampanjer måste Platform först ansluta till destinationen. Se [självstudiekurs om att skapa mål](../../ui/connect-destination.md) för detaljerad information om hur du konfigurerar ett nytt mål.
