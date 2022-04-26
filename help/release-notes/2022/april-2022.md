---
title: Versionsinformation om Adobe Experience Platform april 2022
description: Versionsinformation från april 2022 för Adobe Experience Platform.
source-git-commit: fe30444fb2d11c38433c73d88ee4c8e9a32bdff8
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 april 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataflöden](#dataflows)
- [Experience Data Model (XDM)](#xdm)

## Dataflöden {#dataflows}

I Platform hämtas data från många olika källor, analyseras i systemet och aktiveras till en mängd olika destinationer. Plattformen gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av jobb som flyttar data över plattformen. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av identitetstjänsten och kundprofilen i realtid innan de aktiveras för destinationerna.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontrollpanel för segment | Nu kan du använda kontrollpanelen för övervakning för att övervaka dataflöden för segment. Läs guiden om du vill veta mer [övervaka segment i användargränssnittet](../../dataflows/ui/monitor-segments.md) |

Mer allmän information om dataflöden finns i [dataflödesöversikt](../../dataflows/home.md). Mer information om segmentering finns i [segmenteringsöversikt](../../segmentation/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Lägga till eller ta bort enskilda standardfält för ett schema | Nu kan du lägga till delar av standardfältgrupper i scheman, vilket ger större flexibilitet för de fält du väljer att ta med utan att du behöver skapa anpassade resurser från grunden.<br><br>Nu kan du även definiera egna ad hoc-fält direkt i schemastrukturen och tilldela dem till en ny eller befintlig anpassad fältgrupp utan att behöva skapa eller redigera fältgruppen i förväg.<br><br>Se guiden [skapa och redigera scheman i användargränssnittet](../../xdm/ui/resources/schemas.md) om du vill ha mer information om de nya arbetsflödena. |

{style=&quot;table-layout:auto&quot;}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Globalt schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Hämtar information om en datarensningsbegäran om att ta bort eller ändra poster i en angiven datamängd eller sandlåda. |
| Beskrivning | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Anger granulariteten för tidsserie- och sammanfattningsdata. När schemat tillämpas på ett schema, är schemats `timestamp` fältet är den första tidsstämpeln i en period av den här granulariteten. |
| Klass | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Tillhandahåller försummerade mått med grupperingsdimensioner, t.ex. resultatet av en SQL SELECT med en GROUP BY. |
| Fältgrupp | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hämtar utvärderingsresultatet för principen för samtycke för en individ. |
| Fältgrupp | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hämtar platssökningsrelaterad information som sökfråga, filtrering och ordning. |
| Fältgrupp | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Hämtar information om en händelse där två eller flera leads sammanfogas. |
| Fältgrupp | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Hämtar information om en händelse där ett e-postmeddelande skickas till en mottagare. |
| Fältgrupp | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Hämtar värden som beräknas genom identitetssammanfogningsprocessen för en händelse. |
| Fältgrupp | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | En Adobe Journey Optimizer-fältgrupp som samlar in en sekundär mottagarinformation för en granskning. |
| Fältgrupp | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hämtar information som är relaterad till en konto-person-relation. |
| Fältgrupp | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hämtar information som är relaterad till en konto-person-relation. |
| Datatyp | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Fångar information om en e-handelskundvagn. |
| Datatyp | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Hämtar leveransinformation för en eller flera produkter. |
| Datatyp | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hämtar information om webbplatssökningsaktivitet. |
| Tillägg (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Hämtar information om en operativ uppgift. |
| Tillägg (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Hämtar information om en arbetsportfölj. |
| Tillägg (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Hämtar information om ett arbetsprogram. |
| Tillägg (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Hämtar information om ett arbetsprojekt. |

{style=&quot;table-layout:auto&quot;}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Uppdatera beskrivning |
| --- | --- | --- |
| Globalt schema | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nya uppräkningsvärden för `destinationCategory`. |
| Beskrivning | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Stöd för borttagning av föreslagna värden har lagts till (`meta:enum`) som inte behövs från standardfält. |
| Fältgrupp | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` fältet har lagts till. |
| Datatyp | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Flera kundvagnsrelaterade fält har lagts till. |
| Datatyp | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nya fält har lagts till för valda alternativ och rabattbelopp. |
| Tillägg (Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimera lagringsformatet för bakgrundsmusik. |
| Tillägg (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Flera fält har ersatts med `workfront:customData` fält för anpassade formulärfält. |
| Tillägg (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Flera fält har lagts till. |
| Tillägg (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nya fält för överordnad objekttyp och anpassade formulärfält. |

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

