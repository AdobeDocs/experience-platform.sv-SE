---
title: Översikt över granskningsloggar
description: Lär dig hur granskningsloggar gör det möjligt för dig att se vilka åtgärder som har utförts och av vem, i Adobe Experience Platform.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 3%

---

# Granskningsloggar {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="De vanligaste åtgärderna"
>abstract="Den här widgeten visar de vanligaste åtgärderna som har vidtagits i Experience Platform inom den valda tidsramen. Om du vill visa en fullständig lista över inspelade åtgärder i Experience Platform väljer du **Granskningar** i den vänstra navigeringen."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="De vanligaste användarna"
>abstract="Den här widgeten visar de användare som har utfört de flesta åtgärderna i Experience Platform inom den valda tidsramen. Om du vill visa en fullständig lista över inspelade åtgärder i Experience Platform väljer du **Granskningar** i den vänstra navigeringen."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Övervaka användaraktiviteter i Experience Platform"
>abstract="<h2>Beskrivning</h2><p>Du kan övervaka användaraktiviteten för olika Experience Platform-tjänster och funktioner i form av granskningsloggar. Dessa loggar utgör ett granskningsspår som registrerar <b>vem</b> utförde <b>vad</b>-åtgärden och <b>när</b>. Granskningsloggar kan hjälpa till med felsökningsproblem på Experience Platform och hjälpa ert företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.</p>"

För att öka insynen i och synligheten i de aktiviteter som utförs i systemet kan du med Adobe Experience Platform granska användaraktiviteter för olika tjänster och funktioner i form av &quot;granskningsloggar&quot;. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökning på Experience Platform och hjälpa ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.

I grundläggande bemärkelse anger en granskningslogg **vem** utförde **vad**-åtgärden och **när**. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

När en användare utför en åtgärd registreras två typer av granskningshändelser. En core-händelse hämtar auktoriseringsresultatet för åtgärden, [!UICONTROL allow] eller [!UICONTROL deny], medan en förbättrad händelse hämtar körningsresultatet, [!UICONTROL success] eller [!UICONTROL failure]. Flera förbättrade händelser kan länkas till samma viktiga händelse. När du t.ex. aktiverar ett mål registreras behörigheten för åtgärden [!UICONTROL Destination Update] av huvudhändelsen, medan de förbättrade händelserna registrerar flera [!UICONTROL Segment Activate]-åtgärder.

>[!NOTE]
>
> Metadata för åtgärderna **Lägg till användare** och **Ta bort användare** i **rollen**-resursen kommer inte att innehålla e-post-ID:t för den användare som utförde åtgärden. Loggarna visar i stället systemgenererat e-post-ID (system@adobe.com).

Det här dokumentet innehåller granskningsloggar i Experience Platform, inklusive hur du visar och hanterar dem i användargränssnittet eller API.

## Händelsetyper som hämtats av granskningsloggar {#category}

Följande tabell visar vilka åtgärder som resurser registreras av granskningsloggar för:

