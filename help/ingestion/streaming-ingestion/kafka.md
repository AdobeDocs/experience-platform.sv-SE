---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kafka-kontakt
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Kafka-kontakt för Adobe Experience Platform

Strömkopplingen för Adobe Experience Platform baseras på Apache Kafka Connect. Det här biblioteket kan användas för att direktuppspela JSON-händelser från Kafka-ämnen i ditt datacenter direkt till Experience Platform i realtid.

Strömkopplingen är en enkelriktad koppling som levererar data från Kafka-avsnitt till en registrerad slutpunkt på Experience Platform. Om du vill använda den här kopplingen måste du hämta biblioteket, lägga till det i din befintliga Kafka-distribution och konfigurera Kafka-avsnitten i Adobe Streaming HTTP URL. Ytterligare kod krävs **inte** . Kopplingen har stöd för följande funktioner:

- Autentiserad datainsamling
- Gruppera meddelanden för att minska nätverksanrop och öka genomströmningen

Mer information om Kafka-anslutningen, inklusive anvisningar om hur du konfigurerar anslutningen, finns i [Komma igång-guiden](https://github.com/adobe/experience-platform-streaming-connect). Mer information om arbetsflödet finns i [utvecklarhandboken](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).