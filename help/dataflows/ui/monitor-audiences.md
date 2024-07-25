---
description: Lär dig hur du kan övervaka dataflöden under segmentering med användargränssnittet i Experience Platform.
title: Övervaka dataflöden för målgrupper i användargränssnittet
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 0%

---

# Övervaka dataflöden för målgrupper i användargränssnittet

Med segmenteringstjänsten kan du skapa målgrupper genom segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Plattformen tillhandahåller dataflöden för att på ett transparent sätt spåra detta dataflöde från källor till destinationer.

Använd kontrollpanelen för att se en visuell representation av dataaktiviteten inom en målgrupp, inklusive status för datasegmenteringen. I självstudiekursen finns instruktioner om hur du kan använda kontrollpanelen för att övervaka hur data segmenteras i användargränssnittet i Experience Platform, så att du kan spåra status för målgruppsaktivering, utvärdering och exportjobb.

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] samt till [!DNL Destinations].
   - [Dataflöden körs](../../sources/notifications.md): Dataflöden är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
- [Segmentering](../../segmentation/home.md): Med segmentering kan du skapa målgrupper utifrån kundprofildata i realtid.
   - [Aktiveringsjobb](../../destinations/ui/activation-overview.md): Ett aktiveringsjobb används för att aktivera målgruppen till ett angivet mål.
   - [Utvärderingsjobb](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Ett utvärderingsjobb är en asynkron process som utvärderar målgruppen.
   - [Exportera jobb](../../segmentation/api/export-jobs.md): Ett exportjobb är en asynkron process som används för att behålla målgruppsmedlemmar i datauppsättningar.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

## Övervaka målgruppspanelen {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Målgrupper"
>abstract="Målgruppsvyn innehåller information om alla era målgrupper, med ytterligare information om deras aktiverings- och utvärderingsjobb."

Om du vill komma åt kontrollpanelen **[!UICONTROL Audiences]** väljer du **[!UICONTROL Monitoring]** i den vänstra navigeringen. Välj **[!UICONTROL Audiences]**-kortet på sidan **[!UICONTROL Monitoring]**.

![Publikkortet. Information om det senaste utvärderingsjobbet och det senaste exportjobbet visas.](../assets/ui/monitor-audiences/audience-card.png)

På huvudkontrollpanelen **[!UICONTROL Audiences]** visar **[!UICONTROL Audiences]**-kortet status och datum för det senaste utvärderingsjobbet och det senaste exportjobbet.

Instrumentpanelen innehåller mätvärden för både målgrupper och segmenteringsjobb. Som standard visas målgruppsmått för de senaste 24 timmarna på kontrollpanelen. Läs avsnittet [Övervaka segmenteringsjobb](#monitoring-segmentation-jobs-dashboard) om du vill veta mer om vyn för segmenteringsjobb.

>[!IMPORTANT]
>
>För närvarande stöds bara målgrupper som har aktiverats för [gruppmål (filbaserade) ](../../destinations/destination-types.md#file-based) för kontrollpanelen för målgrupper.

![Målgruppspanelen. Information om olika målgrupper i din organisation och sandlåda visas.](../assets/ui/monitor-audiences/audience-dashboard.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Audience name]** | Namnet på publiken. |
| **[!UICONTROL Data type]** | Målgruppens datatyp. Möjliga värden är **[!UICONTROL Customer]**, **[!UICONTROL Account]** och **[!UICONTROL Prospect]**. Du kan visa målgrupper med en viss datatyp genom att använda filtret [!UICONTROL Data type] ovanför kortmenyfliksområdet. |
| **[!UICONTROL Last evaluation timestamp]** | Datum och tid då målgruppens senaste utvärderingsjobb kördes. |
| **[!UICONTROL Last evaluation status]** | Status för målgruppens senaste utvärderingsjobb. Möjliga värden är **[!UICONTROL Success]**, **[!UICONTROL No runs]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Last evaluation method]** | Målgruppens utvärderingsmetod. Eftersom endast gruppsegmentering stöds är det enda möjliga värdet **[!UICONTROL Batch]**. |
| **[!UICONTROL Last evaluation profiles]** | Antalet profiler som utvärderades i målgruppens senaste utvärderingsjobb. |
| **[!UICONTROL Last activation timestamp]** | Datum och tid då målgruppens senaste aktiveringsjobb kördes. |
| **[!UICONTROL Last activation status]** | Status för målgruppens senaste aktiveringsjobb. Möjliga värden är **[!UICONTROL Success]**, **[!UICONTROL No runs]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Last activation identities]** | Antalet identiteter som aktiverades i målgruppens senaste aktiveringsjobb. |
| **[!UICONTROL Last activation destination]** | Namnet på målet som målgruppens senaste aktiveringsjobb aktiverades för. |

Du kan filtrera resultaten till en viss målgrupp och visa dess segmenteringsjobb genom att välja filterikonen (![Filterikonen.](/help/images/icons/filter-add.png)). Segmenteringsjobben sorteras i kronologisk ordning och de senaste segmenteringsjobben visas först.

![Filterikonen är markerad. Om du väljer detta kan du visa segmenteringsjobben för den angivna målgruppen.](../assets/ui/monitor-audiences/filter-audience.png)

Den filtrerade målgruppsdashboard visas. Kortet **[!UICONTROL Audiences]** visar status och datum för det senaste utvärderingsjobbet och det senaste aktiveringsjobbet.

![Publikkortet. Information om det senaste utvärderingsjobbet och det senaste aktiveringsjobbet visas.](../assets/ui/monitor-audiences/specified-audience-card.png)

På kontrollpanelen visas tid och status för de senaste utvärderings- och aktiveringsjobben, en graf som visar antalet profiler för målgruppsutvärderingen och mått för de segmenteringsjobb som kördes. Som standard visas segmenteringsjobbstatistik för de senaste 24 timmarna på kontrollpanelen.

![Den filtrerade målgruppsinstrumentpanelen. Information om de olika segmenteringsjobb som har körts för den här målgruppen visas.](../assets/ui/monitor-audiences/filter-audience.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Job start]** | Datum och tid då segmenteringsjobbet startades. |
| **[!UICONTROL Type]** | Anger segmenteringsjobbets typ. De två jobbtyper som stöds är **aktiverings**- och **utvärderingsjobb**. |
| **[!UICONTROL Job complete]** | Datum och tid när segmenteringsjobbet slutfördes. |
| **[!UICONTROL Processing time]** | Den tid det tog för segmenteringsjobbet att slutföras. |
| **[!UICONTROL Job status]** | Status för segmenteringsjobbet. Värden som stöds är **[!UICONTROL Success]**, **[!UICONTROL In Progress]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Profile count]** | Antalet profiler som segmenteringsjobbet utvärderar. Varje användare ska ha en unik profil. |
| **[!UICONTROL Identity activated]** | Antalet identiteter som segmenteringsjobbet aktiveras för. Varje profil kan ha flera identiteter. En profil kan till exempel ha ett e-postmeddelande, ett telefonnummer och ett förmånsnummer som identiteter. |
| **[!UICONTROL Destination name]** | Namnet på målet som segmenteringsjobbet aktiveras till. |

Du kan filtrera ytterligare till ett specifikt segmenteringsjobb och visa information om det genom att välja filterikonen (![Filterikonen.](/help/images/icons/filter.png)). Det finns två olika sorters segmenteringsjobb som kan filtreras: aktiveringsjobb och utvärderingsjobb.

### Aktiveringsjobbinformation {#activation-job-details}

På informationssidan för körningsinformation för aktiveringsjobb visas information om körningens mått, körningsfel och målgrupper som är relaterade till segmenteringsjobbet. Ett aktiveringsjobb används för att aktivera målgruppen för ett visst mål.

![Kontrollpanelen för aktiveringsjobb. Information om de olika segmenteringsjobb som har körts för den här målgruppen visas.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Profiles received]** | Det totala antalet profiler som tagits emot i aktiveringsflödet. |
| **[!UICONTROL Identities activated]** | Det totala antalet identiteter som aktiverats till målet, baserat på mottagna profiler. |
| **[!UICONTROL Identities excluded]** | Det totala antalet identiteter som uteslöts från att aktiveras till målet, baserat på mottagna profiler. Dessa identiteter kan uteslutas på grund av saknade attribut eller brott mot medgivandet. |
| **[!UICONTROL Size of data]** | Storleken på det dataflöde som aktiveras. |
| **[!UICONTROL Total files]** | Det totala antalet filer som aktiveras i dataflödet. |
| **[!UICONTROL Status]** | Aktiveringsjobbets aktuella status. |
| **[!UICONTROL Dataflow run start]** | Datum och tid då aktiveringsjobbet startades. |
| **[!UICONTROL Dataflow run end]** | Datum och tid då aktiveringsjobbet avslutades. |
| **[!UICONTROL Dataflow run ID]** | ID för det aktuella aktiveringsjobbet. |
| **[!UICONTROL IMS org ID]** | ID för organisationen som aktiveringsjobbet tillhör. |
| **[!UICONTROL Destination name]** | Namnet på målet som data aktiveras till. |

Under målgruppssektionen kan du se en lista över målgrupper som aktiverats som en del av aktiveringsjobbet.

![Kontrollpanelen för aktiveringsjobb. Information om de identiteter som misslyckades eller exkluderades markeras.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Följande värden är tillgängliga för målgruppsavsnittet:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Name]** | Namnet på den målgrupp som aktiverades. |
| **[!UICONTROL Identities activated]** | Det totala antalet identiteter som aktiverats till målet, baserat på mottagna profiler. |
| **[!UICONTROL Identities excluded]** | Det totala antalet identiteter som uteslöts från att aktiveras till målet, baserat på mottagna profiler. Dessa identiteter kan uteslutas på grund av saknade attribut eller brott mot medgivandet. |
| **[!UICONTROL Last dataflow run status]** | Status för det senaste aktiveringsjobbet som kördes för den målgruppen. |
| **[!UICONTROL Last dataflow run date]** | Datum och tid för det senaste aktiveringsjobbet som kördes för den målgruppen. |

Dessutom kan du visa information om körningsfel i dataflödet. Under avsnittet med fel vid körning av dataflöde kan du visa både de identiteter som misslyckades eller de identiteter som uteslöts. Felavsnittet innehåller information om felkoden och antalet identiteter som misslyckats eller utelämnats.

![Kontrollpanelen för aktiveringsjobb. Information om de identiteter som misslyckades eller exkluderades markeras.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Information om utvärderingsjobb {#evaluation-job-details}

Sidan med information om körningsinformation för utvärderingsjobbdata visar information om körningens mått och målgrupper som är relaterade till segmenteringsjobbet.

![Kontrollpanelen för utvärderingsjobbet. Information om målgruppens utvärderingsjobb visas.](../assets/ui/monitor-audiences/evaluation-job-details.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | Det totala antalet profiler som utvärderas. |
| **[!UICONTROL Status]** | Utvärderingsjobbets status. Möjliga statusar för utvärderingsjobbet är **[!UICONTROL Success]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Job start]** | Datum och tid då utvärderingsjobbet startades. |
| **[!UICONTROL Job end]** | Datum och tid då utvärderingsjobbet avslutades. |
| **[!UICONTROL Job type]** | Typ av segmenteringsjobb. I det här fallet är det alltid ett **[!UICONTROL Segment evaluation]**-jobb. |
| **[!UICONTROL Evaluation type]** | Typen av utvärdering som görs. Detta kan vara antingen **[!UICONTROL Batch]** eller **[!UICONTROL Streaming]**. |
| **[!UICONTROL Job ID]** | ID för utvärderingsjobbet. |
| **[!UICONTROL IMS org ID]** | ID:t för organisationen som utvärderingsjobbet tillhör. |
| **[!UICONTROL Audience name]** | Namnet på den målgrupp som utvärderas. |
| **[!UICONTROL Audience ID]** | ID för den målgrupp som utvärderas. |

Under avsnittet [!UICONTROL Audiences] kan du se en lista över målgrupper som utvärderas som en del av utvärderingsjobbet. Du kan filtrera listan över målgrupper efter namn med hjälp av sökfältet.

>[!IMPORTANT]
>
>Den här instrumentpanelsvyn har stöd för upp till 800 målgruppsmått.

Följande mått är tillgängliga för avsnittet [!UICONTROL Audiences]:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Name]** | Namnet på den målgrupp som utvärderas. |
| **[!UICONTROL Profile count]** | Antalet profiler som utvärderas. |

## Kontrollpanel för segmenteringsjobb {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmenteringsjobb"
>abstract="Vyn för segmenteringsjobb innehåller information om utvärderings- och exportjobb för alla era målgrupper."

Om du vill komma åt kontrollpanelen **[!UICONTROL Segmentation Jobs]** väljer du **[!UICONTROL Segmentation jobs]** på kontrollpanelen [!UICONTROL Audiences]. Kontrollpanelen [!UICONTROL Monitoring] innehåller mått och information om utvärderings- och exportjobb.

>[!NOTE]
>
>Endast **segmenteringsutvärderingsjobb** stöds för övervakning per målgrupp. Segmenteringsexportjobb har endast stöd för övervakning på organisationsnivå.

![Kontrollpanelen för segmenteringsjobbövervakning visas. Växlingen mellan målgrupps- och segmenteringsjobb är markerad.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Använd kontrollpanelen [!UICONTROL Segmentation Jobs] för att förstå om profilutvärdering och -export sker i tid och utan några undantag, så att de underordnade tjänsterna för målaktivering kan ha de senaste utvärderade profildata.

Följande mått är tillgängliga för segmenteringsjobb:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Segmentation job]** | Anger segmenteringsjobbets namn. |
| **[!UICONTROL Type]** | Anger segmenteringstypen - export eller utvärdering. Observera att i båda fallen utvärderar eller exporterar segmenteringsjobbet **alla** målgrupper som tillhör en organisation. Läs guiden om slutpunkten för [exportjobb](../../segmentation/api/export-jobs.md) om du vill veta mer om exportjobb. Om du vill veta mer om utvärderingsjobb kan du läsa självstudiekursen [som utvärderar en segmentdefinition](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | Datum och tid då segmenteringsjobbet startades. |
| **[!UICONTROL Job end]** | Datum och tid när segmenteringsjobbet slutfördes. |
| **[!UICONTROL Status]** | Status för det slutförda jobbet. Möjliga statusar för segmenteringsjobbet kan vara om det lyckades eller misslyckades. |
