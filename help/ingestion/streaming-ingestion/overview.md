---
keywords: Experience Platform;hem;populära ämnen;datainmatning;inmatade data;strömning;översikt;strömningsupptagning;latens;strömningstid;
solution: Experience Platform
title: Direktuppspelning - översikt
description: Läs mer om direktuppspelning i Adobe Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 568208c9b2cb774bbbeed74ae2d456c87e99bca9
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Översikt över direktuppspelning

Direktuppspelning för Adobe Experience Platform ger användarna en metod för att skicka data från klient- och serverenheter till Experience Platform i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en kundprofil i realtid för var och en av era enskilda kunder. Direktuppspelning spelar en viktig roll när det gäller att bygga upp dessa profiler genom att göra det möjligt för er att leverera profildata i sjön med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Direktuppspelningsprofilsposter och [!DNL ExperienceEvents]

Med direktuppspelningsinmatning kan användare strömma profilposter och [!DNL ExperienceEvents] till Experience Platform på några sekunder för att hjälpa till att driva personalisering i realtid. Alla data som skickas till API:er för direktuppspelning bevaras automatiskt i datasjön.

Mer information finns i [Skapa en anslutningsguide för direktuppspelning](../tutorials/create-streaming-connection.md).

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för kundprofilen i realtid och [!DNL Identity Service].

Mer information om hur du aktiverar en datauppsättning för profilen och [!DNL Identity Service] finns i [Konfigurera en datauppsättningsguide](/help/profile/tutorials/dataset-configuration.md).

## Vilken fördröjning förväntas för direktuppspelning på Experience Platform?

>[!IMPORTANT]
>
>Garantier för direktuppspelning är bundna till det totala licensanvändningsberättigande som motsvarar hela organisationen. Dessutom är dataanvändningen i utvecklingssandlådor begränsad till 10 % av det totala antalet profiler. Mer information om berättigande för licensanvändning finns i [handboken om bästa praxis för datahantering](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Läs [Översikt över kapacitet](../../landing/license-usage-and-guardrails/capacity.md) om du vill lära dig hur du ställer in gränser för ditt strömmande flöde.

| Mål | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | <ul><li>&lt; 15 minuter vid den 95:e percentilen för B2C-datainmatning.</li><li>&lt; 30 minuter vid den 95:e percentilen för B2B-datainmatning.</li></ul> |
| Data Lake | &lt; 60 minuter |

## Begär per sekund (RPS) - vägledning om direktuppspelad inmatning

Tabellen nedan visar vägledning om gränsen per sekund för direktuppspelning vid begäran.

| RPS-gräns | Anteckningar |
| --- | --- |
| 1 000 begäranden per sekund | Dessa kan innehålla flera meddelanden när `/collection/batch`-slutpunkten används. |
| 10000 enskilda meddelanden per sekund | Meddelandena kan grupperas i färre faktiska begäranden när slutpunkten `/collection/` används. |

>[!IMPORTANT]
>
>Den framtvingade gränsen blir **60 begäranden per minut** när synkron validering används som den är avsedd för felsökning.

## Adobe Experience Platform-tillägg

Du kan använda Adobe Experience Platform-tillägget för att skapa en ny direktuppspelningsanslutning. Tillägget [!DNL Experience Platform] innehåller åtgärder för att skicka beacons som är formaterade i [!DNL Experience Data Model] (XDM) för realtidsförtäring till [!DNL Experience Platform]. Mer information finns i dokumentationen för [Experience Platform Extension](/help/tags/extensions/client/web-sdk/overview.md).
