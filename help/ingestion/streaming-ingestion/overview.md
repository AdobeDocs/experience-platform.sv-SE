---
keywords: Experience Platform;hemmabruk;populära ämnen;datainmatning;inmatade data;strömning;översikt;strömningsupptagning;latens;strömningstid;
solution: Experience Platform
title: Direktuppspelning - översikt
topic-legacy: overview
description: Direktuppspelning för Adobe Experience Platform ger användare en metod för att skicka data från klient- och serverenheter till Experience Platform i realtid.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Översikt över direktuppspelning

Direktuppspelning för Adobe Experience Platform ger användarna en metod för att skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en [!DNL Real-time Customer Profile] för var och en av era enskilda kunder. Direktuppspelning spelar en viktig roll när det gäller att skapa dessa profiler genom att göra det möjligt att leverera [!DNL Profile]-data till [!DNL Data Lake] med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Direktuppspelningsprofilsposter och [!DNL ExperienceEvents]

Med direktuppspelningsinmatning kan användare strömma profilposter och [!DNL ExperienceEvents] till [!DNL Platform] på några sekunder för att hjälpa till att driva personaliseringen i realtid. Alla data som skickas till API:er för direktuppspelning sparas automatiskt i [!DNL Data Lake].

Läs [skapa en guide för direktuppspelad anslutning](../tutorials/create-streaming-connection.md) om du vill ha mer information.

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera datauppsättningarna för [!DNL Real-time Customer Profile] och [!DNL Identity Service].

Mer information om hur du aktiverar en datauppsättning för [!DNL Profile] och [!DNL Identity Service] finns i [konfigurationsguiden](../../profile/tutorials/dataset-configuration.md).

## Vad är den förväntade fördröjningen för direktuppspelad inmatning på [!DNL Platform]?

| Destination | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60=&quot;&quot; minutes=&quot;&quot;> |

## Adobe Experience Platform-tillägg

Du kan använda Adobe Experience Platform-tillägget för att skapa en ny direktuppspelningsanslutning. Tillägget [!DNL Experience Platform] innehåller åtgärder för att skicka beacons som är formaterade i [!DNL Experience Data Model] (XDM) för realtidsinmatning till [!DNL Experience Platform]. Mer information finns i dokumentationen för [Experience Platform Extension](../../tags/extensions/web/sdk/overview.md).
