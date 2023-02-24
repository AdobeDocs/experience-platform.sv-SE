---
title: Översikt över Pendo-källa
description: Lär dig hur du ansluter Pendo till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att använda webbhooks
badge: "Beta"
source-git-commit: 24691e3ded33c3af31fd0cee107f2f3ca898585f
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>The [!DNL Pendo] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inhämtning av data från analysprogram från tredje part. Stöd för analysleverantörer innefattar [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) är en produktanalysapp som byggts för att hjälpa programvaruföretag att utveckla produkter som passar in hos kunderna. Med appen kan programvarutillverkare bädda in sina produkter med ett stort antal verktyg som kan leda till både en bättre produktupplevelse för användarna och nya insikter för produktteamet.

The [!DNL Pendo] Med -källa kan du importera webbhoaktiviteter som stöds och tillhörande händelsedata från [!DNL Pendo.io] med [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). The [!DNL Pendo] fungerar med [!DNL Pendo] URL-webbhooks.

De webbhooks som stöds är:

* [Guide](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Visad
* [Omröstning](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Visad/skickad
* [Net Promoter Score](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Visad/skickad

## Förutsättningar {#prerequisites}

Innan du kan skapa en [!DNL Pendo] måste du först kontrollera att du har följande:

A [!DNL Pendo] konto. Om du inte redan har en kan du se [[!DNL Pendo] register](https://app.pendo.io/register) för att registrera och skapa ditt konto.

### Konfigurera [!DNL Pendo] Webkrok {#set-up-webhook}

När du har skapat dataflödet måste du skapa en webkrok som informerar plattformen om [!DNL Pendo] händelser. [!DNL Pendo] Webhooks kan skicka ut meddelanden i realtid till andra tjänster när vissa händelser inträffar och skicka informationen till [!DNL Pendo] källa. Mer information finns i självstudiekurserna på [hämta URL för direktuppspelningsslutpunkt](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) och [konfigurera [!DNL Pendo] Webkrok](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Ansluter [!DNL Pendo] till plattform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Pendo] direktuppspelningskontakt att ansluta med [!DNL Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Pendo] till plattform med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning att hämta [!DNL Pendo] data till plattformen med API:er.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Anslut [!DNL Pendo] till plattform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning att hämta [!DNL Pendo] data till plattformen via användargränssnittet](../../tutorials/ui/create/analytics/pendo-webhook.md)

