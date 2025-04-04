---
title: Customer.io Source Overview
description: Lär dig hur du ansluter Customer.io till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att utnyttja webbhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>Källan [!DNL Customer.io] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för direktuppspelningsproviders är [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) är en plattform för automatiserade meddelanden för marknadsförare som vill ha större kontroll och flexibilitet att skapa och skicka datadrivna e-postmeddelanden, push-meddelanden, meddelanden i appen och SMS.

Med källan [!DNL Customer.io] kan du importera webbhooks-händelsescheman som stöds och tillhörande händelsedata från [!DNL Customer.io] med hjälp av [[!DNL Customer.io] rapporteringswebbhooks](https://customer.io/docs/api/webhooks/).

De webbholls-händelsescheman som stöds är:

* Kundevent
* E-posthändelser
* SMS-händelser
* Push-meddelandehändelser
* Meddelandehändelser i appar
* Slack Events
* Webkrohändelser

En lista över händelser som är tillgängliga via webbhookar finns i dokumentationen för [[!DNL Customer.io] Reporting Webkroch-händelser](https://customer.io/docs/webhooks/#events) .

## Förhandskrav {#prerequisites}

Innan du kan skapa en [!DNL Customer.io]-källanslutning måste du se till att du har följande:

* Ett [!DNL Customer.io]-konto. Om du inte har läst [[!DNL Customer.io] registreringssidan](https://fly.customer.io/signup) för att registrera och skapa ditt konto.
* När du har skapat ditt konto måste du också validera kontot. Slutför processen genom att följa stegen som beskrivs på sidan [[!DNL Customer.io] Kontoverifiering](https://customer.io/docs/account-verification/).

### Konfigurera [!DNL Customer.io]-webkrok {#set-up-webhook}

När du har skapat dataflödet måste du konfigurera en rapportwebkrok som informerar Experience Platform om [!DNL Customer.io] händelser. Webhooks kan meddela dig omedelbart när kundattributen ändras eller när personer öppnar dina meddelanden, och skicka informationen till din [!DNL Customer.io]-källa. Mer information finns i självstudiekurserna om hur du [hämtar URL:en för direktuppspelningsslutpunkten](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) och [konfigurerar en [!DNL Customer.io] webkrok](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Ansluter [!DNL Customer.io] till Experience Platform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Customer.io]-direktuppspelningsanslutning för att ansluta till [!DNL Experience Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Customer.io] till Experience Platform med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning och ett dataflöde för att hämta  [!DNL Customer.io] -data till Experience Platform med API:er.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Anslut [!DNL Customer.io] till Experience Platform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning och ett dataflöde för att hämta [!DNL Customer.io] data till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
