---
title: Översikt över granskningsloggar
description: Lär dig hur granskningsloggar gör det möjligt för dig att se vilka åtgärder som har utförts och av vem, i Adobe Experience Platform.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 4%

---

# Granskningsloggar {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="De vanligaste åtgärderna"
>abstract="Den här widgeten visar de vanligaste åtgärderna som har vidtagits i Experience Platform inom den valda tidsramen. Om du vill visa en fullständig lista över registrerade åtgärder i Platform väljer du **Granskningar** i den vänstra navigeringen."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="De vanligaste användarna"
>abstract="Den här widgeten visar de användare som har utfört de flesta åtgärderna i Experience Platform inom den valda tidsramen. Om du vill visa en fullständig lista över registrerade åtgärder i Platform väljer du **Granskningar** i den vänstra navigeringen."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Övervaka användaraktiviteter på plattformen"
>abstract="<h2>Beskrivning</h2><p>Du kan övervaka användaraktivitet för olika plattformstjänster och funktioner i form av granskningsloggar. Dessa loggar utgör ett granskningsspår som registrerar <b>vem</b> utförde <b>vad</b>-åtgärden och <b>när</b>. Granskningsloggar kan hjälpa till med felsökningsproblem på plattformen och hjälpa ert företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.</p>"

För att öka insynen i och synligheten i de aktiviteter som utförs i systemet kan du med Adobe Experience Platform granska användaraktiviteter för olika tjänster och funktioner i form av &quot;granskningsloggar&quot;. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem på plattformen och hjälpa ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.

I grundläggande bemärkelse anger en granskningslogg **vem** utförde **vad**-åtgärden och **när**. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

Det här dokumentet innehåller granskningsloggar i Platform, inklusive hur du visar och hanterar dem i användargränssnittet eller API.

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

För att kunna visa och exportera granskningsloggar måste du ha åtkomstkontrollbehörighet **[!UICONTROL View User Activity Log]** (finns under kategorin [!UICONTROL Data Governance]). Mer information om hur du hanterar individuella behörigheter för plattformsfunktioner finns i [åtkomstkontrollsdokumentationen](../../../access-control/home.md).

## Hantera granskningsloggar i användargränssnittet {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instruktioner"
>abstract="<ul><li>Välj <b>Granskningar</b> i den vänstra navigeringen. På arbetsytan Granskningar visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.</li>   <li> Obs! Granskningsloggarna sparas i 365 dagar, varefter de tas bort från systemet. Därför kan du bara gå tillbaka under en period på högst 365 dagar. Om du behöver titta tillbaka på data som är äldre än 365 dagar bör du exportera loggar med en regelbunden gräns för att uppfylla dina interna policykrav. </li><li>Välj en händelse i listan om du vill visa information om händelsen i den högra listen. </li><li>Markera trattsymbolen om du vill visa en lista med filterkontroller för att begränsa resultatet. Endast de 1 000 sista posterna visas, oavsett vilket filter du har valt. </li><li>Om du vill exportera den aktuella listan med granskningsloggar väljer du **Hämta logg**.</li><li>Mer hjälp om den här funktionen finns i <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html">Översikt över granskningsloggar</a> på Experience League.</li></ul>"

Du kan visa granskningsloggar för olika Experience Platform-funktioner på arbetsytan för **[!UICONTROL Audits]** i plattformsgränssnittet. På arbetsytan visas en lista med inspelade loggar. Som standard sorteras de från senaste till senaste.

![Kontrollpanelen Granskningar markerar Granskningar på den vänstra menyn.](../../images/audit-logs/audits.png)

Granskningsloggarna sparas i 365 dagar efter vilka de kommer att tas bort från systemet. Därför kan du bara gå tillbaka under en period på högst 365 dagar. Om du behöver data som är längre än 365 dagar bör du exportera loggar med en regelbunden mellanrum för att uppfylla dina interna policykrav.

Välj en händelse i listan om du vill visa information om händelsen i den högra listen.

![Granskar fliken Aktivitetslogg på kontrollpanelen med panelen med händelseinformation markerad.](../../images/audit-logs/select-event.png)

### Filtrera granskningsloggar

>[!NOTE]
>
>Eftersom det här är en ny funktion går de data som visas endast tillbaka till mars 2022. Beroende på vilken resurs som valts kan tidigare data vara tillgängliga från januari 2022.


Markera trattikonen (![Filterikon](/help/images/icons/filter.png)) om du vill visa en lista med filterkontroller för att begränsa resultatet. Endast de 1000 sista posterna visas oavsett vilket filter du har valt.

![Kontrollpanelen Granskningar med den filtrerade aktivitetsloggen markerad.](../../images/audit-logs/filters.png)

Följande filter är tillgängliga för granskningshändelser i användargränssnittet:

| Filter | Beskrivning |
| --- | --- |
| [!UICONTROL Category] | Använd listrutan för att filtrera resultat som visas efter [kategori](#category). |
| [!UICONTROL Action] | Filtrera efter åtgärd. De åtgärder som är tillgängliga för respektive tjänst visas i resurstabellen ovan. |
| [!UICONTROL User] | Ange det fullständiga användar-ID:t (till exempel `johndoe@acme.com`) som ska filtreras efter användare. |
| [!UICONTROL Status] | Filtrera efter om åtgärden tilläts (slutförd) eller nekades på grund av att [åtkomstkontrollen](../../../access-control/home.md) inte hade behörighet. |
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

### Exportera granskningsloggar

Om du vill exportera den aktuella listan med granskningsloggar väljer du **[!UICONTROL Download log]**.

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

I den här guiden beskrivs hur du hanterar granskningsloggar i Experience Platform. Mer information om hur du övervakar plattformsaktiviteter finns i dokumentationen om [observabilitetsinsikter](../../../observability/home.md) och [övervakning av datainhämtning](../../../ingestion/quality/monitor-data-ingestion.md).

Titta på följande video för att få en bättre förståelse för granskningsloggar i Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
