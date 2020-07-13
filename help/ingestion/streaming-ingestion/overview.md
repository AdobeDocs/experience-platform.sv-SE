---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över Adobe Experience Platform Streaming Ingtion
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Översikt över direktuppspelning

Med direktuppspelningsuppläsning för Adobe Experience Platform kan användare skicka data från klient- och serverenheter till Experience Platform i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en kundprofil i realtid för var och en av era enskilda kunder. Direktuppspelning spelar en viktig roll när det gäller att skapa dessa profiler genom att göra det möjligt för er att leverera profildata till datasjön med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Direktuppspela profilposter och ExperienceEvents

Med direktuppspelningsuppläsning kan användare strömma profilposter och ExperienceEvents till Platform på bara några sekunder för att hjälpa till att driva personaliseringen i realtid. Alla data som skickas till API:er för direktuppspelning bevaras automatiskt i datasjön.

Mer information finns i [Skapa en anslutningsguide](../tutorials/create-streaming-connection.md) för direktuppspelning.

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för kundprofil och identitetstjänst i realtid.

Mer information om hur du aktiverar en datauppsättning för profil- och identitetstjänsten finns i [Konfigurera en datauppsättningsguide](../../profile/tutorials/dataset-configuration.md).

## Vilken fördröjning förväntas för direktuppspelning på Platform?

| Destination | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 1 minut |
| Data Lake | &lt; 60 minuter |

## Adobe Experience Platform

Du kan använda tillägget Adobe Experience Platform för att skapa en ny direktuppspelningsanslutning. Tillägget Experience Platform innehåller åtgärder för att skicka beacons som är formaterade i Experience Data Model (XDM) för realtidsintag till Experience Platform. Mer information finns i dokumentationen för [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .