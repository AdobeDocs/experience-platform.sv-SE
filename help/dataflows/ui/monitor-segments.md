---
keywords: Experience Platform;hem;populära ämnen;övervakningssegment;övervaka dataflöden;dataflöden;segmentering
description: Med segmentering kan ni skapa segment och målgrupper utifrån era kundprofildata i realtid. I den här självstudiekursen finns anvisningar om hur du kan övervaka dataflöden under segmentering med användargränssnittet i Experience Platform.
title: Övervaka dataflöden för segment i användargränssnittet
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 0%

---

# Övervaka dataflöden för segment i användargränssnittet

Med segmenteringstjänsten kan ni skapa segment och målgrupper utifrån kundprofildata i realtid i Adobe Experience Platform. Plattformen tillhandahåller dataflöden för att på ett transparent sätt spåra detta dataflöde från källor till destinationer.

Kontrollpanelen ger dig en visuell representation av dataaktiviteten inom ett segment, inklusive status för datasegmenteringen. I den här självstudiekursen får du anvisningar om hur du kan använda kontrollpanelen för att övervaka datasegmenteringen med användargränssnittet i Experience Platform, så att du kan spåra statusen för segmentaktivering, utvärdering och exportjobb.

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras över olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar till [!DNL Identity] och [!DNL Profile]och till [!DNL Destinations].
   - [Dataflödeskörningar](../../sources/notifications.md): Dataflödeskörningar är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
- [Segmentering](../../segmentation/home.md): Med segmentering kan ni skapa segment och målgrupper utifrån era kundprofildata i realtid.
   - [Aktiveringsjobb](../../destinations/ui/activation-overview.md): Ett aktiveringsjobb används för att aktivera ditt segment till en angiven destination.
   - [Utvärderingsjobb](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Ett utvärderingsjobb är en asynkron process som kör skapar ett målgruppssegment baserat på det angivna segmentet.
   - [Exportera jobb](../../segmentation/api/export-jobs.md): Ett exportjobb är en asynkron process som används för att behålla målgruppsmedlemmar i datauppsättningar.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

## Kontrollpanel för segment {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segment"
>abstract="Vyn Segment innehåller information om alla IMS-organisationens segment, med ytterligare information om aktiverings- och utvärderingsjobben."

Så här öppnar du **[!UICONTROL Segments]** kontrollpanel, välja **[!UICONTROL Monitoring]** i den vänstra navigeringen. På **[!UICONTROL Monitoring]** väljer du **[!UICONTROL Segments]** kort.

![Segmentkortet. Information om det senaste utvärderingsjobbet och det senaste exportjobbet visas.](../assets/ui/monitor-segments/segment-card-monitoring.png)

På vänster sida **[!UICONTROL Segments]** kontrollpanelen, **[!UICONTROL Segments]** visas status och datum för det senaste utvärderingsjobbet och det senaste exportjobbet.

Instrumentpanelen innehåller mätvärden för både segment och segmentjobb. Som standard visas segmentvärdena för de senaste 24 timmarna på kontrollpanelen. Om du vill veta mer om segmentjobbvyn kan du läsa [övervaka segmentjobb](#monitoring-segment-jobs-dashboard) -avsnitt.

>[!IMPORTANT]
>
>För närvarande är det bara segment som aktiveras för [batchvis (filbaserat) mål](../../destinations/destination-types.md#file-based) stöds för kontrollpanelen för övervakningssegment.

![Segmentkontrollpanelen. Information om de olika segmenten i IMS-organisationen och sandlådan visas.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Segment name]** | Segmentets namn. |
| **[!UICONTROL Last evaluation timestamp]** | Datum och tid då segmentets senaste utvärderingsjobb kördes. |
| **[!UICONTROL Last evaluation status]** | Status för segmentets senaste utvärderingsjobb. Möjliga värden är **[!UICONTROL Success]**, **[!UICONTROL No runs]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Last evaluation profiles]** | Antalet profiler som utvärderades i segmentets senaste utvärderingsjobb. |
| **[!UICONTROL Last activation timestamp]** | Datum och tid då segmentets senaste aktiveringsjobb kördes. |
| **[!UICONTROL Last activation status]** | Status för segmentets senaste aktiveringsjobb. Möjliga värden är **[!UICONTROL Success]**, **[!UICONTROL No runs]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Last activation identities]** | Antalet identiteter som aktiverades i segmentets senaste aktiveringsjobb. |
| **[!UICONTROL Last activation destination]** | Namnet på målet som segmentets senaste aktiveringsjobb aktiverades för. |

Du kan filtrera resultaten till ett specifikt segment och visa segmentjobben genom att välja filterikonen (![Filterikonen.](../assets/ui/monitor-segments/filter-icon.png)). Segmentjobben sorteras i kronologisk ordning och de senaste segmentjobben visas först.

![Filterikonen är markerad. Om du väljer det här alternativet kan du visa segmentjobben för det angivna segmentet.](../assets/ui/monitor-segments/filter-segment.png)

Den filtrerade segmentkontrollpanelen visas. The **[!UICONTROL Segments]** visar status och datum för det senaste utvärderingsjobbet och det senaste aktiveringsjobbet.

![Segmentkortet. Information om det senaste utvärderingsjobbet och det senaste aktiveringsjobbet visas.](../assets/ui/monitor-segments/specified-segment-card.png)

På kontrollpanelen visas tid och status för de senaste utvärderings- och aktiveringsjobben, ett diagram som visar antalet profiler för segmentutvärderingen och mått för segmentjobben som kördes. Som standard visas segmentjobbstatistik för de senaste 24 timmarna på kontrollpanelen.

![Den filtrerade segmentkontrollpanelen. Information om de olika segmentjobben som har körts för det här segmentet visas.](../assets/ui/monitor-segments/filter-specified-segment.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Job start]** | Datum och tid då segmentjobbet startades. |
| **[!UICONTROL Type]** | Anger segmentjobbets typ. De två jobbtyperna som stöds är **aktivering** och **utvärdering** jobb. |
| **[!UICONTROL Job complete]** | Datum och tid då segmentjobbet slutfördes. |
| **[!UICONTROL Processing time]** | Den tid det tog för segmentjobbet att slutföras. |
| **[!UICONTROL Job status]** | Segmentjobbets status. Värden som stöds är **[!UICONTROL Success]**, **[!UICONTROL In Progress]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Profile count]** | Antalet profiler som segmentjobbet utvärderar. Varje användare ska ha en unik profil. |
| **[!UICONTROL Identity count]** | Antalet identiteter som segmentjobbet aktiveras för. Varje profil kan ha flera identiteter. En profil kan till exempel ha ett e-postmeddelande, ett telefonnummer och ett förmånsnummer som identiteter. |
| **[!UICONTROL Destination name]** | Namnet på målet som segmentjobbet aktiveras till. |

Du kan filtrera ytterligare till ett specifikt segmentjobb och visa information om det genom att välja filterikonen (![Filterikonen.](../assets/ui/monitor-segments/filter-icon.png)). Det finns två olika typer av segmentjobb som kan filtreras: aktiveringsjobb och utvärderingsjobb.

### Aktiveringsjobbinformation {#activation-job-details}

På sidan med information om körningsinformation för aktiveringsjobb visas information om körningens mått, körningsfel och segment som är relaterade till segmentjobbet. Ett aktiveringsjobb används för att aktivera ditt segment för en angiven destination. Som standard visas felen vid körning av dataflödet på informationssidan.

![Den filtrerade segmentkontrollpanelen. Information om de olika segmentjobben som har körts för det här segmentet visas.](../assets/ui/monitor-segments/activation-job-details.png)

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
| **[!UICONTROL IMS org ID]** | ID för den IMS-organisation som aktiveringsjobbet tillhör. |
| **[!UICONTROL Destination name]** | Namnet på målet som data aktiveras till. |

Under mätvärdena visas en växel som du kan använda för att välja mellan körningsfel i dataflödet och segmenten.

![Kontrollpanelen för filtrerade segment. Den växel som används för att växla mellan dataflödeskörningsfel och segmentvisningen markeras.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

Under avsnittet med fel vid körning av dataflöde väljer du växlingsknappen för att visa de felaktiga identiteterna eller de exkluderade fälten. Felavsnittet innehåller information om felkoden och antalet identiteter som misslyckats eller utelämnats.

![Den filtrerade segmentkontrollpanelen. Information om de identiteter som misslyckades eller uteslöts markeras.](../assets/ui/monitor-segments/activation-job-details.png)

Under segmentavsnittet visas en lista med segment som aktiverats som en del av aktiveringsjobbet. Använd sökfältet för att filtrera listan med segment efter namn.

![Den filtrerade segmentkontrollpanelen. Information om de identiteter som misslyckades eller uteslöts markeras.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Följande mått är tillgängliga för segmentavsnittet:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Name]** | Namnet på det segment som aktiverades. |
| **[!UICONTROL Identities activated]** | Det totala antalet identiteter som aktiverats till målet, baserat på mottagna profiler. |
| **[!UICONTROL Identities excluded]** | Det totala antalet identiteter som uteslöts från att aktiveras till målet, baserat på mottagna profiler. Dessa identiteter kan uteslutas på grund av saknade attribut eller brott mot medgivandet. |
| **[!UICONTROL Last dataflow run status]** | Status för det senaste aktiveringsjobbet som kördes för det segmentet. |
| **[!UICONTROL Last dataflow run date]** | Datum och tid för det senaste aktiveringsjobbet som kördes för det segmentet. |

### Information om utvärderingsjobb {#evaluation-job-details}

Sidan med information om körning av utvärderingsjobbdata visar information om körningens mått och segment som är relaterade till segmentjobbet. Ett utvärderingsjobb är en asynkron process som skapar ett målgruppssegment baserat på det angivna segmentet. Läs självstudiekursen om du vill veta mer om utvärderingsjobb [utvärdera ett segment](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![Kontrollpanelen för utvärderingsjobbet. Information om segmentutvärderingsjobbet visas.](../assets/ui/monitor-segments/evaluation-job-details.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | Det totala antalet profiler som utvärderas. |
| **[!UICONTROL Status]** | Utvärderingsjobbets status. Möjliga statusar för utvärderingsjobbet är bland annat **[!UICONTROL Success]** och **[!UICONTROL Failed]**. |
| **[!UICONTROL Job start]** | Datum och tid då utvärderingsjobbet startades. |
| **[!UICONTROL Job end]** | Datum och tid då utvärderingsjobbet avslutades. |
| **[!UICONTROL Job type]** | Typ av segmentjobb. I det här fallet blir det alltid ett segmentutvärderingsjobb. |
| **[!UICONTROL Evaluation type]** | Typen av utvärdering som görs. Detta kan vara **[!UICONTROL Batch]** eller **[!UICONTROL Streaming]**. |
| **[!UICONTROL Job ID]** | ID för utvärderingsjobbet. |
| **[!UICONTROL IMS org ID]** | ID:t för den IMS-organisation som utvärderingsjobbet tillhör. |
| **[!UICONTROL Segment name]** | Namnet på det segment som utvärderas. |
| **[!UICONTROL Segment ID]** | ID:t för det segment som utvärderas. |

Under segmentavsnittet visas en lista med segment som utvärderas som en del av utvärderingsjobbet. Du kan filtrera listan med segment efter namn med hjälp av sökfältet.

>[!IMPORTANT]
>
>Den här instrumentpanelsvyn har stöd för upp till 800 segmentvärden.

Följande mått är tillgängliga för segmentavsnittet:

| Mått | Beskrivning |
| ------ | ----------- |
| **[!UICONTROL Name]** | Namnet på det segment som utvärderas. |
| **[!UICONTROL Profile count]** | Antalet profiler som utvärderas. |

## Kontrollpanel för segmentjobb {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentjobb"
>abstract="Vyn Segmentjobb innehåller information om utvärderings- och exportjobb för alla segment."

Så här öppnar du **[!UICONTROL Segment Jobs]** kontrollpanel, välja **[!UICONTROL Monitoring]** (![övervakningsikon](../assets/ui/monitor-destinations/monitoring-icon.png)) i den vänstra navigeringen. På [!UICONTROL Monitoring] sida, markera **[!UICONTROL Segment Jobs]**. The [!UICONTROL Monitoring] Kontrollpanelen innehåller mätvärden och information om segmentutvärderingen och exportjobben.

>[!NOTE]
>
>Endast **segmentutvärderingsjobb** stöds för övervakning per segment. Segmentexportjobb har endast stöd för övervakning på organisationsnivå.

![Kontrollpanel för segmentjobbövervakning](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Använd [!UICONTROL Segment Jobs] Instrumentpanelen för att förstå om profilutvärdering och -export sker i tid och utan några undantag, så att de underordnade tjänsterna för målaktivering kan ha de senaste utvärderade profildata.

Följande mått är tillgängliga för segmentjobb:

| Mått | Beskrivning |
---------|----------|
| **[!UICONTROL Segment job]** | Anger segmentjobbets namn. |
| **[!UICONTROL Type]** | Anger typen av segmentjobb - export eller utvärdering. Observera att i båda fallen utvärderas eller exporteras segmentjobbet **alla** segment som tillhör en organisation. Mer information om exportjobb finns i guiden på [slutpunkt för exportjobb](../../segmentation/api/export-jobs.md). Läs självstudiekursen om du vill veta mer om utvärderingsjobb [utvärdera ett segment](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | Datum och tid då segmentjobbet startades. |
| **[!UICONTROL Job end]** | Datum och tid då segmentjobbet slutfördes. |
| **[!UICONTROL Status]** | Status för det slutförda jobbet. Möjliga statusar för segmentjobbet kan vara lyckade eller misslyckade. |
