---
title: Sekretess i kunddataprofil i realtid
seo-title: Sekretess i kunddataprofil i realtid
description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
seo-description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Sekretess i CDP i realtid

Med kunddataplattformen i realtid (CDP i realtid) kan marknadsförarna samla data från flera företagssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av CDP-funktionerna i realtid drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika integritetsförbättringstekniker som stöds av CDP i realtid, med länkar till Experience Platform-dokumentationen för mer information.

## Integritetstjänst

Med Adobe Experience Platform Privacy Service kan ni effektivisera processen för att se till att era dataåtgärder är kompatibla med sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA). Eftersom CDP i realtid utnyttjar Experience Platform-funktioner för datainsamling och lagring bör förfrågningar om åtkomst och borttagning för GDPR och CCPA hanteras inom plattformen. En mer detaljerad introduktion till tjänsten finns i översikten över [](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) sekretesstjänsten.

Det finns två metoder för att skicka in enskilda förfrågningar från registrerade personer om GDPR och CCPA för att få tillgång till och ta bort kunddata:

* Använd användargränssnittet [för](https://gdprui.cloud.adobe.io/) sekretesstjänsten för att skapa och övervaka begäranden om åtkomst och borttagning på en visuell arbetsyta. I självstudiekursen [för](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) sekretesstjänsten finns stegvisa instruktioner.
* Använd API:t [för](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) sekretesstjänsten för att hantera åtkomst- och borttagningsbegäranden med RESTful API-anrop. I självstudiekursen [för API:t för](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) sekretesstjänster finns stegvisa instruktioner.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i CDP i realtid. Mer detaljerad information om bästa praxis och steg för att skicka in begäran om åtkomst/borttagning finns i dokumentationen [till](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html)Integritetstjänst.