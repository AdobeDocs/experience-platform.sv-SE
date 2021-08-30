---
title: Översikt över granskningsloggar
description: Läs om hur granskningsloggar gör det möjligt för dig att se vilka åtgärder som har utförts i Adobe Experience Platform.
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Granskningsloggar (beta)

>[!IMPORTANT]
>
>Granskningsloggfunktionen i Adobe Experience Platform är för närvarande i betaversion. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

För att öka insynen i och synligheten i de aktiviteter som utförs i systemet kan du med Adobe Experience Platform granska användaraktiviteter för olika tjänster och funktioner i form av &quot;granskningsloggar&quot;. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem på plattformen och hjälpa ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.

I grundläggande bemärkelse anger en granskningslogg **vem** som utförde **vad**-åtgärden och **när**. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

Det här dokumentet innehåller granskningsloggar i Platform, inklusive hur du visar och hanterar dem i användargränssnittet eller API.

## Händelsetyper som hämtats av granskningsloggar

Följande tabell visar vilka åtgärder som resurser registreras av granskningsloggar för:

| Resurs | Instruktioner |
| --- | --- |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Återställ</li><li>Ta bort</li></ul> |
| [Datauppsättning](../../../catalog/datasets/overview.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li><li>Aktivera för [Kundprofil i realtid](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Fältgrupp](../../../xdm/schema/composition.md#field-group) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Destination](../../../destinations/home.md) | <ul><li>Aktivera</li></ul> |

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha åtkomstkontrollbehörighet för Visa granskningsloggar. Mer information om hur du hanterar individuella behörigheter för plattformsfunktioner finns i [åtkomstkontrollsdokumentationen](../../../access-control/home.md).

## Hantera granskningsloggar i användargränssnittet

Du kan visa granskningsloggar för olika Experience Platform-funktioner på arbetsytan **[!UICONTROL Audits]** i plattformsgränssnittet. På arbetsytan visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.

![Kontrollpanel för granskningsloggar](../../images/audit-logs/audits.png)

Systemet visar endast granskningsloggar från det senaste året. Loggar som överskrider den här gränsen tas automatiskt bort från systemet.

Välj en händelse i listan om du vill visa information om händelsen i den högra listen.

![Händelseinformation](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Hantera granskningsloggar i API

Alla åtgärder som du kan utföra i användargränssnittet kan också utföras med API-anrop. Mer information finns i [API-referensdokumentet](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Hantera granskningsloggar för Adobe Admin Console

Mer information om hur du hanterar granskningsloggar för aktiviteter i Adobe Admin Console finns i följande [dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nästa steg

I den här guiden beskrivs hur du hanterar granskningsloggar i Experience Platform. Mer information om hur du övervakar plattformsaktiviteter finns i dokumentationen om [observabilitetsinsikter](../../../observability/home.md) och [övervakning av datainhämtning](../../../ingestion/quality/monitor-data-ingestion.md).