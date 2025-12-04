---
title: getVisitorId
description: Hämta tilläggsinstansen för servicemärke för Experience Cloud Visitor ID.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

Metoden `_satellite.getVisitorId()` returnerar en instans av [Adobe Experience Cloud ID-tjänsten](https://experienceleague.adobe.com/sv/docs/id-service/using/home) i taggegenskapen, **om** du har ID-tjänsttillägget installerat och publicerat. Den här metoden är användbar när du vill ha direktåtkomst till besökar-ID-instansen för användning i anpassade kodblock, avancerad dataelementskonfiguration eller felsökning av identitetsproblem för besökare.

>[!IMPORTANT]
>
>Den här metoden gäller bara för egenskaper som innehåller det fristående tillägget för servicemärket Experience Cloud ID. Det gäller inte de implicita ID-tjänstfunktioner som finns i Web SDK-taggtillägget. Se kommandot [`getIdentity`](/help/collection/js/commands/getidentity.md) om du behöver hämta en besöksidentitet med hjälp av de implicita ID-tjänstfunktionerna i Web SDK.

Om du anropar den här metoden med ID-tjänsttillägget installerat och publicerat returneras ett objekt som liknar det objekt som erhållits efter anropet till metoden [`Visitor.getInstance()`](https://experienceleague.adobe.com/sv/docs/id-service/using/id-service-api/methods/getinstance). Om du anropar den här metoden när ID-tjänsttillägget inte är installerat eller publicerat returnerar metoden `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Tillgängliga fält och metoder

Se Experience Cloud ID-tjänsten [Metoder](https://experienceleague.adobe.com/sv/docs/id-service/using/id-service-api/methods/get-set) i dokumentationen för Experience Cloud Visitor ID-tjänsten för att se vilka fält och metoder som är tillgängliga för dig.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
