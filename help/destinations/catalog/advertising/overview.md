---
keywords: reklamdestinationer;destinationer;plattformsdestinationer
title: Översikt över Advertising destinationer
description: Koppla Adobe Experience Platform till en annonsplattform från tredje part (till exempel DSP, annonsnätverk, SSP) och dela pseudonyma målgrupper med dessa plattformar.
exl-id: 072743a4-fc62-4a61-92ec-8f9640a47ab2
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# Översikt över Advertising destinationer {#advertising-destinations}

## Översikt {#overview}

Anslut [!DNL Adobe Experience Platform] till annonsnätverk som efterfrågeplattformar (DSP), plattformar på utbudssidan (SSP) och nätverk för att dela kända och pseudonyma målgrupper med dessa plattformar.

När ni ansluter till en annonsdestination skickas era målgrupper som ID:n till målplattformen, där de mappas till ett ID som är känt av målplattformen.

## Annonsdestinationer som stöds {#supported-destinations}

För närvarande stöder Experience Platform de reklamdestinationer som anges nedan.

Mer information om skillnaden mellan anslutningar och tillägg finns i [Anslutningar](../../destination-types.md#connections) på sidan Måltyper och kategorier.

### Anslutningar {#connections}

* [(Beta) Acxiom Audience Distribution](acxiom-audience-connection.md)
* [(Beta) Acxiom Real ID Audience Connection](acxiom-real-id-audience-connection.md)
* [Adobe Advertising DSP](adobe-advertising-dsp-connection.md)
* [Äldre Adobe Advertising DSP-anslutning](adobe-advertising-cloud-dsp-connection-legacy.md)
* [Amazon Ads-anslutning](amazon-ads.md)
* [Amazon Ads v2-anslutning](amazon-ads-v2.md)
* [Bomboras anslutning](bombora.md)
* [Kriterieanslutning](criteo.md)
* [Demandbase-anslutning](demandbase.md)
* [Anslutning för Demandbase-användare](demandbase-people.md)
* [Google Display &amp; Video 360-anslutning](google-dv360.md)
* [Google Ads-anslutning](google-ads-destination.md)
* [Google Ad Manager-anslutning](google-ad-manager.md)
* [(Beta) Google Ad Manager 360-anslutning](google-ad-manager-360-connection.md)
* [Google Customer Match Connection](google-customer-match.md)
* [Magnite Batch-anslutning](magnite-batch.md)
* [Realtidsanslutning för Magnite Streaming](magnite-streaming.md)
* [Microsoft Bing-anslutning](bing.md)
* [Pinterest Customer List Connection](pinterest.md)
* [Mål för PubMatic Connect](pubmatic.md)
* [(Beta) Snapchat Ads-anslutning](snap-inc.md)
* [The Trade Desk connection](tradedesk.md)
* [(Beta) The Trade Desk CRM connection](tradedesk-emails.md)
* [Yahoo/Verizon DataX](datax.md)

### Tillägg {#extensions}

* [Adobe Advertising-tillägg](adobe-advertising-cloud.md)
* [Awin Advertising Conversion Tag extension](awin-conversiontag.md)
* [Awin Advertising Mastertag-tillägg](awin-mastertag.md)
* [Bing Ads Universal Event Tracking-tillägg](bing-ads.md)
* [Förgreningstillägg](branch.md)
* [Dubbelklicka på FlowLight-tillägg](doubleclick-floodlight.md)
* [Pixeltillägg för Facebook](facebook-pixel.md)
* [Flashtalk OneTag-tillägg](flashtalking.md)
* [Google Gtag-tillägg](gtag-advertising.md)
* [Tillägget LinkedIn Insight-tagg](linkedin.md)
* [Pinterest Conversion Tracking-tillägg](pinterest-extension.md)
* [Twitter Universal Website Tag-tillägg](twitter-uwt.md)

## Anslut till ett nytt annonsmål {#connect-destination}

För att kunna skicka målgrupper till reklamdestinationer för era kampanjer måste Experience Platform först ansluta till destinationen. Se självstudiekursen [för att skapa mål](../../ui/connect-destination.md) för mer information om hur du konfigurerar ett nytt mål.
