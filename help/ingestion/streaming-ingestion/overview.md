---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över Ingest om Adobe Experience Platform Streaming
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# Översikt över direktuppspelning

Direktuppspelning för Adobe Experience Platform ger användarna en metod för att skicka data från klient- och serverenheter till Experience Platform i realtid.

## Vad kan du göra med direktuppspelning?

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser genom att generera en kundprofil i realtid för var och en av era enskilda kunder. Direktuppspelning spelar en viktig roll när det gäller att skapa dessa profiler genom att göra det möjligt för er att leverera profildata till datasjön med så lite fördröjning som möjligt.

### Direktuppspela profilposter och ExperienceEvents

Med direktuppspelningsuppläsning kan användarna strömma profilposter och ExperienceEvents till Platform på bara några sekunder för att hjälpa till att driva personaliseringen i realtid. Alla data som skickas till API:er för direktuppspelning bevaras automatiskt i datasjön.

Mer information finns i [Skapa en anslutningsguide](../tutorials/create-streaming-connection.md) för direktuppspelning.

### Strömma till datauppsättningar

När du är säker på att dina data är rena kan du aktivera dina datauppsättningar för kundprofil och identitetstjänst i realtid.

Mer information om hur du aktiverar en datauppsättning för profil- och identitetstjänsten finns i [Konfigurera en datauppsättningsguide](../../profile/tutorials/dataset-configuration.md).

## Vad är den förväntade fördröjningen för direktuppspelning på plattformen?

| Mål | Förväntad fördröjning |
| --------- | ---------------- |
| Kundprofil i realtid | &lt; 1 minut |
| Data Lake | &lt; 60 minuter |

## Adobe Experience Platform-tillägg

Du kan använda Adobe Experience Platform-tillägget för att skapa en ny direktuppspelningsanslutning. Tillägget Experience Platform innehåller åtgärder för att skicka beacons som är formaterade i Experience Data Model (XDM) för realtidsförtäring till Experience Platform. Mer information finns i dokumentationen för [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) .