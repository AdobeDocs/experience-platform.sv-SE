---
keywords: Experience Platform;hemmabas;populära ämnen;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka Connector
description: Strömkopplingen för Adobe Experience Platform baseras på Apache Kafka Connect. Det här biblioteket kan användas för att direktuppspela JSON-händelser från Kafka-avsnitt i ditt datacenter direkt till Experience Platform i realtid.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# [!DNL Kafka]-anslutning för Adobe Experience Platform

Dataströmsanslutningen för Adobe Experience Platform baseras på [!DNL Apache Kafka Connect]. Det här biblioteket kan användas för att direktuppspela JSON-händelser från [!DNL Kafka] ämnen i ditt datacenter direkt till [!DNL Experience Platform] i realtid.

Strömkopplingen är en envägsanslutning som levererar data från [!DNL Kafka] ämnen till en registrerad slutpunkt på [!DNL Experience Platform]. Om du vill använda den här kopplingen måste du hämta biblioteket, lägga till det i din befintliga [!DNL Kafka]-distribution och konfigurera [!DNL Kafka]-avsnitten till HTTP-URL:en för Adobe-direktuppspelning. Ytterligare kod krävs **inte**. Kopplingen stöder följande funktioner:

- Autentiserad datainsamling
- Gruppera meddelanden för att minska nätverksanrop och öka genomströmningen

Mer information om [!DNL Kafka]-anslutningen, inklusive anvisningar om hur du konfigurerar anslutningen, finns i [Komma igång-guiden](https://github.com/adobe/experience-platform-streaming-connect). Mer information om arbetsflödet finns i [utvecklarhandboken](https://www.adobe.com/go/kafka-connector-developer-guide).
