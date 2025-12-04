---
title: företag
description: Hämta information om den IMS-organisation som äger den implementerade taggegenskapen.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

Objektet `_satellite.company` visar information om den IMS-organisation som äger taggegenskapen.

```ts
readonly _satellite.company: Company
```

## Tillgängliga fält

Följande fält är tillgängliga när det här objektet anropas:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Namn | Typ | Beskrivning |
| --- | --- | --- |
| **`orgId`** | `string` | IMS-organisations-ID för taggegenskapen. |
| **`dynamicCdnEnabled`** | `boolean` | Avgör om taggegenskapen använder Adobe dynamiska CDN-växlingsfunktion. Om värdet är `true` växlar den automatiskt det CDN som en besökare begär din tagg från baserat på deras plats. |
| **`cdnAllowList`** | `string[]` | Tillåtna CDN:er att läsa in taggegenskap från. |

Liknande information finns också i `_satellite._container.company`. Mer information finns i [`_container`](container.md).
