---
keywords: Experience Platform;hemmabas;populära ämnen;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka Connector
topic: overview
description: Strömkopplingen för Adobe Experience Platform baseras på Apache Kafka Connect. Det här biblioteket kan användas för att direktuppspela JSON-händelser från Kafka-avsnitt i ditt datacenter direkt till Experience Platform i realtid.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# [!DNL Kafka] anslutning för Adobe Experience Platform

Strömkopplingen för Adobe Experience Platform baseras på [!DNL Apache Kafka Connect]. Det här biblioteket kan användas för att direktuppspela JSON-händelser från [!DNL Kafka]-ämnen i ditt datacenter direkt till [!DNL Experience Platform] i realtid.

Strömkopplingen är en envägsanslutning som levererar data från [!DNL Kafka]-ämnen till en registrerad slutpunkt på [!DNL Experience Platform]. Om du vill använda den här kopplingen måste du hämta biblioteket, lägga till det i din befintliga [!DNL Kafka]-distribution och konfigurera [!DNL Kafka]-avsnitten till HTTP-URL:en för Adobe-direktuppspelning. Ytterligare kod **krävs inte**. Kopplingen har stöd för följande funktioner:

- Autentiserad datainsamling
- Gruppera meddelanden för att minska nätverksanrop och öka genomströmningen

Mer information om [!DNL Kafka]-anslutningen, inklusive anvisningar om hur du konfigurerar anslutningen, finns i [guiden ](https://github.com/adobe/experience-platform-streaming-connect) Komma igång. Mer information om arbetsflödet finns i [utvecklarhandboken](https://www.adobe.com/go/kafka-connector-developer-guide).