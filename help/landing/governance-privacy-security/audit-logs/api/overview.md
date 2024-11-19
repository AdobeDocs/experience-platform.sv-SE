---
title: API-guide för granskningsfrågor
description: Granskningsfrågan är ett RESTful-API som gör att utvecklare kan se vem som gjorde vilka åtgärder i Adobe Experience Platform.
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---

# API-guide för [!DNL Audit Query]

API:t [!DNL Audit Query] innehåller slutpunkter som gör att du kan hämta och övervaka händelsedata för olika Adobe Experience Platform-funktioner. Slutpunkterna anges nedan. Besök [Komma igång-guiden](./getting-started.md) om du vill ha viktig information om nödvändiga huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [[!DNL Audit Query] API-växlaren](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Händelser

Granskningshändelser ger insikter om användaråtgärder i Platform, inklusive åtgärdstyp, datum och tid, e-post-ID för den användare som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen för olika funktioner i Adobe Experience Platform. Mer information om hur du hämtar mätvärden med API:t finns i [händelsens slutpunktshandbok](./events.md).

## Exportera

Med granskningsexport kan du hämta händelsedata genom att ange vilka händelser som ska hämtas i nyttolasten. Mer information om hur du hämtar mätvärden med API:t finns i [exportslutpunktshandboken](./export.md).
