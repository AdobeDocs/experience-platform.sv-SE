---
title: Customer.io Source Overview
description: Lär dig hur du ansluter Customer.io till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att utnyttja webbhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>The [!DNL Customer.io] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för strömningsleverantörer innefattar [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) är en plattform för automatiserade meddelanden för marknadsförare som vill ha större kontroll och flexibilitet att skapa och skicka datadrivna e-postmeddelanden, push-meddelanden, meddelanden i appen och SMS.

The [!DNL Customer.io] Med -källa kan du importera webbhoaktiviteter som stöds och tillhörande händelsedata från [!DNL Customer.io] med [[!DNL Customer.io] Rapportera webbhotell](https://customer.io/docs/api/webhooks/).

De webbholls-händelsescheman som stöds är:

* Kundevent
* E-posthändelser
* SMS-händelser
* Push-meddelandehändelser
* Meddelandehändelser i appar
* Slack Events
* Webkrohändelser

En lista över händelser som är tillgängliga via webbhooks finns i [[!DNL Customer.io] Rapportera webbhotell-händelser](https://customer.io/docs/webhooks/#events) dokumentation.

## Förutsättningar {#prerequisites}

Innan du kan skapa en [!DNL Customer.io] måste du först kontrollera att du har följande:

* A [!DNL Customer.io] konto. Om du inte har någon kan du läsa [[!DNL Customer.io] registreringssida](https://fly.customer.io/signup) för att registrera och skapa ditt konto.
* När du har skapat ditt konto måste du också validera kontot. Följ de steg som beskrivs på [[!DNL Customer.io] Kontoverifiering](https://customer.io/docs/account-verification/) sida för att slutföra processen.

### Konfigurera [!DNL Customer.io] Webkrok {#set-up-webhook}

När du har skapat dataflödet måste du konfigurera en webkrok för rapportering för att informera plattformen om [!DNL Customer.io] händelser. Webhooks kan meddela dig omedelbart när kundattributen ändras eller när någon öppnar dina meddelanden och skicka informationen till [!DNL Customer.io] källa. Mer information finns i självstudiekurserna på [hämta URL för direktuppspelningsslutpunkt](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) och [konfigurera [!DNL Customer.io] Webkrok](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Ansluter [!DNL Customer.io] till plattform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Customer.io] direktuppspelningsanslutning att ansluta med [!DNL Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Customer.io] till plattform med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning och ett dataflöde som ger [!DNL Customer.io] data till plattformen med API:er.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Anslut [!DNL Customer.io] till plattform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning och ett dataflöde som ger [!DNL Customer.io] data till plattformen via användargränssnittet](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
