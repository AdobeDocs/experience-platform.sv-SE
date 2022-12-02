---
title: API-guide för granskningsfrågor
description: Granskningsfrågan är ett RESTful-API som gör att utvecklare kan se vem som gjorde vilka åtgärder i Adobe Experience Platform.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# [!DNL Audit Query] API-guide

The [!DNL Audit Query] API innehåller slutpunkter som gör att du kan hämta och övervaka händelsedata för olika Adobe Experience Platform-funktioner programmatiskt. Slutpunkterna anges nedan. Besök [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Audit Query] API-växling](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Händelser

Granskningshändelser ger insikter om användaråtgärder i Platform, inklusive åtgärdstyp, datum och tid, e-post-ID för den användare som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen för olika funktioner i Adobe Experience Platform. Om du vill lära dig hur du hämtar mätvärden med API:t kan du läsa [slutpunktsguide för händelser](./events.md).

## Exportera

Med granskningsexport kan du hämta händelsedata genom att ange vilka händelser som ska hämtas i nyttolasten. Om du vill lära dig hur du hämtar mätvärden med API:t kan du läsa [slutpunktsguide för export](./export.md).
