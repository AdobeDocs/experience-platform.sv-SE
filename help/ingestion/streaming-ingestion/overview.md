---
keywords: Experience Platform;hemmabruk;populära ämnen;datainmatning;inmatade data;strömning;översikt;strömningsupptagning;latens;strömningstid;
solution: Experience Platform
title: Direktuppspelning - översikt
description: Direktuppspelning för Adobe Experience Platform ger användare en metod för att skicka data från klient- och serverenheter till Experience Platform i realtid.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: d6424e2a9afc046f4bff329797954fd43939a819
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Översikt över direktuppspelning

Direktuppspelningsuppläsning för Adobe Experience Platform ger användarna en metod för att skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en [!DNL Real-Time Customer Profile] för var och en av era enskilda kunder. Direktuppspelning av inmatning spelar en viktig roll när det gäller att skapa de här profilerna genom att göra det möjligt för dig att leverera [!DNL Profile]-data till [!DNL Data Lake] med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Direktuppspelningsprofilsposter och [!DNL ExperienceEvents]

Med direktuppspelningsinmatning kan användare direktuppspela profilposter och [!DNL ExperienceEvents] till [!DNL Platform] på några sekunder för att hjälpa till att driva personalisering i realtid. Alla data som skickas till API:er för direktuppspelning sparas automatiskt i [!DNL Data Lake].

Mer information finns i [Skapa en anslutningsguide för direktuppspelning](../tutorials/create-streaming-connection.md).

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för [!DNL Real-Time Customer Profile] och [!DNL Identity Service].

Mer information om hur du aktiverar en datauppsättning för [!DNL Profile] och [!DNL Identity Service] finns i [Konfigurera en datauppsättningsguide](../../profile/tutorials/dataset-configuration.md).

## Vilken fördröjning förväntas för direktuppspelad förtäring på Experience Platform?

>[!IMPORTANT]
>
>Guardrails för direktuppspelning beräknas på organisationsnivå och inte på sandlådenivå. Detta innebär att din dataanvändning per sandlåda är bunden till det totala licensanvändningsberättigande som motsvarar hela din organisation. Dessutom är dataanvändningen i utvecklingssandlådor begränsad till 10 % av det totala antalet profiler. Mer information om berättigande för licensanvändning finns i [handboken om bästa praxis för datahantering](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Mål | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 15 minuter vid den 95:e percentilen |
| Data Lake | &lt; 60 minuter |

## Begär per sekund (RPS) - vägledning om direktuppspelad inmatning

Tabellen nedan visar vägledning om gränsen per sekund för direktuppspelning vid begäran.

| RPS-gräns | Anteckningar |
| --- | --- |
| 1 000 begäranden per sekund | Dessa kan innehålla flera meddelanden när `/collection/batch`-slutpunkten används. |
| 10000 enskilda meddelanden per sekund | Meddelandena kan grupperas i färre faktiska begäranden när slutpunkten `/collection/batch` används. |

>[!IMPORTANT]
>
>Den framtvingade gränsen blir **60 begäranden per minut** när synkron validering används som den är avsedd för felsökning.

## Adobe Experience Platform-tillägg

Du kan använda Adobe Experience Platform-tillägget för att skapa en ny direktuppspelningsanslutning. Tillägget [!DNL Experience Platform] innehåller åtgärder för att skicka beacons som är formaterade i [!DNL Experience Data Model] (XDM) för realtidsförtäring till [!DNL Experience Platform]. Mer information finns i dokumentationen för [Experience Platform-tillägget](../../tags/extensions/client/web-sdk/overview.md).
