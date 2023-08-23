---
title: Chatlio Source Overview
description: Lär dig hur du ansluter Chatlio till Adobe Experience Platform med hjälp av API:er eller användargränssnittet genom att utnyttja webbhooks
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# [!DNL Chatlio]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för strömningsleverantörer innefattar [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) är en live chattapp som är helt integrerad med [!DNL Slack] och underlättar för flera supporttekniker att samtidigt hjälpa en enskild besökare. [!DNL Chatlio] använder [!DNL Chatio Zapier App] ansluta [!DNL Chatlio] med över 2 000 olika program och tjänster.

The [!DNL Chatlio] Med -källa kan du importera webbhoaktiviteter som stöds och tillhörande händelsedata från [!DNL Chatlio.com] med [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

De webbhooks som stöds är:

* Exportera chattutskrifter
* Exportera offlinemeddelanden
* Ny konversation har startats
* Besökaren fick inget svar i tid
* Besökaren lämnade feedback efter en chatt

## Förutsättningar {#prerequisites}

Innan du kan skapa en [!DNL Chatlio] måste du först kontrollera att du har följande:

* A [!DNL Chatlio] konto. Om du inte redan har ett besök [[!DNL Chatlio] registreringssida](https://chatlio.com/app/#/signup) för att registrera och skapa ditt konto.
* När du har registrerat ett konto följer du [[!DNL Chatlio] installationsdokumentation](https://chatlio.com/docs/setup/) för att slutföra kontokonfigurationen.

### Inställningar [!DNL Chatlio] webkrok {#set-up-webhook}

När du har skapat dataflödet måste du skapa en webkrok som informerar plattformen om [!DNL Chatlio] händelser. Webbhotell kan meddela dig omedelbart när kundattributen ändras eller när personer öppnar dina meddelanden och skickar informationen till [!DNL Chatlio] källa.

Mer information finns i självstudiekurserna på [hämta URL för direktuppspelningsslutpunkt](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) och [konfigurera [!DNL Chatlio] Webkrok](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Anslut [!DNL Chatlio] till plattform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du skapar en [!DNL Chatlio] direktuppspelningskontakt att ansluta med [!DNL Platform] med API:er eller användargränssnittet:

### Anslut [!DNL Chatlio] till plattform med API:er {#connect-to-platform-using-api}

* [Skapa en källanslutning att hämta [!DNL Chatlio] data till plattformen med API:er.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Anslut [!DNL Chatlio] till plattform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en källanslutning att hämta [!DNL Chatlio] data till plattformen via användargränssnittet](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
