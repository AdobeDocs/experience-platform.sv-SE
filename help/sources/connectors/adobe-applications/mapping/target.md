---
solution: Experience Platform
title: Mappa Adobe Target-händelsedata till XDM
description: Lär dig hur du mappar Adobe Target-händelsefält till ett XDM-schema (Experience Data Model) som kan användas i Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Mappningar av målmappningsfält

I följande tabell visas fälten i ett Experience Data Model (XDM) Experience Event-schema och motsvarande fält från Adobe Target som de ska mappas till. Ytterligare information om vissa mappningar finns också.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| XDM ExperienceEvent-fält | Fält för målbegäran | Anteckningar |
| ------------------------- | -------------------- | ----- |
| **`id`** | En unik begärandeidentifierare |
| **`dataSource`** | | Konfigurerad till &quot;1&quot; för alla klienter. |
| `dataSource._id` | Ett systemgenererat värde som inte kan skickas med begäran. | Datakällans unika ID. Detta tillhandahålls av den person eller det system som skapade datakällan. |
| `dataSource.code` | Ett systemgenererat värde som inte kan skickas med begäran. | En genväg till det fullständiga @id:t. Minst en av koderna eller @id kan användas. Ibland kallas den här koden för integreringskoden för datakällan. |
| `dataSource.tags` | Ett systemgenererat värde som inte kan skickas med begäran. | Taggar används för att ange hur alias som representeras av en viss datakälla ska tolkas av program som använder dessa alias.<br><br>Exempel:<br><ul><li>`isAVID`: Datakällor som representerar besökar-ID för Analytics.</li><li>`isCRSKey`: Datakällor som representerar alias som ska användas som nycklar i CRS.</li></ul>Taggar anges när datakällan skapas, men de inkluderas även i pipeline-meddelanden när en viss datakälla refereras. |
| **`timestamp`** | Tidsstämpel för händelse |
| **`channel`** | `context.channel` | Fungerar bara med visningsleverans. Alternativen är &quot;web&quot; och &quot;mobile&quot;, med &quot;web&quot; som standard. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience Cloud ID (ECID) kallas även MCID och används även i namnutrymmen. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Mobiloperatörens namn matchades baserat på begärans IP-adress. |
| `environment.ipV4` | `mboxRequest.ipAddress` (om i V4-format) |
| `environment.ipV6` | `mboxRequest.ipAddress` (om i V6-format) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Målets interna mappning för kunddefinierade miljöer (som dev, qa eller prod). |
| `experience.target.supplementalDataID` | Identifierare som används för att sätta ihop Target-händelser med Analytics-händelser |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Lista (matris) med aktiviteter som besökaren har kvalificerat för |
| `experience.target.activities[i].activityID` | ID för en given aktivitet som besökaren är kvalificerad för |
| `experience.target.activities[i].version` | Den version av en viss aktivitet som besökaren är kvalificerad för |
| `experience.target.activities[i].activityEvents` | Innehåller information om aktivitetshändelser som användaren har träffats med den här händelsen. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | En av följande egenskaper i `deviceAtlas` (eller NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (tom sträng) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (tom sträng) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | Slumpmässig UID (obligatoriskt) |
| `placeContext.geo.city` | Ortsnamnet matchades baserat på begärans IP-adress. |
| `placeContext.geo.countryCode` | Landskoden löstes baserat på den begärda IP-adressen. |
| `placeContext.geo.dmaId` | Den utsedda marknadsområdeskoden löstes utifrån den begärda IP-adressen. |
| `placeContext.geo.postalCode` | Postnumret löstes utifrån den begärda IP-adressen. |
| `placeContext.geo.stateProvince` | Stat eller provins löstes utifrån begärans IP-adress. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Ange bara om det finns orderinformation i begäran. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
