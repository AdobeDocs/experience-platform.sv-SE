---
title: Översikt över granskningsloggar
description: Läs om hur granskningsloggar gör det möjligt för dig att se vilka åtgärder som har utförts i Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 2677d5f0c4369ab692f9e4b16710098a359402d7
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Granskningsloggar (beta)

>[!IMPORTANT]
>
>Granskningsloggfunktionen i Adobe Experience Platform är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

För att öka insynen i och synligheten i de aktiviteter som utförs i systemet kan du med Adobe Experience Platform granska användaraktiviteter för olika tjänster och funktioner i form av &quot;granskningsloggar&quot;. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem på plattformen och hjälpa ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.

I grundläggande bemärkelse anger en granskningslogg **som** utförd **vad** och **när**. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

Det här dokumentet innehåller granskningsloggar i Platform, inklusive hur du visar och hanterar dem i användargränssnittet eller API.

## Händelsetyper som hämtats av granskningsloggar {#category}

Följande tabell visar vilka åtgärder som resurser registreras av granskningsloggar för:

| Resurs | Instruktioner |
| --- | --- |
| [Datauppsättning](../../../catalog/datasets/overview.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li><li>Aktivera för [Kundprofil i realtid](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Klass](../../../xdm/schema/composition.md#class) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Fältgrupp](../../../xdm/schema/composition.md#field-group) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Datatyp](../../../xdm/schema/composition.md#data-type) | <ul><li>Skapa</li><li>Uppdatera</li><li>Ta bort</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Skapa</li><li>Uppdatera</li><li>Återställ</li><li>Ta bort</li></ul> |
| [Destination](../../../destinations/home.md) | <ul><li>Aktivera</li></ul> |

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha **[!UICONTROL View User Activity Log]** behörighet för åtkomstkontroll (finns under [!UICONTROL Data Governance] kategori). Läs mer om hur du hanterar individuella behörigheter för plattformsfunktioner i [dokumentation om åtkomstkontroll](../../../access-control/home.md).

## Hantera granskningsloggar i användargränssnittet

Du kan visa granskningsloggar för olika Experience Platform-funktioner i **[!UICONTROL Audits]** i plattformsgränssnittet. På arbetsytan visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.

![Kontrollpanel för granskningsloggar](../../images/audit-logs/audits.png)

Systemet visar endast granskningsloggar från det senaste året. Loggar som överskrider den här gränsen tas automatiskt bort från systemet.

Välj en händelse i listan om du vill visa information om händelsen i den högra listen.

![Händelseinformation](../../images/audit-logs/select-event.png)

### Filtrera granskningsloggar

Markera trattecknet (![Filterikon](../../images/audit-logs/icon.png)) för att visa en lista med filterkontroller för att begränsa resultatet.

![Filter](../../images/audit-logs/filters.png)

Följande filter är tillgängliga för granskningshändelser i användargränssnittet:

| Filter | Beskrivning |
| --- | --- |
| [!UICONTROL Category] | Använd listrutan för att filtrera de resultat som visas med [kategori](#category). |
| [!UICONTROL Action] | Filtrera efter åtgärd. Endast för närvarande [!UICONTROL Create] och [!UICONTROL Delete] kan filtreras. |
| [!UICONTROL Access Control Status] | Filtrera efter om åtgärden tilläts (slutförd) eller nekades på grund av brist på [åtkomstkontroll](../../../access-control/home.md) behörigheter. |
| [!UICONTROL Date] | Välj ett startdatum och/eller ett slutdatum för att definiera ett datumintervall som resultaten ska filtreras efter. |

Om du vill ta bort ett filter väljer du &quot;X&quot; på ikonen för pilen för filtret i fråga eller väljer **[!UICONTROL Clear all]** om du vill ta bort alla filter.

![Rensa filter](../../images/audit-logs/clear-filters.png)

### Exportera granskningsloggar

Om du vill exportera den aktuella listan med granskningsloggar väljer du **[!UICONTROL Download log]**.

![Hämtningslogg](../../images/audit-logs/download.png)

Välj önskat format i dialogrutan som visas (antingen **[!UICONTROL CSV]** eller **[!UICONTROL JSON]**) och sedan väljer **[!UICONTROL Download]**. Webbläsaren hämtar den genererade filen och sparar den på datorn.

![Välj hämtningsformat](../../images/audit-logs/select-download-format.png)

## Hantera granskningsloggar i API

Alla åtgärder som du kan utföra i användargränssnittet kan också utföras med API-anrop. Se [API-referensdokument](https://www.adobe.io/experience-platform-apis/references/audit-query/) för mer information.

## Hantera granskningsloggar för Adobe Admin Console

Mer information om hur du hanterar granskningsloggar för aktiviteter i Adobe Admin Console finns i följande [dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nästa steg

I den här guiden beskrivs hur du hanterar granskningsloggar i Experience Platform. Mer information om hur du övervakar plattformsaktiviteter finns i dokumentationen om [Insikter om observerbarhet](../../../observability/home.md) och [övervaka datainmatning](../../../ingestion/quality/monitor-data-ingestion.md).
