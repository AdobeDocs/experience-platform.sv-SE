---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappningsfält för Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Mappningsfält för Audience Manager

Tabellerna nedan innehåller mappningarna mellan fälten i Adobe Audience Manager-data (Realtime-, Onboarding- och Profile-data) och deras motsvarande XDM-fält.

Mer information om varje XDM-fält finns i [XDM-fältordlistan](../../../xdm/schema/field-dictionary.md) .

## Realtidsdata

Typ: Realtidsdata

| Datafält för realtid | XDM-fält |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Endast för namnutrymmen som finns i endUserIds och endast det första värdet.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Endast för namnutrymmen som finns i endUserIds och endast det första värdet.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primärHardwareType → typ</li><li>tillverkare → tillverkare</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateRegion</li><li>_stad → ort</li><li>d_mail → mailCode</li><li>d_lat → latitud</li><li>d_longitude → longitud</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os name </li><li>d_os_version → os_version</li></ul> |
| `Signals` | ExperienceEvent.signals |

## Inkommande data **(inaktuellt)**

Typ: ExperienceEvent

| Inkommande fält | XDM-fält |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Inkommande fält är schemalagda att bli inaktuella i en framtida version.

## Profildata

Typ: Profil-XDM

| Profilfält | XDM-fält |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