| Resurs | Instruktioner |
| --- | --- |
| [Åtkomstkontrollprincip (attributbaserad åtkomstkontroll)](../../../access-control/home.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Konto (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Attribution AI-instans](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera</li><li>Inaktivera</li></ul> |
| [Granskningsloggar](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportera</li></ul> |
| [Klass](../../../xdm/schema/composition.md#class) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| Beräknat attribut | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Kund-AI-instans](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera</li><li>Inaktivera</li></ul> |
| [Datauppsättning](../../../catalog/datasets/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera för [kundprofil i realtid](../../../profile/home.md)</li><li>Inaktivera för profil</li><li>Lägg till data</li><li>Ta bort batch</li></ul> |
| [Datastream](../../../datastreams/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera</li><li>Inaktivera</li><li>[Redigera mappning](../../../datastreams/data-prep.md)</li></ul> |
| [Datatyper](../../../xdm/schema/composition.md#data-type) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Mål](../../../destinations/home.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera</li><li>Inaktivera</li><li>Aktivera datauppsättning</li><li>Ta bort datauppsättning</li><li>Aktivera profil</li><li>Ta bort profil</li></ul> |
| [Fältgrupp](../../../xdm/schema/composition.md#field-group) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Identitetsdiagram](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Visa</li></ul> |
| [Identitetsnamnområde](../../../identity-service/features/namespaces.md) | <ul><li>Skapa</li><li>Uppdatering</li></ul> |
| [Kopplingsprincip](../../../profile/merge-policies/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Produktprofil](../../../access-control/home.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Fråga](../../../query-service/ui/overview.md) | <ul><li>Kör</li></ul> |
| [Frågemall](../../../query-service/ui/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Roll (attributbaserad åtkomstkontroll)](../../../access-control/home.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Lägg till användare</li><li>Ta bort användare</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Återställ</li><li>Ta bort</li></ul> |
| [Schemalagd fråga](../../../query-service/ui/overview.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera för profil</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Skapa</li><li>Ta bort</li><li>Aktivera segment</li><li>Ta bort segment</li></ul> |
| [Source-dataflöde](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Skapa</li><li>Uppdatering</li><li>Ta bort</li><li>Aktivera</li><li>Inaktivera</li><li>Aktivera datauppsättning</li><li>Ta bort datauppsättning</li><li>Profil aktiverad</li><li>Ta bort profil</li></ul> |
| [Arbetsorder](../../../hygiene/home.md) | <ul><li>Skapa</li></ul> |

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha åtkomstkontrollbehörighet **[!UICONTROL View User Activity Log]** (finns under kategorin [!UICONTROL Data Governance]). Mer information om hur du hanterar enskilda behörigheter för Experience Platform-funktioner finns i [åtkomstkontrollsdokumentationen](../../../access-control/home.md).

## Hantera granskningsloggar i användargränssnittet {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instruktioner"
>abstract="<ul><li>Välj <b>Granskningar</b> i den vänstra navigeringen. På arbetsytan Granskningar visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.</li>   <li> Obs! Granskningsloggarna sparas i 365 dagar, varefter de tas bort från systemet. Därför kan du bara gå tillbaka under en period på högst 365 dagar. Om du behöver titta tillbaka på data som är äldre än 365 dagar bör du exportera loggar med en regelbunden gräns för att uppfylla dina interna policykrav. </li><li>Välj en händelse i listan om du vill visa information om händelsen i den högra listen. </li><li>Markera trattsymbolen om du vill visa en lista med filterkontroller för att begränsa resultatet. Endast de 1 000 sista posterna visas, oavsett vilket filter du har valt. </li><li>Om du vill exportera den aktuella listan med granskningsloggar väljer du **Hämta logg**.</li><li>Mer hjälp om den här funktionen finns i <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html">Översikt över granskningsloggar</a> på Experience League.</li></ul>"

Du kan visa granskningsloggar för olika Experience Platform-funktioner på arbetsytan **[!UICONTROL Audits]** i Experience Platform användargränssnitt. På arbetsytan visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.

![Kontrollpanelen Granskningar markerar Granskningar på den vänstra menyn.](../../images/audit-logs/audits.png)

Granskningsloggarna sparas i 365 dagar efter vilka de kommer att tas bort från systemet. Om du behöver data som är längre än 365 dagar bör du exportera loggar med en regelbunden mellanrum för att uppfylla dina interna policykrav.

Metoden för att begära granskningsloggar ändrar den tillåtna tidsperioden och antalet poster som du har åtkomst till. [Med export av loggar](#export-audit-logs) kan du gå tillbaka 365 dagar (i 90-dagarsintervall) till maximalt 10 000 granskningsloggar (antingen core eller enhanced), där [aktivitetsloggens gränssnitt](#filter-audit-logs) i Experience Platform visar de senaste 90 dagarna upp till maximalt 1 000 kärnhändelser, var och en med motsvarande förbättrade händelser.

Välj en händelse i listan om du vill visa information om händelsen i den högra listen.

![Granskar fliken Aktivitetslogg på kontrollpanelen med panelen med händelseinformation markerad.](../../images/audit-logs/select-event.png)

### Filtrera granskningsloggar

Markera trattikonen (![Filterikon](/help/images/icons/filter.png)) om du vill visa en lista med filterkontroller för att begränsa resultatet.

>[!NOTE]
>
>Experience Platform-gränssnittet visar bara de senaste 90 dagarna upp till högst 1 000 kärnhändelser, var och en med motsvarande förbättrade händelser, oavsett vilka filter som används. Om du behöver fler loggar än så (högst 365 dagar) måste du [exportera dina granskningsloggar](#export-audit-logs).

![Kontrollpanelen Granskningar med den filtrerade aktivitetsloggen markerad.](../../images/audit-logs/filters.png)

Följande filter är tillgängliga för granskningshändelser i användargränssnittet:

| Filter | Beskrivning |
| --- | --- |
| [!UICONTROL Category] | Använd listrutan för att filtrera resultat som visas efter [kategori](#category). |
| [!UICONTROL Action] | Filtrera efter åtgärd. De åtgärder som är tillgängliga för respektive tjänst visas i resurstabellen ovan. |
| [!UICONTROL User] | Ange det fullständiga användar-ID:t (till exempel `johndoe@acme.com`) som ska filtreras efter användare. |
| [!UICONTROL Status] | Filtrera granskningshändelser efter resultat: lyckades, misslyckades, tilläts eller nekades på grund av att [åtkomstkontrollen](../../../access-control/home.md) saknar behörighet. Kärnhändelser visar [!UICONTROL Allow] eller [!UICONTROL Deny] för en utförd åtgärd. När kärnhändelsen är [!UICONTROL Allow] kan den ha bifogat en eller flera förbättrade händelser som visar **[!UICONTROL Success]** eller **[!UICONTROL Failure]**. En lyckad åtgärd visar till exempel [!UICONTROL Allow] för kärnhändelsen och [!UICONTROL Success] för den bifogade förbättrade händelsen. |
| [!UICONTROL Date] | Välj ett startdatum och/eller ett slutdatum för att definiera ett datumintervall som resultaten ska filtreras efter. Data kan exporteras med en 90-dagars uppslagsperiod (till exempel 2021-12-15 till 2022-03-15). Detta kan skilja sig åt beroende på händelsetyp. |

Om du vill ta bort ett filter väljer du X på ikonen för piller för filtret i fråga eller väljer **[!UICONTROL Clear all]** om du vill ta bort alla filter.

![Kontrollpanelen för granskningar med ett tydligt filter markerat.](../../images/audit-logs/clear-filters.png)

Returnerade granskningsloggdata innehåller följande information om alla frågor som uppfyller de valda filtervillkoren.

| Kolumnnamn | Beskrivning |
|---|---|
| [!UICONTROL Timestamp] | Exakt datum och tid för åtgärden som utfördes i formatet `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Asset Name] | Värdet för fältet [!UICONTROL Asset Name] beror på vilken kategori som valts som ett filter. |
| [!UICONTROL Category] | Det här fältet matchar den kategori som har valts i listrutan för filter. |
| [!UICONTROL Action] | Vilka åtgärder som är tillgängliga beror på vilken kategori som valts som filter. |
| [!UICONTROL User] | Det här fältet innehåller användar-ID:t som körde frågan. |

![Kontrollpanelen Granskningar med den filtrerade aktivitetsloggen markerad.](../../images/audit-logs/filtered.png)

### Exportera granskningsloggar {#export-audit-logs}

Om du vill exportera den aktuella listan med granskningsloggar väljer du **[!UICONTROL Download log]**.

>[!NOTE]
>
>Loggar kan begäras i 90 dagars intervall upp till 365 dagar tidigare. Det maximala antalet loggar som kan returneras under en enskild export är emellertid 10 000 granskningshändelser (antingen kärnhändelser eller förbättrat).

![Kontrollpanelen Granskningar med [!UICONTROL Download log] markerat.](../../images/audit-logs/download.png)

Välj önskat format (antingen **[!UICONTROL CSV]** eller **[!UICONTROL JSON]**) i dialogrutan som visas och välj sedan **[!UICONTROL Download]**. Webbläsaren hämtar den genererade filen och sparar den på datorn.

![Dialogrutan för val av filformat med [!UICONTROL Download] markerat.](../../images/audit-logs/select-download-format.png)

## Aktivera aviseringar {#enable-alerts}

Du kan aktivera granskningsmeddelanden om du vill få meddelanden om följande regler:

* Skapa målgrupp
* Målgruppsuppdatering
* Målgruppsborttagning
* Skapa datauppsättning
* Uppdatering av datauppsättning
* Ta bort datauppsättning
* Skapa schema
* Schemauppdatering
* Ta bort schema

Välj önskad avisering i listan för att prenumerera och få meddelanden. Mer information om varningar finns i guiden om att [prenumerera på varningar med användargränssnittet](../../../observability/alerts/ui.md).

## Hantera granskningsloggar i API

Alla åtgärder som du kan utföra i användargränssnittet kan också utföras med API-anrop. Mer information finns i [API-referensdokumentet](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Hantera granskningsloggar för Adobe Admin Console

Mer information om hur du hanterar granskningsloggar för aktiviteter i Adobe Admin Console finns i följande [dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nästa steg och ytterligare resurser

I den här guiden beskrivs hur du hanterar granskningsloggar i Experience Platform. Mer information om hur du övervakar Experience Platform-aktiviteter finns i dokumentationen om [Insikter om observabilitet](../../../observability/home.md) och [övervakning av datainhämtning](../../../ingestion/quality/monitor-data-ingestion.md).

Titta på följande video för att få en bättre förståelse för granskningsloggar i Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
