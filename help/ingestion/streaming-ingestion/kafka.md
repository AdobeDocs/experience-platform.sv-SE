---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka-kontakt
topic: overview
description: Strömkopplingen för Adobe Experience Platform baseras på Apache Kafka Connect. Det här biblioteket kan användas för att direktuppspela JSON-händelser från Kafka-avsnitt i ditt datacenter direkt till Experience Platform i realtid.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# [!DNL Kafka] anslutning för Adobe Experience Platform

Strömkopplingen för Adobe Experience Platform baseras på [!DNL Apache Kafka Connect]. Det här biblioteket kan användas för att direktuppspela JSON-händelser från [!DNL Kafka] ämnen i ditt datacenter direkt till [!DNL Experience Platform] i realtid.

Strömkopplingen är en enkelriktad koppling som levererar data från [!DNL Kafka] ämnen till en registrerad slutpunkt på [!DNL Experience Platform]. Om du vill använda den här kopplingen måste du hämta biblioteket, lägga till det i din befintliga [!DNL Kafka] distribution och konfigurera [!DNL Kafka] avsnitten till HTTP-URL:en för direktuppspelning i Adobe. Ytterligare kod krävs **inte** . Kopplingen har stöd för följande funktioner:

- Autentiserad datainsamling
- Gruppera meddelanden för att minska nätverksanrop och öka genomströmningen

Mer information om [!DNL Kafka] anslutningen, inklusive anvisningar om hur du konfigurerar anslutningen, finns i guiden [](https://github.com/adobe/experience-platform-streaming-connect)Komma igång. Mer information om arbetsflödet finns i [utvecklarhandboken](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).