---
title: Pendo Source - översikt
description: Lär dig hur du ansluter Pendo till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att använda webbhooks
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>Källan [!DNL Pendo] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från analysprogram från tredje part. Stöd för analysleverantörer inkluderar [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) är en produktanalysapp som har byggts för att hjälpa programvaruföretag att utveckla produkter som passar kunderna. Med appen kan programvarutillverkare bädda in sina produkter med ett stort antal verktyg som kan leda till både en bättre produktupplevelse för användarna och nya insikter för produktteamet.

Med källan [!DNL Pendo] kan du importera webbhooks-händelsescheman som stöds och tillhörande händelsedata från [!DNL Pendo.io] med hjälp av [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). [!DNL Pendo]-källan fungerar med [!DNL Pendo] URL-webbhooks.

De webbhooks som stöds är:

* [Guiden](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) visas
* [Avfrågning](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) visas/skickas
* [Net Promoter-poäng](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) som visas/skickas

## Förhandskrav {#prerequisites}

Innan du kan skapa en [!DNL Pendo]-källanslutning måste du se till att du har följande:

Ett [!DNL Pendo]-konto. Om du inte redan har någon kan du se sidan [[!DNL Pendo] registrera](https://app.pendo.io/register) för att registrera och skapa ditt konto.

### Konfigurera [!DNL Pendo]-webkrok {#set-up-webhook}

När du har skapat dataflödet måste du konfigurera en webkrok som informerar Experience Platform om [!DNL Pendo]-händelser. [!DNL Pendo] Webhooks kan skicka ut meddelanden i realtid till andra tjänster när vissa händelser inträffar och skicka informationen till din [!DNL Pendo]-källa. Mer information finns i självstudiekurserna om hur du [hämtar URL:en för direktuppspelningsslutpunkten](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) och [konfigurerar en [!DNL Pendo] webkrok](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Ansluter [!DNL Pendo] till Experience Platform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Pendo]-direktuppspelningsanslutare som ska ansluta till [!DNL Experience Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Pendo] till Experience Platform med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning för att hämta  [!DNL Pendo] -data till Experience Platform med API:er.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Anslut [!DNL Pendo] till Experience Platform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning för att hämta  [!DNL Pendo] -data till Experience Platform med användargränssnittet](../../tutorials/ui/create/analytics/pendo-webhook.md)
