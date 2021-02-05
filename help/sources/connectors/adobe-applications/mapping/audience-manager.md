---
keywords: Experience Platform;hem;populära ämnen;Audience Manager-mappning;målgruppshanterarmappning
solution: Experience Platform
title: Mappningsfält för Adobe Audience Manager Source Connector
topic: overview
description: Lär dig hur du mappar Adobe Audience Manager-data (realtids-, onboardations- och profildata) till motsvarande XDM-fält (Experience Data Model) för Audience Manager-källkopplingen.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Fältkopplingar i Audience Manager

Tabellerna nedan innehåller mappningarna mellan fälten i Adobe Audience Manager-data (Realtime-, On-board- och Profile-data) och deras motsvarande XDM-fält.

Mer information om varje XDM-fält finns i [XDM-fältordlistan](../../../../xdm/schema/field-dictionary.md).

## Realtidsdata

Typ: Realtidsdata

| Datafält för realtid | XDM-fält |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *Endast för namnutrymmen som finns i endUserIds och endast det första värdet.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Endast för namnutrymmen som finns i endUserIds och endast det första värdet.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primärHardwareType → typ</li><li>tillverkare → tillverkare</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateRegion</li><li>d_city → stad</li><li>d_mail → mailCode</li><li>d_lat → latitud</li><li>d_longitude → longitud</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os name </li><li>d_os_version → os_version</li></ul> |

## Profildata

Typ: Profil-XDM

| Profilfält | XDM-fält |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
