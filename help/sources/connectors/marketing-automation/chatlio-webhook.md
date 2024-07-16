---
title: Chatlio Source - översikt
description: Lär dig hur du ansluter Chatlio till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att utnyttja webbhooks
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>Källan [!DNL Chatlio] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för direktuppspelningsproviders är [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) är en chattapp som är helt integrerad med [!DNL Slack] och som underlättar för flera supporttekniker att samtidigt hjälpa en enskild besökare. [!DNL Chatlio] använder [!DNL Chatio Zapier App] för att ansluta [!DNL Chatlio] med över 2 000 olika appar och tjänster.

Med källan [!DNL Chatlio] kan du importera webbhooks-händelsescheman som stöds och tillhörande händelsedata från [!DNL Chatlio.com] med hjälp av [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

De webbhooks som stöds är:

* Exportera chattutskrifter
* Exportera offlinemeddelanden
* Ny konversation har startats
* Besökaren fick inget svar i tid
* Besökaren lämnade feedback efter en chatt

## Förhandskrav {#prerequisites}

Innan du kan skapa en [!DNL Chatlio]-källanslutning måste du se till att du har följande:

* Ett [!DNL Chatlio]-konto. Om du inte redan har någon går du till [[!DNL Chatlio] registreringssidan](https://chatlio.com/app/#/signup) och registrerar och skapar ditt konto.
* När du har registrerat ett konto följer du [[!DNL Chatlio] installationsdokumentationen](https://chatlio.com/docs/setup/) för att slutföra kontokonfigurationen.

### Konfigurera webbkrok för [!DNL Chatlio] {#set-up-webhook}

När du har skapat dataflödet måste du konfigurera en webkrok som informerar plattformen om [!DNL Chatlio]-händelser. Webhooks kan meddela dig omedelbart när kundattributen ändras eller när personer öppnar dina meddelanden och skickar informationen till din [!DNL Chatlio]-källa.

Mer information finns i självstudiekurserna om hur du [hämtar URL:en för direktuppspelningsslutpunkten](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) och [konfigurerar en [!DNL Chatlio] webkrok](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Anslut [!DNL Chatlio] till plattformen {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Chatlio]-direktuppspelningsanslutare som ska ansluta till [!DNL Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Chatlio] till plattformen med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning för att hämta  [!DNL Chatlio] -data till plattformen med API:er.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Anslut [!DNL Chatlio] till plattformen med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning för att hämta  [!DNL Chatlio] -data till plattformen med användargränssnittet](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
