---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över Adobe Experience Platform Streaming Ingtion
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Översikt över direktuppspelning

Direktuppspelning för Adobe Experience Platform ger användare en metod för att skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en [!DNL Real-time Customer Profile] för varje enskild kund. Direktuppspelning spelar en viktig roll när det gäller att skapa dessa profiler genom att ni kan leverera [!DNL Profile] data till [!DNL Data Lake] servern med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Strömma profilposter och [!DNL ExperienceEvents]

Med direktuppspelningsinmatning kan användare strömma profilposter och [!DNL ExperienceEvents] till [!DNL Platform] på bara några sekunder för att hjälpa till att driva personaliseringen i realtid. Alla data som skickas till API:er för direktuppspelning sparas automatiskt i [!DNL Data Lake].

Mer information finns i [Skapa en anslutningsguide](../tutorials/create-streaming-connection.md) för direktuppspelning.

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för [!DNL Real-time Customer Profile] och [!DNL Identity Service].

Mer information om hur du aktiverar en datauppsättning för [!DNL Profile] och [!DNL Identity Service]finns i [Konfigurera en datauppsättningsguide](../../profile/tutorials/dataset-configuration.md).

## Vilken fördröjning förväntas för direktuppspelad inmatning på [!DNL Platform]?

| Destination | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 1 minut |
| Data Lake | &lt; 60 minuter |

## Adobe Experience Platform

Du kan använda tillägget Adobe Experience Platform för att skapa en ny direktuppspelningsanslutning. Tillägget innehåller åtgärder för att skicka beacons som är formaterade i [!DNL Experience Platform] (XDM) för realtidsintag till [!DNL Experience Data Model] [!DNL Experience Platform]. Mer information finns i dokumentationen för [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .