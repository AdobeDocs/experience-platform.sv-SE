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

Direktuppspelning för Adobe Experience Platform ger användarna en metod för att skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att skapa en [!DNL Real-Time Customer Profile] för var och en av era enskilda kunder. Direktinmatning spelar en viktig roll när det gäller att skapa dessa profiler genom att göra det möjligt att leverera [!DNL Profile] data till [!DNL Data Lake] med så lite fördröjning som möjligt.

Följande video är utformad för att hjälpa dig förstå hur man får in strömmande material och beskriver koncepten ovan.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Strömma profilposter och [!DNL ExperienceEvents]

Med direktuppspelningsinmatning kan användarna strömma profilposter och [!DNL ExperienceEvents] till [!DNL Platform] på bara några sekunder för att driva personaliseringen i realtid. Alla data som skickas till direktuppspelnings-API:er sparas automatiskt i [!DNL Data Lake].

Läs [skapa en anslutningsguide för direktuppspelning](../tutorials/create-streaming-connection.md) för mer information.

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för [!DNL Real-Time Customer Profile] och [!DNL Identity Service].

Mer information om hur du aktiverar en datauppsättning för [!DNL Profile] och [!DNL Identity Service], kan du läsa [konfigurera en datauppsättningsguide](../../profile/tutorials/dataset-configuration.md).

## Vilken fördröjning förväntas för direktuppspelad förtäring på Experience Platform?

>[!IMPORTANT]
>
>Guardrails för direktuppspelning beräknas på organisationsnivå och inte på sandlådenivå. Detta innebär att din dataanvändning per sandlåda är bunden till det totala licensanvändningsberättigande som motsvarar hela din organisation. Dessutom är dataanvändningen i utvecklingssandlådor begränsad till 10 % av det totala antalet profiler. Mer information om berättigande för licensanvändning finns i [metodguide för datahantering](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Mål | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 15 minuter vid den 95:e percentilen |
| Data Lake | &lt; 60 minuter |

## Begär per sekund (RPS) - vägledning om direktuppspelad inmatning

Tabellen nedan visar vägledning om gränsen per sekund för direktuppspelning vid begäran.

| RPS-gräns | Anteckningar |
| --- | --- |
| 1 000 begäranden per sekund | Dessa kan innehålla flera meddelanden när de används `/collection/batch` slutpunkt. |
| 10000 enskilda meddelanden per sekund | Meddelandena kan grupperas i färre faktiska förfrågningar när du använder `/collection/batch` slutpunkt. |

>[!IMPORTANT]
>
>Den tvingande gränsen blir **60 begäranden per minut** när synkron validering används som avsett för felsökning.

## Adobe Experience Platform-tillägg

Du kan använda Adobe Experience Platform-tillägget för att skapa en ny direktuppspelningsanslutning. The [!DNL Experience Platform] tillägg innehåller åtgärder för att skicka beacons som är formaterade i [!DNL Experience Data Model] (XDM) för realtidsinmatning till [!DNL Experience Platform]. Besök [Experience Platform-tillägg](../../tags/extensions/client/web-sdk/overview.md) mer information.
