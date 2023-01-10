---
keywords: Experience Platform;hemmabas;populära ämnen;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka Connector
description: Strömkopplingen för Adobe Experience Platform baseras på Apache Kafka Connect. Det här biblioteket kan användas för att direktuppspela JSON-händelser från Kafka-avsnitt i ditt datacenter direkt till Experience Platform i realtid.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] anslutning för Adobe Experience Platform

Strömkopplingen för Adobe Experience Platform baseras på [!DNL Apache Kafka Connect]. Det här biblioteket kan användas för att direktuppspela JSON-händelser från [!DNL Kafka] ämnen i ditt datacenter direkt till [!DNL Experience Platform] i realtid.

Strömkopplingen är en enkelriktad kontakt som levererar data från [!DNL Kafka] ämnen till en registrerad slutpunkt på [!DNL Experience Platform]. Om du vill använda den här kopplingen måste du hämta biblioteket och lägga till det i din befintliga [!DNL Kafka] och konfigurera [!DNL Kafka] ämne(n) till HTTP-URL:en för direktuppspelning i Adobe. Ytterligare kod är **not** krävs. Kopplingen har stöd för följande funktioner:

- Autentiserad datainsamling
- Gruppera meddelanden för att minska nätverksanrop och öka genomströmningen

Mer information om [!DNL Kafka] anslutningsprogrammet, inklusive instruktioner om hur du konfigurerar anslutningsprogrammet, läs [komma igång-guide](https://github.com/adobe/experience-platform-streaming-connect). Mer information om arbetsflödet finns i [utvecklarhandbok](https://www.adobe.com/go/kafka-connector-developer-guide).
